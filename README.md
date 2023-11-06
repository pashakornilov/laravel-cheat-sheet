# laravel-cheat-sheet

## Маршруты

```php
// Регистрация GET-маршрута с использованием замыкания

Route::get('sheets', function(){});
```

```php
// Регистрация GET-маршрута с использованием контроллера, логика находится в методе index контроллера SheetController.

Route::get('sheets', 'SheetController@index');
Route::get('sheets', [SheetController::class, 'index']);
```