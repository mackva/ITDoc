
#### Как удалить appsettings.Development.json из всех коммитов
```sh
git filter-branch --force --index-filter \
'git rm --cached --ignore-unmatch src/appsettings.Development.json' \
--prune-empty --tag-name-filter cat -- --all


git push origin --force --all
git push origin --force --tags
```