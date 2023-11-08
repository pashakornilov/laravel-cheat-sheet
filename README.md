# laravel-cheat-sheet

- [Eloquent](#eloquent)
    - [Получение записей](#получение-записей)
    - [Вставка / обновление](#вставкаобновление)
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

## Eloquent

### Получение записей

```php
// Получить все записи модели Post
Post::all();

// Получить записи модели Post порциями по 100 штук 
Post::chunk(100, function($posts) { /* ... */ });

// Найти запись модели Post с первичным ключом 1
Post::find(1);

// Получить первую запись модели Post
Post::first();

// Получить первую запись модели Post или создать новую
Post::firstOrCreate(['title' => 'Test']);

// Получить первую запись модели Post или вызвать исключение
Post::firstOrFail();

// Получить первую запись модели Post или новый экземпляр
Post::firstOrNew(['title' => 'Test']);

// Получить первую запись модели Post где views > 100
Post::firstWhere('views', '>', 100);

// Получить записи модели Post по массиву ключей [1, 2, 3]
Post::get([1, 2, 3]);

// Получить записи модели Post в случайном порядке
Post::inRandomOrder()->get();

// Получить последнюю запись модели Post
Post::latest()->first(); 

// Получить самую старую запись модели Post  
Post::oldest()->first();

// Получить записи модели Post с постраничной разбивкой по 10 штук
Post::paginate(10);

// Получить одну запись модели Post или вызвать исключение
Post::sole();

// Получить 5 записей модели Post
Post::take(5)->get();

// Получить записи модели Post где active = 1 
Post::where('active', 1)->get();

// Получить записи модели Post где id между 1 и 10
Post::whereBetween('id', [1, 10])->get(); 

// Получить записи модели Post где id в [1, 2, 3]
Post::whereIn('id', [1, 2, 3])->get();

// Получить записи модели Post где id не между 5 и 15
Post::whereNotBetween('id', [5, 15])->get();

// Получить записи модели Post где id не в [1, 2, 3] 
Post::whereNotIn('id', [1, 2, 3])->get();

// Получить записи модели Post где deleted_at IS NULL
Post::whereNull('deleted_at')->get();
```

### Вставка / обновление

```php 
// Создать и сохранить новую запись модели Post
Post::create(['title' => 'Test']);

// Принудительно удалить запись модели Post с ID 1
Post::find(1)->forceDelete(); 

// Вставить запись в таблицу posts
Post::insert(['title' => 'Test']);

// Создать новый экземпляр модели Post
Post::make(['title' => 'Test']);

// Сохранить запись модели Post
$post->save();

// Обновить запись модели Post с ID 1
Post::where('id', 1)->update(['title' => 'New title']); 

// Обновить или создать запись модели Post
Post::updateOrCreate(['id' => 1], ['title' => 'Test']);
```

### Удаление


```php 
// Удалить запись модели Post с ID 1
Post::destroy(1);

// Удалить запись модели Post с ID 1 и связанные
Post::destroy(1);

// Принудительно удалить запись модели Post с ID 1
Post::withTrashed()->find(1)->forceDelete();

// Восстановить удаленную запись модели Post с ID 1
Post::withTrashed()->find(1)->restore();

// Получить только удаленные записи модели Post
Post::onlyTrashed()->get();
```

### Агрегация

```php
// Получить среднее значение столбца views модели Post 
Post::avg('views');

// Получить количество записей модели Post
Post::count();

// Получить максимальное значение столбца views модели Post
Post::max('views');

// Получить минимальное значение столбца views модели Post
Post::min('views');

// Получить сумму значений столбца views модели Post
Post::sum('views');
```

### Отношения

```php  
// Присоединить модель Tag с ID [1, 2, 3] к модели Post
$post->tags()->attach([1, 2, 3]); 

// Модель Post принадлежит модели User
public function user() {
  return $this->belongsTo(User::class);
}

// Связь многие-ко-многим между Post и Tag
public function tags() {
  return $this->belongsToMany(Tag::class); 
}

// Модель Post имеет одну связанную модель Phone
public function phone() {
  return $this->hasOne(Phone::class);
}

// Модель Post имеет много связанных моделей Comment
public function comments() {
  return $this->hasMany(Comment::class);
}

// Полиморфное отношение модели Post имеет много Comment
public function comments() {
  return $this->morphMany(Comment::class, 'commentable');  
}

// Полиморфное отношение модели Post имеет одну Image
public function image() {
  return $this->morphOne(Image::class, 'imageable');
}

// Полиморфное отношение модели Comment к imageable
public function imageable() {
  return $this->morphTo();   
}

// Полиморфное отношение многие-ко-многим между Post и Tag  
public function tags() {
  return $this->morphToMany(Tag::class, 'taggable');
}

// Синхронизировать связи модели Post с моделью Tag
$post->tags()->sync([1, 2, 3]); 
```

### Коллекции

```php
// Выполнить функцию для каждой записи коллекции
$posts->each(function ($post) {
  
});

// Отфильтровать коллекцию по активным записям
$posts->filter(function ($post) {
  return $post->active;
});

// Получить названия всех записей  
$posts->map(function ($post) {
  return $post->title;
});

// Преобразовать коллекцию и добавить в модель Post
$posts->mapInto('\App\Post', function ($post) {
  // ...
});

// Распаковать коллекцию с индексами
$posts->mapSpread(function ($post, $i) {
  // использовать индекс
});

// Отфильтровать неактивные записи 
$posts->reject(function ($post) {
  return $post->active; 
});

// Сортировать по дате создания
$posts->sortBy('created_at');

// Сортировать по дате создания по убыванию
$posts->sortByDesc('created_at');

// Убрать дубликаты записей
$posts->unique();

// Получить только значения коллекции  
$posts->values();
```

### Другое

```php 
// Уменьшить значение views модели Post на 1
$post->decrement('views');

// Удалить связь комментария с постом
$comment->detach();

// Увеличить значение views модели Post на 1
$post->increment('views');

// Получить только удаленные записи Post
Post::onlyTrashed()->get();

// Получить значения указанного столбца
$posts->pluck('title');

// Добавить элемент в массив 
$post->push('tags', 1);

// Сохранить коллекцию моделей
Post::saveMany([$post1, $post2]);

// Преобразовать к первоначальному состоянию
$post->toBase();

// Получить SQL запрос модели
Post::where('id', 1)->toSql();

// Добавить дополнительные условия
Post::with('user', 'comments')->get();

// Добавить агрегатную функцию
Post::withAggregate('comments', 'count')->get();

// Добавить подсчет связанных моделей
Post::withCount('comments')->get();
```