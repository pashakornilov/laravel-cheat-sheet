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
#### Числа

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

#### Строки

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