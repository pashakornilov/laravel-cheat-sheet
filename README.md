# laravel-cheat-sheet

## Route

Пример: http://example.com/articles

### Define route

```php
// Регистрация GET-маршрута с использованием замыкания
Route::get('/articles', function(){});

// Регистрация GET-маршрута с использованием контроллера
Route::get('/articles', 'SheetController@index');
Route::get('/articles', [SheetController::class, 'index']);
```

### HTTP Verbs

```php
// Опции для определения доступных http методов
Route::options('/articles', function() {});

// Получение данных с сервера
Route::get('/articles', function() {});

// Отправка данных на сервер
Route::post('/articles', function() {});

//  Обновление существующего ресурса
Route::put('/articles', function() {});

// Частичное обновление ресурса
Route::patch('/articles', function() {});

//  Удаление ресурса.
Route::delete('/articles', function() {});
```