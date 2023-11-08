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

## Eloquent

Вот таблица методов Eloquent с примерами использования:

| Группа | Метод | Описание | Пример |
|-|-|-|-|
| Получение записей | all() | Получить все записи модели | `Post::all();` |
|  | chunk() | Получить записи модели порциями | `Post::chunk(100, function($posts) { /* ... */ });` |
|  | find() | Найти запись по первичному ключу | `Post::find(1);` |
|  | first() | Получить первую запись | `Post::first();` | 
|  | firstOrCreate() | Получить первую запись или создать новую | `Post::firstOrCreate(['title' => 'Test']);` |
|  | firstOrFail() | Получить первую запись или вызвать исключение | `Post::firstOrFail();` |
|  | firstOrNew() | Получить первую запись или новый экземпляр | `Post::firstOrNew(['title' => 'Test']);` |
|  | firstWhere() | Получить первую запись по условию | `Post::firstWhere('views', '>', 100);` |
|  | get() | Получить записи по первичному ключу или массиву ключей | `Post::get([1, 2, 3]);` |
|  | inRandomOrder() | Получить записи в случайном порядке | `Post::inRandomOrder()->get();` | 
|  | latest() | Получить последнюю запись | `Post::latest()->first();` |
|  | oldest() | Получить самую старую запись | `Post::oldest()->first();` |
|  | paginate() | Получить записи с постраничной разбивкой | `Post::paginate(10);` |
|  | sole() | Получить одну запись или вызвать исключение | `Post::sole();` |
|  | take() | Получить указанное количество записей | `Post::take(5)->get();` | 
|  | where() | Фильтрация записей | `Post::where('active', 1)->get();` |
|  | whereBetween() | Фильтрация между значениями | `Post::whereBetween('id', [1, 10])->get();` |
|  | whereIn() | Фильтрация по массиву значений | `Post::whereIn('id', [1, 2, 3])->get();` |
|  | whereNotBetween() | Исключить значения между | `Post::whereNotBetween('id', [5, 15])->get();` |
|  | whereNotIn() | Исключить значения из массива | `Post::whereNotIn('id', [1, 2, 3])->get();` |  
|  | whereNull() | Фильтрация по NULL значению | `Post::whereNull('deleted_at')->get();` |
| Вставка/обновление | create() | Создать и сохранить новую запись | `Post::create(['title' => 'Test']);` |
|  | forceDelete() | Принудительно удалить запись | `Post::find(1)->forceDelete();` |  
|  | insert() | Вставить запись в таблицу | `Post::insert(['title' => 'Test']);` |
|  | make() | Создать новый экземпляр модели | `Post::make(['title' => 'Test']);` |
|  | save() | Сохранить запись | `$post->save();` |  
|  | update() | Обновить существующую запись | `Post::where('id', 1)->update(['title' => 'New title']);` |
|  | updateOrCreate() | Обновить или создать запись | `Post::updateOrCreate(['id' => 1], ['title' => 'Test']);` |
| Удаление | delete() | Удалить запись | `Post::destroy(1);` |
|  | destroy() | Удалить запись и связанные | `Post::destroy(1);` |
|  | forceDelete() | Принудительно удалить запись | `Post::withTrashed()->find(1)->forceDelete();` |
|  | restore() | Восстановить удаленную запись | `Post::withTrashed()->find(1)->restore();` |
|  | trashed() | Получить только удаленные записи | `Post::onlyTrashed()->get();` |
| Агрегация | avg() | Получить среднее значение столбца | `Post::avg('views');` |
|  | count() | Получить количество записей | `Post::count();` |
|  | max() | Получить максимальное значение столбца | `Post::max('views');` |  
|  | min() | Получить минимальное значение столбца | `Post::min('views');` |
|  | sum() | Получить сумму значений столбца | `Post::sum('views');` |
| Отношения | attach() | Присоединить связанную модель | `$post->tags()->attach([1, 2, 3]);` |
|  | belongsTo() | Определить отношение "принадлежит" | `public function user() { return $this->belongsTo(User::class); }` |  
|  | belongsToMany() | Определить многие-ко-многим | `public function tags() { return $this->belongsToMany(Tag::class); }` |
|  | hasOne() | Определить отношение "имеет один" | `public function phone() { return $this->hasOne(Phone::class); }` |
|  | hasMany() | Определить отношение "имеет много" | `public function comments() { return $this->hasMany(Comment::class); }` |
|  | morphMany() | Полиморфное отношение "имеет много" | `public function comments() { return $this->morphMany(Comment::class, 'commentable'); }` |  
|  | morphOne() | Полиморфное отношение "имеет один" | `public function image() { return $this->morphOne(Image::class, 'imageable'); }` |
|  | morphTo() | Определить полиморфное отношение | `public function imageable() { return $this->morphTo(); }` |
|  | morphToMany() | Полиморфное многие-ко-многим | `public function tags() { return $this->morphToMany(Tag::class, 'taggable'); }` |
|  | sync() | Синхронизировать связи | `$post->tags()->sync([1, 2, 3]);` | 
| Коллекции | each() | Выполнить функцию для каждого элемента | `$posts->each(function ($post) { // действие });` |  
|  | filter() | Фильтрация коллекции | `$posts->filter(function ($post) { return $post->active; });` |
|  | map() | Применить функцию к каждому элементу | `$posts->map(function ($post) { return $post->title; });` |
|  | mapInto() | Применить функцию и добавить в коллекцию | `$posts->mapInto('\App\Post', function ($post) { // ... });` |
|  | mapSpread() | Распаковать коллекцию в массив | `$posts->mapSpread(function ($post, $i) { // использовать индекс });` |
|  | reject() | Фильтрация по условию | `$posts->reject(function ($post) { return $post->active; });` | 
|  | sortBy() | Сортировка коллекции | `$posts->sortBy('created_at');` |
|  | sortByDesc() | Сортировка коллекции по убыванию | `$posts->sortByDesc('created_at');` |
|  | unique() | Убрать дубликаты из коллекции | `$posts->unique();` |
|  | values() | Получить все значения коллекции | `$posts->values();` |
| Другое | decrement() | Уменьшить числовое значение | `$post->decrement('views');` |
|  | detach() | Удалить связь с родительской моделью | `$comment->detach();` |
|  | increment() | Увеличить числовое значение | `$post->increment('views');` |
|  | onlyTrashed() | Получить только удаленные модели | `Post::onlyTrashed()->get();` |  
|  | pluck() | Получить значения указанного столбца | `$posts->pluck('title');` |
|  | push() | Добавить элемент в массив | `$post->push('tags', 1);` | 
|  | saveMany() | Сохранить коллекцию моделей | `Post::saveMany([$post1, $post2]);` |
|  | toBase() | Преобразовать к первоначальному состоянию | `$post->toBase();` | 
|  | toSql() | Получить SQL запрос модели | `Post::where('id', 1)->toSql();` |  
|  | with() | Добавить дополнительные условия | `Post::with('user', 'comments')->get();` |
|  | withAggregate() | Добавить агрегатную функцию | `Post::withAggregate('comments', 'count')->get();` | 
|  | withCount() | Добавить подсчет связанных моделей | `Post::withCount('comments')->get();` |