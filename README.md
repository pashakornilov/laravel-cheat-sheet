# laravel-cheat-sheet

## Маршруты

Пример: http://example.com/articles

```php
// Регистрация GET-маршрута с использованием замыкания

Route::get('articles', function(){});
```

```php
// Регистрация GET-маршрута с использованием контроллера

Route::get('articles', 'SheetController@index');
Route::get('articles', [SheetController::class, 'index']);
```