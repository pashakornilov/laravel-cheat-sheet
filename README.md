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

- [Eloquent](#eloquent)
    - [Получение записей](#получение-записей)
    - [Вставка / обновление](#вставкаобновление)
    - [Удаление](#удаление)
    - [Отношения](#отношения)
    - [Коллекции](#коллекции)
    - [Другие](#другие)

### Получение записей

#### all()  
```php
// Получить все записи модели Post
Post::all();
```

#### chunk()
```php  
// Получить записи модели Post порциями по 100 штук 
Post::chunk(100, function($posts) { /* ... */ });
```

#### find()
```php
// Найти запись модели Post с первичным ключом 1
Post::find(1);
```

#### first()
```php
// Получить первую запись модели Post
Post::first();
```

#### firstOrCreate()
```php
// Получить первую запись модели Post или создать новую
Post::firstOrCreate(['title' => 'Test']);
```

#### firstOrFail()
```php
// Получить первую запись модели Post или вызвать исключение
Post::firstOrFail();
```

#### firstOrNew()
```php
// Получить первую запись модели Post или новый экземпляр
Post::firstOrNew(['title' => 'Test']);
```

#### firstWhere() 
```php
// Получить первую запись модели Post где views > 100
Post::firstWhere('views', '>', 100);
```

#### get()
```php
// Получить записи модели Post по массиву ключей [1, 2, 3]
Post::get([1, 2, 3]);
```

#### inRandomOrder()
```php
// Получить записи модели Post в случайном порядке
Post::inRandomOrder()->get();
```

#### latest() 
```php
// Получить последнюю запись модели Post
Post::latest()->first(); 
```

#### oldest()
```php
// Получить самую старую запись модели Post  
Post::oldest()->first();
```

#### paginate()
```php
// Получить записи модели Post с постраничной разбивкой по 10 штук
Post::paginate(10);
```

#### sole()
```php
// Получить одну запись модели Post или вызвать исключение
Post::sole();
```

#### take()
```php 
// Получить 5 записей модели Post
Post::take(5)->get();
```

#### where()
```php
// Получить записи модели Post где active = 1 
Post::where('active', 1)->get();
```

#### whereBetween()
```php
// Получить записи модели Post где id между 1 и 10
Post::whereBetween('id', [1, 10])->get(); 
```

#### whereIn()
```php
// Получить записи модели Post где id в [1, 2, 3]
Post::whereIn('id', [1, 2, 3])->get();
```

#### whereNotBetween()
```php  
// Получить записи модели Post где id не между 5 и 15
Post::whereNotBetween('id', [5, 15])->get();
```

#### whereNotIn()
```php
// Получить записи модели Post где id не в [1, 2, 3] 
Post::whereNotIn('id', [1, 2, 3])->get();
```

#### whereNull()
```php
// Получить записи модели Post где deleted_at IS NULL
Post::whereNull('deleted_at')->get();
```

### Вставка/обновление

#### create()
```php 
// Создать и сохранить новую запись модели Post
Post::create(['title' => 'Test']);
```  

#### forceDelete()
```php
// Принудительно удалить запись модели Post с ID 1
Post::find(1)->forceDelete(); 
```

#### insert()
```php
// Вставить запись в таблицу posts
Post::insert(['title' => 'Test']);
```

#### make()
```php 
// Создать новый экземпляр модели Post
Post::make(['title' => 'Test']);
```

#### save()
```php
// Сохранить запись модели Post
$post->save();
```

#### update() 
```php
// Обновить запись модели Post с ID 1
Post::where('id', 1)->update(['title' => 'New title']); 
```

#### updateOrCreate()
```php
// Обновить или создать запись модели Post
Post::updateOrCreate(['id' => 1], ['title' => 'Test']);
```

### Удаление

#### delete() 
```php 
// Удалить запись модели Post с ID 1
Post::destroy(1);
```

#### destroy()
```php
// Удалить запись модели Post с ID 1 и связанные
Post::destroy(1);
```

#### forceDelete()
```php
// Принудительно удалить запись модели Post с ID 1
Post::withTrashed()->find(1)->forceDelete();
```

#### restore()
```php  
// Восстановить удаленную запись модели Post с ID 1
Post::withTrashed()->find(1)->restore();
```

#### trashed()
```php
// Получить только удаленные записи модели Post
Post::onlyTrashed()->get();
```

### Агрегация

#### avg()
```php
// Получить среднее значение столбца views модели Post 
Post::avg('views');
```

#### count() 
```php
// Получить количество записей модели Post
Post::count();
```

#### max()
```php
// Получить максимальное значение столбца views модели Post
Post::max('views');
```

#### min()
```php  
// Получить минимальное значение столбца views модели Post
Post::min('views');
``` 

#### sum()
```php
// Получить сумму значений столбца views модели Post
Post::sum('views');
```

### Отношения

#### attach()
```php  
// Присоединить модель Tag с ID [1, 2, 3] к модели Post
$post->tags()->attach([1, 2, 3]); 
```

#### belongsTo()
```php
// Модель Post принадлежит модели User
public function user() {
  return $this->belongsTo(User::class);
}
```

#### belongsToMany()
```php
// Связь многие-ко-многим между Post и Tag
public function tags() {
  return $this->belongsToMany(Tag::class); 
}
```

#### hasOne()
```php 
// Модель Post имеет одну связанную модель Phone
public function phone() {
  return $this->hasOne(Phone::class);
}
```

#### hasMany()
```php
// Модель Post имеет много связанных моделей Comment
public function comments() {
  return $this->hasMany(Comment::class);
}
```

#### morphMany()
```php
// Полиморфное отношение модели Post имеет много Comment
public function comments() {
  return $this->morphMany(Comment::class, 'commentable');  
}
```

#### morphOne()
```php 
// Полиморфное отношение модели Post имеет одну Image
public function image() {
  return $this->morphOne(Image::class, 'imageable');
}
```

#### morphTo()
```php
// Полиморфное отношение модели Comment к imageable
public function imageable() {
  return $this->morphTo();   
}
```

#### morphToMany() 
```php
// Полиморфное отношение многие-ко-многим между Post и Tag  
public function tags() {
  return $this->morphToMany(Tag::class, 'taggable');
}
```

#### sync()
```php
// Синхронизировать связи модели Post с моделью Tag
$post->tags()->sync([1, 2, 3]); 
```

### Коллекции

#### each()
```php
// Выполнить функцию для каждой записи коллекции
$posts->each(function ($post) {
  // действие
});
```

#### filter()
```php 
// Отфильтровать коллекцию по активным записям
$posts->filter(function ($post) {
  return $post->active;
});
```

#### map()
```php
// Получить названия всех записей  
$posts->map(function ($post) {
  return $post->title;
});
```

#### mapInto()
```php  
// Преобразовать коллекцию и добавить в модель Post
$posts->mapInto('\App\Post', function ($post) {
  // ...
});
```

#### mapSpread() 
```php
// Распаковать коллекцию с индексами
$posts->mapSpread(function ($post, $i) {
  // использовать индекс
});
```

#### reject()
```php
// Отфильтровать неактивные записи 
$posts->reject(function ($post) {
  return $post->active; 
});
```

#### sortBy()
```php  
// Сортировать по дате создания
$posts->sortBy('created_at');
```

#### sortByDesc()
```php
// Сортировать по дате создания по убыванию
$posts->sortByDesc('created_at');
```

#### unique() 
```php
// Убрать дубликаты записей
$posts->unique();
```

#### values()
```php
// Получить только значения коллекции  
$posts->values();
```

### Другое

#### decrement()
```php 
// Уменьшить значение views модели Post на 1
$post->decrement('views');
```

#### detach()
```php
// Удалить связь комментария с постом
$comment->detach();
```

#### increment()
```php
// Увеличить значение views модели Post на 1
$post->increment('views');
```

#### onlyTrashed()
```php  
// Получить только удаленные записи Post
Post::onlyTrashed()->get();
```

#### pluck()
```php
// Получить значения указанного столбца
$posts->pluck('title');
```

#### push()
```php
// Добавить элемент в массив 
$post->push('tags', 1);
```

#### saveMany() 
```php
// Сохранить коллекцию моделей
Post::saveMany([$post1, $post2]);
```
#### toBase()
```php
// Преобразовать к первоначальному состоянию
$post->toBase();
```

#### toSql()
```php
// Получить SQL запрос модели
Post::where('id', 1)->toSql();
```
#### with()
```php
// Добавить дополнительные условия
Post::with('user', 'comments')->get();
```
#### withAggregate()
```php
// Добавить агрегатную функцию
Post::withAggregate('comments', 'count')->get();
```
#### withCount()
```php
// Добавить подсчет связанных моделей
Post::withCount('comments')->get();
```