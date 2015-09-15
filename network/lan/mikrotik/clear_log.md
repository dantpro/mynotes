# Очистка логов

Создаем скрипт со следующим текстом и выполняем, когда надо очистить логи:

```
/system logging action
set 0 memory-lines=1
set 0 memory-lines=1000
```
