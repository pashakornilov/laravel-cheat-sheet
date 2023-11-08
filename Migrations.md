
### Консольные команды
#### Выполнить миграции:

   ```console
   php artisan migrate
   ```

#### Создать репозиторий для миграций:

   ```console
   php artisan migrate:install
   ```

#### Создать новый файл миграции:

   ```console
   php artisan migrate:make name
   ```

#### Сброс и повторное выполнение всех миграций:

   ```console
   php artisan migrate:refresh
   ```

#### Отмена всех миграций базы данных:

   ```console
   php artisan migrate:reset
   ```

#### Откат последней миграции базы данных:

   ```console
   php artisan migrate:rollback
   ```

#### Публикация миграций пакета в директорию миграций:

   ```console
   php artisan migrate:publish vendor/package
   ```