# laravel-cheat-sheet

- [Eloquent](#eloquent)
    - [Получение записей](#получение-записей)
    - [Вставка / обновление](#вставка--обновление)
    - [Удаление](#удаление)
    - [Отношения](#отношения)
    - [Коллекции](#коллекции)
    - [Другие](#другие)

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

### Route Parameter

```php
// Передача числового ID статьи в переменную $id.
Route::get('/articles/{article}', function ($id) {return 'article '. $id;});

// Передача числового ID статьи в переменную $articleId, ID комментария в переменную $commentId
Route::get('/articles/{article}/comments/{comment}', function ($articleId, $commentId) {});
```

### Optional parameters

```php
// по умолчанию для $name используется значение null
Route::get('/articles/{name?}', function ($name = null) {return $name;});

// по умолчанию 'Alex' в $name
Route::get('/articles/{name?}', function ($name = 'Alex') {return $name;});
```

	Для использования опционального параметра необходимо указать значение параметров по умолчанию
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

// Ответ на любой тип запроса
Route::any('/articles', function() {});
```

### RESTful Controllers

```php
// Определение ресурсных маршрутов
Route::resource('/articles','ArticleController');

// Частичное определение ресурсных маршрутов
	// only - позволяет определить белый список экшенов, которые доступны по данному роуту
Route::resource('/articles', 'ArticleController',['only' => ['index', 'show']]);
	// except - определяет черный список экшенов, которые недоступны по данному роуту
Route::resource('/articles', 'ArticleController',['except' => ['edit', 'update', 'destroy']]);
```

