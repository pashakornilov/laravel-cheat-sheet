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

#### **Целочисленные столбцы**:

```php
// Очень маленький целочисленный столбец (диапазон: -128 до 127)
$table->tinyInteger('rating');
$table->unsignedTinyInteger('level');

// Маленький целочисленный столбец (диапазон: -32_768 до 32_767)
$table->smallInteger('weight');

// Маленький целочисленный столбец с автоинкрементом (диапазон: 0 до 65_535)
$table->smallIncrements('category_id');

// Средний целочисленный столбец (диапазон: -8_388_608 до 8_388_607)
$table->mediumInteger('size');

// Средний целочисленный столбец с автоинкрементом (диапазон: 0 до 16_777_215)
$table->mediumIncrements('product_id');
$table->unsignedMediumInteger('views');

// Целочисленный столбец (диапазон: -2_147_483_648 до 2_147_483_647)
$table->integer('age');

// Целочисленный столбец с автоинкрементом (диапазон: 0 до 4_294_967_295)
$table->increments('order_id');
$table->unsignedInteger('votes');

// Большой целочисленный столбец без знака (диапазон: 0 до 18_446_744_073_709_551_615)
$table->unsignedBigInteger('account_id');

// Большой целочисленный столбец (диапазон: -9_223_372_036_854_775_808 до 9_223_372_036_854_775_807)
$table->bigInteger('quantity');

// Большой целочисленный столбец с автоинкрементом (диапазон: 0 до 9_223_372_036_854_775_807)
$table->bigIncrements('id');

// Десятичное число без знака (диапазон: от 0 до 99_999.99)
$table->unsignedDecimal('price', 8, 2);
```

#### **Строковые столбцы**:

```php
// Строковый столбец с фиксированной длиной (максимальная длина: 255 символов)
$table->char('code', 255);

// Строковый столбец (максимальная длина: 1_000 символов)
$table->string('title', 1000);

// Текстовый столбец (максимальная длина: 65_535 символов)
$table->text('description');

// Очень короткий текстовый столбец (максимальная длина: 255 символов)
$table->tinyText('short_description');

// Средний текстовый столбец (максимальная длина: 16_777_215 символов)
$table->mediumText('content');

// Длинный текстовый столбец (максимальная длина: 4_294_967_295 символов)
$table->longText('full_text');
```

#### **Дата и время**:

```php
// Пример вывода для типа time (без временной зоны)
$table->time('event_time'); // '12:30:45'

// Пример вывода для типа timeTz (с временной зоной)
$table->timeTz('event_time_with_tz'); // '12:30:45 +03:00'

// Пример вывода для типа date
$table->date('event_date'); // '2023-11-08'

// Пример вывода для типа dateTime (без временной зоны)
$table->dateTime('event_datetime'); // '2023-11-08 12:30:45'

// Пример вывода для типа timestamps (с меткой времени, без временной зоны)
$table->timestamps(); // 'created_at': '2023-11-08 12:30:45', 'updated_at': '2023-11-08 13:45:30'

// Пример вывода для типа timestampsTz (с меткой времени, с временной зоной)
$table->timestampsTz(); // 'created_at': '2023-11-08 12:30:45 +03:00', 'updated_at': '2023-11-08 13:45:30 +03:00'

// Пример вывода для типа timestamp (с меткой времени, без временной зоны)
$table->timestamp('event_timestamp'); // '2023-11-08 12:30:45'

// Пример вывода для типа timestampTz (с меткой времени, с временной зоной)
$table->timestampTz('event_timestamp_with_tz'); // '2023-11-08 12:30:45 +03:00'

// Пример вывода для типа dateTimeTz (с временной зоной)
$table->dateTimeTz('event_datetime_with_tz'); // '2023-11-08 12:30:45 +03:00'
```

#### **Числа с плавающей запятой**:

```php
// Пример вывода для типа float
$table->float('amount'); // 123.45

// Пример вывода для типа double
$table->double('price'); // 123.4567

// Пример вывода для типа decimal
$table->decimal('total', 8, 2); // 12345.67

```

#### **JSON и связанные типы**:

```php
// Пример вывода для типа json
$table->json('data'); // {"key": "value"}

// Пример вывода для типа jsonb
$table->jsonb('settings'); // {"setting1": "value1", "setting2": "value2"}

```

#### **Логический тип**:

```php
// Пример вывода для типа boolean
$table->boolean('is_active'); // true или false
```

#### **Перечисление (Enum)**:

```php
// Пример вывода для типа enum
$table->enum('status', ['active', 'inactive', 'pending']); // 'active', 'inactive' или 'pending'
```

#### **IP-адрес**:

```php
// Пример вывода для типа ipAddress
$table->ipAddress('user_ip'); // '192.168.1.1'
```

#### **Геометрические типы**:

```php
// Пример вывода для типа point
$table->point('location'); // 'POINT(12.345 67.890)'

// Пример вывода для типа lineString
$table->lineString('path'); // 'LINESTRING(1 1, 2 2, 3 3)'

// Пример вывода для типа polygon
$table->polygon('area'); // 'POLYGON((0 0, 0 1, 1 1, 1 0, 0 0))'

// Пример вывода для типа multiPoint
$table->multiPoint('locations'); // 'MULTIPOINT(1 2, 3 4)'

// Пример вывода для типа multiLineString
$table->multiLineString('routes'); // 'MULTILINESTRING((0 0, 1 1), (2 2, 3 3))'

// Пример вывода для типа multiPolygon
$table->multiPolygon('regions'); // 'MULTIPOLYGON(((0 0, 0 1, 1 1, 1 0, 0 0), (2 2, 3 3, 4 4, 2 2)))'

// Пример вывода для типа geometry
$table->geometry('shape'); // 'GEOMETRYCOLLECTION(POINT(1 1), LINESTRING(0 0, 1 1))'

// Пример вывода для типа geometryCollection
$table->geometryCollection('shapes'); // 'GEOMETRYCOLLECTION(POINT(1 1), LINESTRING(0 0, 1 1))'
```

#### **Другие типы**:

```php
// Пример вывода для типа binary
$table->binary('data'); // (бинарные данные)

// Пример вывода для типа ulid
$table->ulid('identifier'); // '01ARZ3NDEKTSV4RRFFQ69G5FAV'

// Пример вывода для типа uuid
$table->uuid('guid'); // '550e8400-e29b-41d4-a716-446655440000'

// Пример вывода для типа year
$table->year('event_year'); // 2023
```

#### **Специфические типы для миграции**:

```php
// Пример вывода для типа rememberToken
$table->rememberToken();

// Пример вывода для типа set
$table->set('options', ['option1', 'option2', 'option3']); // 'option1,option2'

// Пример вывода для типа softDeletes
$table->softDeletes();

// Пример вывода для типа softDeletesTz
$table->softDeletesTz();

// Пример вывода для типа morphs
$table->morphs('commentable');

// Пример вывода для типа nullableMorphs
$table->nullableMorphs('nullable_commentable');

// Пример вывода для типа nullableTimestamps
$table->nullableTimestamps();

// Пример вывода для типа nullableUlidMorphs
$table->nullableUlidMorphs('nullable_morphable');

// Пример вывода для типа nullableUuidMorphs
$table->nullableUuidMorphs('nullable_uuid_morphable');
```

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