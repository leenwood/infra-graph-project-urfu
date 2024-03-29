## Backend documentation

Клонируем репозиторий в раздел с ядром линукса. Это важно так как из-за разности файловой системы винды и докера, если залить на обычный диск, то при конфертации туда или обратно, занимает много времени из-за чего фреймворк работает очень медленно и не успевает отправить ответ.

Скрин находиться в корне проекта

```bash
git clone --recursive https://github.com/leenwood/infra-graph-project-urfu.git
```

```bash
cd infra-graph-project-urfu
```

```bash
cp .env.dist .env
```

Монтируем образы докера
```bash 
docker-compose build
```
Ждем пока домантируется образы
Поднимаем докер в режиме демона
```bash 
docker-compose up -d
```

Разворачиваем симфони в докере
```bash 
docker exec -it graph-backend-app-php-fpm composer install
```

Теперь можно зайти в браузер по ссылке localhost:8000 и увидеть окно привествия от симфони.

Создаем базу данных
```bash
docker exec -it graph-backend-app-php-fpm php bin/console doctrine:database:create
```

Обновляем информацию о базе данных
```bash
docker exec -it graph-backend-app-php-fpm php bin/console doctrine:migrations:migrate
```

Генерируем себе ключи 
```bash
docker exec -it graph-backend-app-php-fpm php bin/console lexik:jwt:generate-keypair
```

Makefile
```bash
cp Makefile.example Makefile //создание Makefile
make first-build //для первого запуска чтобы создалась база данных
//либо
make build //просто чтобы поднять проект
```