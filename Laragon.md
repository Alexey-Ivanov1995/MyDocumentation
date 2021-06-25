$APP_ENV = local // если редактировать локально   prodaction // если отпускаем на сервере
$DATABASE_NAME = database_name
$DB_USERNAME= (root // если ларагон) если нет //  то зависит от сервера
$DB_PASSWORD =  // усли для себя если сервер то пороль есть

# Если есть ошибака при запуске через ларогон
    * заходим в папку с проектом  
    * делаем: composer instal 
    * создаем копи: .env.example в .env 
    * гинерируем ключ php artisan key:generate 
    * ура работает!  
   
   # Создание базы данных mysql
      * mysql -uroot -e "create database $DATABASE_NAME;" |- создаем базу данных
      * php artisan migrate --seed |- кидаем ее в mysql
      * php artisan migrate:fresh --seed |- удаляет все с базы и загружает с нуля
      * делаем в .env  
           1. APP_ENV=local     | меняем с prodaksena на  local 
           1. DB_DATABASE= $DATABASE_NAME  | название базы данных 
           2. DB_USERNAME=root  | название 
           3. DB_PASSWORD=      | пароль делаем как хотим 
           
   # Генерация пороля для базы данных 
      * php artisan tinker        


# Создание компонентов :
    * php artisan make - паказывает возможности make 
    * php artisan make:componet name component(с большой буквы никаких пробуло и камелкейсои)
     создает во views папку components и  в ней создает вю компонент
     и в папке app/View/components содает файл контроллер компонента


  
# База данных :  

### очиска:
       *  Если мы работаем локаально с демо можно делать , чтобы не делать много rollback
       *  php artisan migrate:fresh - очищает и записывает заного все файлы в базе данных 
       *  php artisan migrate:refresh - очищает и записывает заного все файлы в базе данных
        refresh и fresh - одно и тоже 
 
  

### создание базы данных:
     
          * создаем Laravel проект 
          * создаем базу данных через Laragon database 
          * после указывае в .env файле название базы данных пороль и user name
          * после делаем в терменале php artisan migrate
       
       
       
### создание файла в базе данных: 
          * создаем новый файл бызы php artisan make:migration "name" --create name
          * cоздаем можедь php artisan make:model  Name(с большой буквы) -r (resurse)
          * создаем контроллер php artisan make:controller NmaeController -r
             
###  создание колонок в файле при --create  (типы данных = [какой тип данных будем ложить](https://laravel.su/docs/8.x/migrations#available-column-types))

      
     public function up()
     {
       Schema::create('name file', function (Blueprint $table) {
             $table->id(); - появляется автоматом обязательное поле
             --- можем создавать сколько угодно солонок 
             $table->тип данных ссылка выше пример string( column 'name' )->nullable(); (->nullable() не оязательное поле)
             $table->integer(column'age');
             и тд  
             ----      
             $table->timestamps(); - показывает дату создания и дату изменения
        }); 
      }
###  создание содержимого колонок :
      $data = 
      [
         [
           'азвание колонки которое мы создали выше ' => 'то что мы будем ложить в колонку',
           'name' => "alex",
         ]
      ]   
### отправляем содержимое на базу данных 
          foreach ($data as $single) {
                    \App\Models\NameModel::create($single);
                }
                
### итог как выглядет наша база :
     
     public function up(){
         
           Schema::create('name file', function (Blueprint $table) {
                 $table->id(); - появляется автоматом обязательное поле
                 --- можем создавать сколько угодно солонок 
                 $table->тип данных ссылка выше пример string( column 'name' )->nullable(); (->nullable() не оязательное поле)
                 $table->integer(column'age');
                 и тд  
                 ----      
                 $table->timestamps(); - показывает дату создания и дату изменения
            }); 
            
            
            $data = 
               [
                  [
                    'азвание колонки которое мы создали выше ' => 'то что мы будем ложить в колонку',
                    'name' => "alex",
                  ],
               ]; 
               
               
               foreach ($data as $single) {
                   \App\Models\NameModel::create($single);
               }
               
          }
###  в модели указываем    
    
     class NmaeModal extends Model
      {
          protected $table = 'name file';
      
          protected $guarded = [];
      }  
      
                          
#   Читерский способ создания файла в базе 
        * php artisan make: Name -mcr   
        создает файл с названием name  создает контроллер и модель остается создать содержимое базы настроить зависимости 
        и сделать php artisan migrate

# Получение из базы данных в контроллере :
            public function index()
            {
                $ages = NameModal::get();
        
                return view(view:'name page', compact(varname:'ages'));
            }
            
            
# Создание проекта с рандомной базой данных 

##### 1. создакм проект (можно через консоль или ларагон)
##### 2. создаем базы данных (елси нужна только одна, при создании проекта создается автоматически, можно создать свою)
##### 3. создаем контроллер , модель , миграции , фактори
      -php artisan make:model Name -mfc
##### 4. заносим создаем таблицы в файле миграции пример:
        public function up()
        {
            Schema::create('blogs', function (Blueprint $table) {
                $table->id();
                $table->string('title');
                $table->text('body')->nullable();
                $table->string('slug')->nullable();
                $table->string('keywords')->nullable();
                $table->timestamps();
            });
        }  
        отпрваить в базу данных в консоли php artisan migrate
         (если перезаписать migrate:fresh)
#### 5. создаем в фактори рандомное содержимое которое будет вписано в столбцы файла миграции, тобишь базы даннх пример:
            public function definition()
            {
                return [
                    'title' => $this->faker->name(),
                    'body' => $this->faker->text(),
                    'slug' => str_slug($this->faker->name()),
                    'keywords' => $this->faker->name(),
                ];
            }
        }
        (значения генерируются рандомно просто указываем какой тип в них будет лежать 
        тип данных должен быть таким же как и в файле миграции для каждого поля)
#### 6. В seeders создаем количество строк которые будут заполнятья рандомными значениям из фактори (указываем количесвто)
       public function run()
          {
               \App\Models\NameModel::factory(10)->create();
          }        
          (создает 10 строк)
#### после утсанавливаем composer helper
      composer require laravel/helpers (чтобы на slug заработал)    
#### после добавляем все наши раидомные данные в нашу базу 
     php artisan migrate:fresh --seed       
          
#### с базой данных завершили настойку          
          
#### 7.  Создаем во views странички на которых будет отоброжаться контент с базы данных      
#### 8. Создаем в контроллере фонкции 
       class NameController extends Controller
       {
           public function index()
           {
               $blogs(просто название переменной) = NameModal::get();
       
               return view('/название странички на которую удут выводится данные', compact('blogs'));
           }
       
           public function show($slug)
           {
               $blog(просто название переменной)  = NameModal::where('slug', $slug)->firstOrFail();   (slug берется из таблицы)
       
               return view('/название странички которая будет выводить данные одной стоки', compact('blog'));
           }
       }    
       
          
#### 9.  В Web.php настраиваем отображение страниц 

         Route::get('/название страницы', [BlogController::class, 'index'])->name('data');         
         Route::get('/название страницы/{название странички которая будет выводить данные одной стоки :slug}',[BlogController::class,'show'])->name('data-show');  
         в name указываем любое имя по нему будем обращаться к функции
#### 10. В HTML размете указываем куда вписывать значения с  базы пример  основной страницы 
       </head>
       <body>
       
       <div class="container">
           @foreach($blogs as $blog) ($blogs подтягиваетс из контроллера) 
               <div class="card">
                   <div class="head">
                       <a href="{{ route('data-show(имя функции которое мы далавли в web', ['blog' => $blog->slug ]) }}">{{ $blog->title }}</a>
                   </div>
                   <div class="body">
                      <p> {{ $blog->body }}</p>
                       <p>{{ $blog->keywords }}</p>
                   </div>
                   <div class="footer">
                       {{ $blog->created_at }}
                   </div>
               </div>
           @endforeach
       </div>
       
       </body>
       </html>

#### 11. саздаем разметку страницы  которая будет выводить данные одной стоки   пример
        <body>
        <div>
            <h3>Blog</h3>
            <ul>
            ($blog подтягтвается из контроллера)
                <p>{{ $blog->title }}</p>
                <p>{{ $blog->body }}</p>
                <p>{{ $blog->keywords }}</p>
                <p>{{ $blog->created_at }}</p>
                <p>{{ $blog->slug }}</p>
            </ul>
        </div>
        </body>
        </html>      
#### 12.  заходим в браузер на нашу страничку все должно работать)))Ураа!  