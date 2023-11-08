## Migrations

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
   php artisan make:migration create_posts_table
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


### Типы данных
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
