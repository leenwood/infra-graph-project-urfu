## Backend documentation

Клонируем репозиторий в раздел с ядром линукса. Это важно так как из-за разности файловой системы винды и докера, если залить на обычный диск, то при конфертации туда или обратно, занимает много времени из-за чего фреймворк работает очень медленно и не успевает отправить ответ.

Скрин находиться в корне проекта

```git
git clone https://github.com/leenwood/infra_badoo_backend_app.git
```
### Открываем терминал

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
docker exec -it urfu_moment-php-fpm composer install
```

Теперь можно зайти в браузер по ссылке localhost:8000 и увидеть окно привествия от симфони.

Обновляем информацию о базе данных
```bash
docker exec -it urfu_moment-php-fpm php bin/console doctrine:migrations:migrate
```

Следом нужно создать пользователя для работы и подключения в реакт приложение
```bash
docker exec -it urfu_moment-php-fpm php bin/console user:create Nikita 123321 -a true
```

Генерируем себе ключи 
```bash
docker exec -it urfu_moment-php-fpm php bin/console lexik:jwt:generate-keypair
```