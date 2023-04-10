# anglar
ok
## About API pergamo v2.0

Esta API es la nueva versión de Enseñame v2.0, con las siguientes caracteristicas:

-   Framework Laravel [versión 7](https://laravel.com/docs/7.x#server-requirements).
-   Motor de base de datos MySql.
-   **Redis** [Redis en ubuntu](https://www.digitalocean.com/community/tutorials/como-instalar-y-proteger-redis-en-ubuntu-18-04-es)
-   **Supervisor** [Worker ejecución de colas](https://laravel.com/docs/7.x/queues#supervisor-configuration)

## Pasos y Comandos Iniciales

-   Asegurarse contar con los módulos de php a continuación: php-imap php-gmp php-curl php-bz2
-   Crear archivo .env en base al .env.example, escribir datos de accesos BD, redis y servidor email.
-   composer install
-   php artisan key:generate
-   php artisan jwt:secret
-   php artisan make:seeder UserSeeder
-   npm install && npm run dev
-   php artisan migrate:fresh --seed
-   sudo chmod -R 777 storage/
-   php artisan storage:link
-   php artisan serve --host="**mi-ip**" (Solo si no se tiene ejecutando en un host virtual)
-   composer dump-autoload  (Para actualizar la información del cargador automatico de clases)
-   Configurar supervisor para la ejecución automática de [queue](https://laravel.com/docs/7.x/queues#supervisor-configuration), para configurar la queue para logs:
    -   Cola log: crear el archivo con sudo **/etc/supervisor/conf.d/ensename-v2-laravel-worker.conf**, y agregar:
    ```
        [program:ensename-v2-laravel-worker]
        process_name=%(program_name)s_%(process_num)02d
        command=php /var/www/html/api-ensename-v2/artisan queue:work redis
        autostart=true
        autorestart=true
        user=root
        numprocs=8
        redirect_stderr=true
        stdout_logfile=/var/www/html/api-ensename-v2/storage/logs/worker.log
        stopwaitsecs=3600
    ```
    -   sudo supervisorctl reread
    -   sudo supervisorctl update
    -   En la dirección desplegada, se puede visualizar los jobs cuando se crean y sus cambios de estados en: http://host/telescope/jobs
-   Para recibir la sincronización del conector, es **OBLIGATORIO** que las instituciones tengan asociadas las MAC de los SEO, en la tabla **institution_mac**.

## Otros comandos

-   Crear models a partir de la BD [(Reliese)](https://github.com/reliese/laravel)

    - php artisan code:models --schema=**name_db**

-   Documentación autenticación [JWT](https://jwt-auth.readthedocs.io/en/develop/laravel-installation/#generate-secret-key)

-   Documentación comprimido [Madzipper](https://github.com/madnest/madzipper)

-   php artisan make:controller NoteController

-   php artisan config:clear

-   php artisan cache:clear

---

## License

Copyright Health and life ips 2021

/////////////////////////////////////////////////////////////////////angular ///////////////////////////////////////////////////////////////////////////////////


# Pergamo
Herramienta gestión de health and life ips.

---

## Descargar e Instalar CURL
-   sudo apt install curl
-   sudo curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
## Validar version CURL
-   nvm --version
## Versiones disponibles NodeJS
-   nvm ls-remote
## Instalar version especifica NodeJS (Automaticamente agrega el NPM)
-   nvm install 10.16.3
## Validar version NodeJS y NPM
-   node -v 
-   npm -v
## Cambiar version de NodeJS y NPM (Opcional)
-   nvm use 10.16.3

## Ejcutar bash nvm (Opcional)
-   source ~/.nvm/nvm.sh

## Dar permisos a la carpeta
-   sudo chown -R www-data:www-data front-ensename
-   sudo chmod -R 777 front-ensename


## Instalar dependencias (Raiz de front-ensename)
-   npm install

## Instalar AngularCLI
-   npm install -g @angular/cli@9.1.4

## Ejecutar APP (Solo si no se tiene ejecutando en un host virtual)
-   ng serve --host=0.0.0.0 --port=8002
-   node --max_old_space_size=8048 ./node_modules/@angular/cli/bin/ng serve

## Publicar APP (Destino por defecto "dist/")
-   ng build --prod

## Documentación
https://phoenixnap.com/kb/install-latest-node-js-and-nmp-on-ubuntu#:~:text=Install%20a%20Specific%20Version,-Nvm%20is%20a&text=To%20install%20a%20particular%20version,the%20number%20of%20the%20version.&text=This%20will%20list%20all%20installed,the%20default%20and%20stable%20versions.

---
## License

Copyright Health and life ips 2021
