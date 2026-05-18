docker-compose.yaml
```yaml
version: '3.5'

services:
  mysql:
    container_name: mysql_container
    image: mysql
    environment:
      MYSQL_DATABASE: ${MYSQL_DATABASE:-yourdatabase}
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD:-setrootpassword}
      MYSQL_USER: ${MYSQL_USER:-dbuser}
      MYSQL_PASSWORD: ${MYSQL_USER:-dbpassword}
    ports:
      - "3306:3306"
    networks:
      - mysql
    restart: always
  
  phpmyadmin:
    container_name: phpmyadmin_container
    image: phpmyadmin/phpmyadmin
    environment:
      PMA_ARBITRARY: 1
      PMA_HOST: mysql
      PMA_PORT: 3306     
    depends_on:
      - mysql
    links:
      - mysql      
    ports:
      - "9999:80"
    networks:
      - mysql
    restart: always

networks:
  mysql:
    driver: bridge

volumes:
    mysql:  
```