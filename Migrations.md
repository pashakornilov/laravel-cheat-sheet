## Migrations

- [Консольные команды](#консольные-команды)
- [Типы данных](#типы-данных)
- [Модификаторы](#модификаторы-столбцов)
- [Индексы](#индексы)

### Консольные команды

#### Выполнить миграции:

```console
php artisan migrate
```

#### Создать новый файл миграции:

```console
php artisan make:migration CreatePostsTable
```

#### Очистка базы данных перед миграцией

```shell
php artisan migrate:fresh
```
#### Сброс и повторное выполнение всех миграций:

```shell
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


### Типы данных

**Числовые типы данных:**

| Тип данных        | Описание                                    |
|-------------------|--------------------------------------------|
| `bigIncrements`   | Большой целочисленный столбец с автоинкрементом |
| `bigInteger`      | Большой целочисленный столбец                |
| `boolean`         | Булев                                      |
| `decimal`         | Десятичное число                            |
| `double`          | Двойная точность числа                     |
| `increments`      | Целочисленный столбец с автоинкрементом    |
| `integer`         | Целочисленный столбец                      |
| `float`           | Вещественное число                         |

**Типы данных для работы с текстом и строками:**

| Тип данных        | Описание                                    |
|-------------------|--------------------------------------------|
| `char`            | Строковый столбец фиксированной длины       |
| `string`          | Строковый столбец                          |
| `text`            | Текстовый столбец                          |

**Типы данных для работы с датами и временем:**

| Тип данных        | Описание                                    |
|-------------------|--------------------------------------------|
| `date`            | Дата в формате "год-месяц-день"            |
| `dateTime`        | Дата и время в формате ISO8601             |
| `time`            | Время в формате "часы:минуты:секунды"     |
| `timestamp`       | Временная метка (дата и время)            |
| `timestamps`      | Две временные метки (created_at и updated_at) |

**Типы данных для работы с JSON и бинарными данными:**

| Тип данных        | Описание                                    |
|-------------------|--------------------------------------------|
| `json`            | JSON-данные                                |
| `jsonb`           | JSONB-данные (бинарный JSON)               |
| `binary`          | Бинарные данные                            |

**Типы данных для перечислений и полиморфных отношений:**

| Тип данных        | Описание                                    |
|-------------------|--------------------------------------------|
| `enum`            | Перечисление                               |
| `morphs`          | Полиморфное отношение                      |

**Специальные типы данных:**

| Тип данных        | Описание                                    |
|-------------------|--------------------------------------------|
| `longText`        | Длинный текстовый столбец                  |
| `uuid`            | Уникальный идентификатор (UUID)           |


### Модификаторы

| Описание | Код | Поддерживаемые СУБД |
|----------|--------|--------------------|
| Переместить столбец "email" после столбца "username". | `$table->string('email')->after('username')->nullable();` | MySQL |
| Установить столбец "id" как автоинкрементирующийся (первичный ключ). | `$table->increments('id');` | MySQL, PostgreSQL, SQLite |
| Указать набор символов "utf8mb4" для столбца "content". | `$table->string('content')->charset('utf8mb4');` | MySQL |
| Указать каталожное сравнение "utf8mb4_unicode_ci" для столбца "name". | `$table->string('name')->collation('utf8mb4_unicode_ci');` | MySQL, PostgreSQL, SQL Server |
| Добавить комментарий к столбцу "description". | `$table->string('description')->comment('Описание столбца');` | MySQL, PostgreSQL |
| Установить значение "по умолчанию" для столбца "status". | `$table->string('status')->default('active');` | MySQL, PostgreSQL |
| Поместить столбец "created_at" в начало таблицы. | `$table->timestamp('created_at')->first();` | MySQL |
| Установить начальное значение 100 для автоинкрементирующегося поля "order_id". | `$table->increments('order_id')->from(100);` | MySQL, PostgreSQL |
| Сделать столбец "secret_key" невидимым для запросов SELECT * | `$table->string('secret_key')->invisible();` | MySQL |
| Разрешить вставку NULL-значений в столбец "notes". | `$table->string('notes')->nullable();` | MySQL, PostgreSQL |
| Создать вычисляемый столбец "total_price" на основе выражения. | `$table->float('total_price')->storedAs('price * quantity');` | MySQL, PostgreSQL |
| Установить INTEGER-столбцы, чтобы использовать CURRENT_TIMESTAMP как значение "по умолчанию" | `$table->integer('votes')->unsigned();` | MySQL |
| Установить TIMESTAMP-столбцы, чтобы использовать CURRENT_TIMESTAMP при обновлении записи | `$table->timestamp('updated_at')->useCurrentOnUpdate();` | MySQL |
| Создать столбец с автоинкрементом с указанными параметрами последовательности | `$table->bigIncrements('id')->generatedAs('nextval(\'my_sequence\')');` | PostgreSQL |
| Определить приоритет значений последовательности над входными данными для столбца с автоинкрементом | `$table->bigIncrements('id')->always();` | PostgreSQL |
| Установить тип пространственного столбца "location" как "geometry" | `$table->geometry('location')->isGeometry();` | PostgreSQL |


### Индексы

| Описание | Пример | Поддерживаемые СУБД |
|----------|--------|--------------------|
| Добавить первичный ключ на столбец "id" | `$table->primary('id');` | MySQL, PostgreSQL, SQLite |
| Добавить составной первичный ключ на столбцы "id" и "parent_id" | `$table->primary(['id', 'parent_id']);` | MySQL, PostgreSQL, SQLite |
| Добавить уникальный индекс на столбец "email" | `$table->unique('email');` | MySQL, PostgreSQL, SQLite |
| Добавить обычный индекс на столбец "state" | `$table->index('state');` | MySQL, PostgreSQL, SQLite |
| Добавить полнотекстовый индекс на столбец "body" | `$table->fullText('body');` | MySQL, PostgreSQL |
| Добавить полнотекстовый индекс на столбец "body" | `$table->fullText('body')->language('english');` | PostgreSQL |
| Добавить пространственный индекс на столбец "location" | `$table->spatialIndex('location');` | MySQL, PostgreSQL |


### Рекомендации

#### Используйте осмысленные имена миграций

```php
// Эта миграция создает таблицу для хранения информации о пользователях
CreateUsersTable
```


#### Список популярных префиксов для именования миграций

| Префикс | Назначение | Пример |
|-|-|-|  
| create_ | Создание таблицы | create_users_table |
| add_ | Добавление столбца |  add_votes_column |
| remove_ | Удаление столбца | remove_deprecated_columns |
| drop_ | Удаление таблицы | drop_temp_table |
| alter_ | Изменение столбца | alter_user_password_column |
| rename_ | Переименование таблицы/столбца | rename_table_users_to_profiles |
| optimize_ | Оптимизация таблицы | optimize_users_table |
| modify_ | Модификация таблицы | modify_posts_table_charset |
| populate_ | Заполнение таблицы | populate_posts_table |
| reset_ | Сброс auto_increment | reset_auto_increment_id |
| restore_ | Восстановление из backup | restore_posts_from_backup |


#### Добавляйте комментарии в миграции  

```php
/**
 * Add votes column to users table.
 */ 
public function up()
{
  Schema::table('users', function (Blueprint $table) {
    $table->integer('votes');
  });
}
```


#### Разделяйте большие миграции 

Если миграция получается слишком большой, разделите её на несколько отдельных миграций по логическим блокам.


#### Реализуйте `down()` противоположно `up()`

Метод `down()` должен действовать противоположно `up()`:

```php 
public function up()
{
  Schema::create('users');
}

public function down()
{
  Schema::drop('users');
}
```


#### Добавляйте в .gitignore сгенерированные миграции

```
/database/migrations/*
!/database/migrations/README.md
```

Это проигнорирует все миграции, кроме README.


#### Тестируйте откаты перед продакшеном

Перед применением миграций на продакшене протестируйте откаты:

```
php artisan migrate
php artisan migrate:rollback
```


#### Используйте seeds после миграций 

Seeds позволяют заполнить БД тестовыми данными. Используйте после миграций:

```
php artisan migrate
php artisan db:seed
```


#### Следите за порядком миграций

Следите, чтобы миграции выполнялись в правильном порядке без ошибок зависимостей.


#### Не изменяйте применённые миграции

Не изменяйте уже применённые на продакшене миграции. Создавайте новые миграции для изменений.