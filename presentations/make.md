title: hexlet.io
author:
  name: Kirill Mokevnin
  twitter: hexletHQ
  url: https://hexlet.io
style: style.css

--

# hexlet.io
## Make (as universal tool)

--

### Задумка

> Утилита для автоматизации сборки исполняемых программ и библиотек из исходного кода.

```makefile
# Makefile
program: main.o lib.o
    cc -o program main.o lib.o
    main.o lib.o: defines.h
```

--

### Особенности

* Появилась в 1977 году.
* Включена в большинство `*nix` дистрибутивов.
* Повсеместно используется для сборки ПО из исходников.

--

### Зачем?

> Универсальная автоматизация часто повторяющихся задач.

```sh
 (master) vagrant$ make start

 sudo service webserver restart
 webserver stop/waiting
 webserver start/running, process 11904
 sudo service activejob restart
```

--

### Примеры использования

```sh
make install # установка зависимостей
make test # запуск тестов
make start # запуск проекта
make deploy # развертывание
make docs # генерация документации
make dump_restore # разворачивание дампа
```

--

### А существующая автоматизация?

* ruby: `rake`, `foreman`
* javascript: `gulp`, `grant`, `npm scripts`
* php: `composer`, `phing`
* python: `fabric`, `pydoit`
* java: `gradle`, `ant`, `maven`

--

### Польза

* Унификация в гетерогенной среде.
* Зависимости между задачами.
* Самодокументирование.
* Автоматизация cli задач.
* Межпроектная стандартизация.

--

### Примеры Хекслета

```makefile
# Makefile

install:
    bundle install -j2
    npm install

start:
    sudo service webserver restart
    sudo service nginx restart

logs:
    sudo tail -f /var/log/upstart/webserver.log

retry:
    for i in {1..5}; do $(CMD) && break \
    || sleep 3; done
```

--

### Инструкция по применению

```makefile
# Makefile

test:
    RAILS_ENV=test make frontend
    bin/rake test

deploy: test
    ansible-playbook deploy.yml -i $(E) -u $(U) -v
```

```sh
# Bash

make test

make deploy E=production U=ubuntu
```

--

### PHONY

```makefile
# Makefile
test:
    echo 'run tests...'
```


```sh
# Bash
(master) hexlet$ ls
test

make test
make: `test` is up to date.
```

```makefile
# Makefile last line
.PHONY: test log
```
