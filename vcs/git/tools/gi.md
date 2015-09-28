# gitignore.io

Очень полезная утилитка для генерации файла .gitignore по заданому шаблону.

Установка для bash и zsh:
```sh
echo "function gi() { curl -L -s https://www.gitignore.io/api/\$@ ;}" >> ~/.bashrc && source ~/.bashrc
echo "function gi() { curl -L -s https://www.gitignore.io/api/\$@ ;}" >> ~/.zshrc && source ~/.zshrc
```

Использование:
```sh
gi osx,yii,phpstorm
```

Список возможных условий:
```sh
gi list
```
