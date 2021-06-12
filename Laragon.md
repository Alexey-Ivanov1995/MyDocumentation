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