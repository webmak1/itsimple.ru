# Исходники сайта [itsimple.ru](https://itsimple.ru)

Запустить itsimple.ru на своем хосте с использованием docker контейнера:

    $ docker run -i -t -p 80:80 --name itsimple.ru marley/itsimple.ru

<br/>

### Как сервис

    # vi /etc/systemd/system/itsimple.ru.service

вставить содержимое файла itsimple.ru.service

    # systemctl enable itsimple.ru.service
    # systemctl start  itsimple.ru.service
    # systemctl status itsimple.ru.service

http://localhost:4006

<br/>

### Вариант для внесения изменений

Инсталлируете docker и docker-compose, далее:

    $ cd ~
    $ mkdir -p itsimple.ru && cd itsimple.ru
    $ git clone --depth=1 https://bitbucket.org/itsimple-ru/itsimple.ru.git .
    $ docker-compose up

<br/>

Остается в браузере подключиться к localhost:80
