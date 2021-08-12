# Админ панель laravel

 ## 1
    * устанавливаем новый ларавель проект
    * устанавливаем node.js
    * устанавливаем 
    
## Добавление картинок в админ панели 
     ссылка на документацию  laravel-elfinder [Обычная ссылка с title](https://github.com/barryvdh/laravel-elfinder "laravel-elfinder")
    
    * устанавливаем  в терминале:  composer require barryvdh/laravel-elfinder 
    *  Добавьте ServiceProvider в массив поставщиков в app/config/app.php
    
         Barryvdh\Elfinder\ElfinderServiceProvider::class   
      
    *   Вам необходимо скопировать ресурсы в общую папку, используя следующую команду artisan:
    
        php artisan elfinder:publish
    
    * Конфигурация
      Для конфигурации по умолчанию требуется каталог под названием «файлы» в общей папке. Вы можете изменить это, опубликовав файл конфигурации.
      
      php artisan vendor:publish --provider='Barryvdh\Elfinder\ElfinderServiceProvider' --tag=config    