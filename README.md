# laravel-cheat-sheet

## Route

Пример: http://example.com/articles

### Define route

```php
// Регистрация GET-маршрута с использованием замыкания
Route::get('/articles', function(){});

// Регистрация GET-маршрута с использованием контроллера
Route::get('/articles', 'ArticleController@index');
Route::get('/articles', [ArticleController::class, 'index']);
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

### RESTful Controllers

```php
// Определение ресурсных маршрутов
Route::resource('Sheets','SheetController');

// Частичное определение ресурсных маршрутов
Route::resource('/articles', 'ArticleController',['only' => ['index', 'show']]);
Route::resource('/articles', 'ArticleController',['except' => ['edit', 'update', 'destroy']]);
```