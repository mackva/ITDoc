### Непрерывная интеграция в gitea

1) Создаем новый репозиторий в Gitea http://192.168.1.31:3000 (см пример [MissJulia.Telegram.Bot](http://192.168.1.31:3000/mackva/MissJulia.Telegram.Bot))
2) В настройках проекта включаем пакеты и действия.
3) Создаем токен пользователя. Заводим в Параметры пользователя (Настройки) => Приложения => Управление токенами. Создаем  токен для публикации Docker образов. 
4) Добавить секреты. Заводим в Параметры пользователя => Действия => Секреты, и добавляем два секрета например DOCKER_HUB_USERNAME, DOCKER_HUB_ACCESS_TOKEN со значениями логина и токена из прошлого шага
5) Добавляем в Portener registries. Заходим в Registries => Custom registry => gitea/Ip/DOCKER_HUB_USERNAME/DOCKER_HUB_ACCESS_TOKEN
6) Добавляем действия (CI) в наш репозиторий. Создаем файла [publish.yaml](http://192.168.1.31:3000/mackva/MissJulia.Telegram.Bot/src/branch/master/.gitea/workflows/publish.yaml) в папке  .gitea\\workflows

Имя рабочего процесса, которое будет отображаться в разделе «Действия».
```
name: Build-and-publish
```

Указывает триггер для этого рабочего процесса. В этом примере используется событие push в ветку master.
```
on:
  push:
    branches: [ master ]
```

Объявляем переменные окружения 
```
env:
  # Use docker.io for Docker Hub if empty
  REGISTRY: 192.168.1.31:3000
  # gitea.repository as <account>/<repo>
  IMAGE_NAME: ${{ gitea.repository }}
```
Группирует все задания, которые выполняются в рабочем процессе **Build-and-publish**. Определяет задание с именем publish.  Настраивает задание для запуска в последней версии среды выполнения Ubuntu. Это означает, что задание будет выполняться на новой виртуальной машине, размещенной на Gitea. 
Контейнер **catthehacker/ubuntu:act-latest** настроен специально для GitHub/Gitea действий.
```
jobs:
  publish:
    runs-on: ubuntu-latest
    container:
      image: catthehacker/ubuntu:act-latest
```
Группирует все шаги, выполняемые в задании publish. Ключевое слово **uses** указывает, что на этом шаге будет выполняться 3 версия actions/checkout. Это действие клонирует репозиторий в рабочую директорию.
```
    steps:
    - uses: actions/checkout@v3
```
Далее устанавливаем .NET, восстанавливаем зависимости, белим и публикуем наш проект, А так же копируем dockerfile. 
```
    - name: Setup .NET
      uses: actions/setup-dotnet@v2
      with:
        dotnet-version: 6.0.x
    - name: Restore dependencies
      run: dotnet restore
    - name: Build
      run: dotnet build --configuration Release --no-restore
    - name: Test
      run: dotnet test --no-restore --verbosity normal
    - name: Publish     
      run: dotnet publish --no-restore --output "linux64_musl"
    - name: Copy dockerfile 
      run: mv ci/Dockerfile linux64_musl/Dockerfile
```
Отобразим содержимое папки linux64_musl
```
    - name: List files in the repository
      run: |
        ls ${{github.workspace}}/linux64_musl
```
Устанавливаем QEMU это универсальный эмулятор и виртуализатор машины и пользовательского пространства с открытым исходным кодом. Он нужен для создания мультиплатформенного образ, см шаг docker/build-push-action и platforms: linux/arm64
```
    - name: Set up QEMU
      uses: docker/setup-qemu-action@v3  
```

Действие для извлечения метаданных из ссылок и событий Gitea.  Полученные метаданных используется в  Используется в действие docker/build-push-action для labels и tags docker образа.
```
    - name: Docker meta
      id: meta
      uses: docker/metadata-action@v5
      with:
        images: ${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}
        flavor: |
          latest=auto  
```
Устанавливаем BuildX это плагин Docker CLI для расширенных возможностей сборки с помощью BuildKit. 
Аргумент config-inline, устанавливает реестр как небезопасный, позволяя нам использовать локальный реестр с http вместо https.
```  
      # setup Docker buld action
    - name: Set up Docker BuildX
      uses: docker/setup-buildx-action@v3
      with:
        config-inline: |
          [registry."${{ env.REGISTRY }}"]
            http = true
            insecure = true             
```
Входим в наш локальный DockerHub с использованием секретов, которые мы установили ранее. 
```
    - name: Login to DockerHub
      uses: docker/login-action@v3
      with:
        registry: ${{ env.REGISTRY }}
        username: ${{ secrets.DOCKER_HUB_USERNAME }}
        password: ${{ secrets.DOCKER_HUB_ACCESS_TOKEN }}
```
Собираем и публикуем наш docker образ под платформу arm64
```
    - name: Build image and push to Docker Hub
      uses: docker/build-push-action@v5
      with:
        # relative path to the place where source code with Dockerfile is located
        context: ${{github.workspace}}/linux64_musl
        platforms: linux/arm64
        # Note: tags has to be all lower-case 
        tags: ${{ steps.meta.outputs.tags }}
        labels: ${{ steps.meta.outputs.labels }}
        push: true
```
Показать дайджест изображения
```
    - name: Image digest
      run: echo ${{ steps.docker_build.outputs.digest }}
```

Возможные ошибки:
1) http: server gave HTTP response to HTTPS client [[Troubleshoot Docker]]
