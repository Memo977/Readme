# 30 Days to Learn Laravel

# Índice General

## Unidad I - Baby Steps
- [Episodio 02 - Your First Route and View](#episodio-02---your-first-route-and-view)
- [Episodio 03 - Create a Layout File Using Laravel Components](#episodio-03---create-a-layout-file-using-laravel-components)
- [Episodio 04 - Make a Pretty Layout Using Tailwind CSS](#episodio-04---make-a-pretty-layout-using-tailwind-css)
- [Episodio 05 - Style the Currently Active Navigation Link](#episodio-05---style-the-currently-active-navigation-link)
- [Episodio 06 - View Data and Route Wildcards](#episodio-06---view-data-and-route-wildcards)
- [Episodio 07 - Autoloading, Namespaces, and Models](#episodio-07---autoloading-namespaces-and-models)

## Unidad II - Eloquent
- [Episodio 08 - Introduction to Migrations](#episodio-08---introduction-to-migrations)
- [Episodio 09 - Meet Eloquent](#episodio-09---meet-eloquent)
- [Episodio 10 - Model Factories](#episodio-10---model-factories)
- [Episodio 11 - Eloquent Relationships](#episodio-11---eloquent-relationships)
- [Episodio 12 - Pivot Tables and Many-to-Many Relationships](#episodio-12---pivot-tables-and-many-to-many-relationships)
- [Episodio 13 - Eager Loading and the N+1 Problem](#episodio-13---eager-loading-and-the-n1-problem)
- [Episodio 14 - All You Need to Know About Pagination](#episodio-14---all-you-need-to-know-about-pagination)
- [Episodio 15 - Understanding Database Seeders](#episodio-15---understanding-database-seeders)

---
# Unidad I - Baby Steps

## Episodio 02 - Your First Route and View

Para comenzar a trabajar con el proyecto, abrimos el editor desde la terminal en la ruta del proyecto:

```bash
code .
```

**Ruta del proyecto:** `/ISW811/M/VMs/webserver/sites/30days.isw811.xyz`

### Modificando la vista principal

Navegamos a la carpeta `resources/views` y editamos el archivo `welcome.blade.php`. Dentro del elemento `<body>`, agregamos un mensaje de saludo:

```html
<body class="font-sans antialiased dark:bg-black dark:text-white/50">
    <h1>Hello, World!</h1>
</body>
```

### Creando rutas en Laravel

Las rutas en Laravel se definen en el archivo `routes/web.php`. Existen diferentes formas de crear rutas:

#### 1. Ruta que retorna una respuesta simple

```php
Route::get('/about', function (){
    return 'About Page';
});
```

#### 2. Ruta que retorna una respuesta JSON

```php
Route::get('/json', function (){
    return ['message' => 'Hello JSON'];
});
```

#### 3. Ruta que retorna una vista (método recomendado)

```php
Route::get('/about', function () {
    return view('about');
});
```

### Creando vistas personalizadas

Las vistas en Laravel se almacenan en la carpeta `resources/views`. Para crear una nueva vista, creamos el archivo `about.blade.php` con el siguiente contenido:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>About Page</title>
</head>
<body>
    <h1>Hello, from the About Page...</h1>
</body>
</html>
```

### Puntos clave del episodio

- **Ubicación de vistas:** `resources/views/`
- **Ubicación de rutas:** `routes/web.php`
- **Función `view()`:** Utilizada para retornar vistas desde las rutas
- **Extensión de archivos:** Las vistas pueden usar `.blade.php` para aprovechar el motor de plantillas Blade de Laravel

## Episodio 03 - Create a Layout File Using Laravel Components

### Creando nuevas rutas

Se crea una nueva ruta para Contacto:

```php
Route::get('/contact', function () {
    return view('contact');
});
```

Actualizamos el nombre de welcome a home:

```php
Route::get('/', function () {
    return view('home');
});
```

### Actualizando las vistas

Por ende también actualizamos la vista, es decir `welcome.blade.php` lo renombramos a `home.blade.php` y actualizamos su contenido:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Home Page</title>
</head>
<body>
    <h1>Hello, from the Home Page... </h1>
</body>
</html>
```

También creamos el archivo `contact.blade.php`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Contact Page</title>
</head>
<body>
    <h1>Hello, from the Contact Page... </h1>
</body>
</html>
```

### Agregando navegación

Tenemos Home, About y Contact. Vamos a agregar nuestra primera barra de navegación simple en cada vista:

```html
<nav>
    <a href="/">Home</a>
    <a href="/about">About</a>
    <a href="/contact">Contact</a>
</nav>
```

### Creando componentes de layout

Creamos una carpeta dentro de `views` llamada `components` y dentro creamos `layout.blade.php`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Home Page</title>
</head>
<body>
    <nav>
        <a href="/">Home</a>
        <a href="/about">About</a>
        <a href="/contact">Contact</a>
    </nav>
    {{ $slot }}
</body>
</html>
```

### Usando el componente layout

Ahora nuestros archivos tendrán lo siguiente:

**home.blade.php:**
```html
<x-layout>
    <h1>Hello from the Home Page.</h1>
</x-layout>
```

**about.blade.php:**
```html
<x-layout>
    <h1>Hello from the About Page.</h1>
</x-layout>
```

**contact.blade.php:**
```html
<x-layout>
    <h1>Hello from the Contact Page.</h1>
</x-layout>
```
## Episodio 04 - Make a Pretty Layout Using Tailwind CSS

### Agregando Tailwind CSS al layout

Ahora en `layout.blade.php` agregamos lo siguiente debajo de `<title>Home Page</title>`:

```html
<title>My Website</title>
<script src="https://cdn.tailwindcss.com"></script>
```

### Implementando el diseño de TailwindUI

Copiamos el código gratuito de tailwindui.com y lo agregamos a nuestro layout:

```html
<!DOCTYPE html>
<html lang="en" class="h-full bg-gray-100">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Website</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="h-full">
    <div class="min-h-full">
        <nav class="bg-gray-800">
            <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
                <div class="flex h-16 items-center justify-between">
                    <div class="flex items-center">
                        <div class="flex-shrink-0">
                            <img class="h-8 w-8" src="https://laracasts.com/images/logo/logo-triangle.svg" alt="Your Company">
                        </div>
                        <div class="hidden md:block">
                            <div class="ml-10 flex items-baseline space-x-4">
                                <!-- Current: "bg-gray-900 text-white", Default: "text-gray-300 hover:bg-gray-700 hover:text-white" -->
                                <a href="/" class="bg-gray-900 text-white rounded-md px-3 py-2 text-sm font-medium" aria-current="page">Home</a>
                                <a href="/about" class="text-gray-300 hover:bg-gray-700 hover:text-white rounded-md px-3 py-2 text-sm font-medium">About</a>
                                <a href="/contact" class="text-gray-300 hover:bg-gray-700 hover:text-white rounded-md px-3 py-2 text-sm font-medium">Contact</a>
                            </div>
                        </div>
                    </div>
                    <div class="hidden md:block">
                        <div class="ml-4 flex items-center md:ml-6">
                            <button type="button" class="relative rounded-full bg-gray-800 p-1 text-gray-400 hover:text-white focus:outline-none focus:ring-2 focus:ring-white focus:ring-offset-2 focus:ring-offset-gray-800">
                                <span class="absolute -inset-1.5"></span>
                                <span class="sr-only">View notifications</span>
                                <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" aria-hidden="true">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M14.857 17.082a23.848 23.848 0 005.454-1.31A8.967 8.967 0 0118 9.75v-.7V9A6 6 0 006 9v.75a8.967 8.967 0 01-2.312 6.022c1.733.64 3.56 1.085 5.455 1.31m5.714 0a24.255 24.255 0 01-5.714 0m5.714 0a3 3 0 11-5.714 0" />
                                </svg>
                            </button>

                            <!-- Profile dropdown -->
                            <div class="relative ml-3">
                                <div>
                                    <button type="button" class="relative flex max-w-xs items-center rounded-full bg-gray-800 text-sm focus:outline-none focus:ring-2 focus:ring-white focus:ring-offset-2 focus:ring-offset-gray-800" id="user-menu-button" aria-expanded="false" aria-haspopup="true">
                                        <span class="absolute -inset-1.5"></span>
                                        <span class="sr-only">Open user menu</span>
                                        <img class="h-8 w-8 rounded-full" src="https://laracasts.com/images/lary-ai-face.svg" alt="">
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="-mr-2 flex md:hidden">
                        <!-- Mobile menu button -->
                        <button type="button" class="relative inline-flex items-center justify-center rounded-md bg-gray-800 p-2 text-gray-400 hover:bg-gray-700 hover:text-white focus:outline-none focus:ring-2 focus:ring-white focus:ring-offset-2 focus:ring-offset-gray-800" aria-controls="mobile-menu" aria-expanded="false">
                            <span class="absolute -inset-0.5"></span>
                            <span class="sr-only">Open main menu</span>
                            <!-- Menu open: "hidden", Menu closed: "block" -->
                            <svg class="block h-6 w-6" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" aria-hidden="true">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5" />
                            </svg>
                            <!-- Menu open: "block", Menu closed: "hidden" -->
                            <svg class="hidden h-6 w-6" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" aria-hidden="true">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                            </svg>
                        </button>
                    </div>
                </div>
            </div>

            <!-- Mobile menu, show/hide based on menu state. -->
            <div class="md:hidden" id="mobile-menu">
                <div class="space-y-1 px-2 pb-3 pt-2 sm:px-3">
                    <!-- Current: "bg-gray-900 text-white", Default: "text-gray-300 hover:bg-gray-700 hover:text-white" -->
                    <a href="/" class="bg-gray-900 text-white block rounded-md px-3 py-2 text-base font-medium" aria-current="page">Home</a>
                    <a href="/about" class="text-gray-300 hover:bg-gray-700 hover:text-white block rounded-md px-3 py-2 text-base font-medium">About</a>
                    <a href="/contact" class="text-gray-300 hover:bg-gray-700 hover:text-white block rounded-md px-3 py-2 text-base font-medium">Contact</a>
                </div>
                <div class="border-t border-gray-700 pb-3 pt-4">
                    <div class="flex items-center px-5">
                        <div class="flex-shrink-0">
                            <img class="h-10 w-10 rounded-full" src="https://laracasts.com/images/lary-ai-face.svg" alt="">
                        </div>
                        <div class="ml-3">
                            <div class="text-base font-medium leading-none text-white">Lary Robot</div>
                            <div class="text-sm font-medium leading-none text-gray-400">jeffrey@laracasts.com</div>
                        </div>
                        <button type="button" class="relative ml-auto flex-shrink-0 rounded-full bg-gray-800 p-1 text-gray-400 hover:text-white focus:outline-none focus:ring-2 focus:ring-white focus:ring-offset-2 focus:ring-offset-gray-800">
                            <span class="absolute -inset-1.5"></span>
                            <span class="sr-only">View notifications</span>
                            <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" aria-hidden="true">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M14.857 17.082a23.848 23.848 0 005.454-1.31A8.967 8.967 0 0118 9.75v-.7V9A6 6 0 006 9v.75a8.967 8.967 0 01-2.312 6.022c1.733.64 3.56 1.085 5.455 1.31m5.714 0a24.255 24.255 0 01-5.714 0m5.714 0a3 3 0 11-5.714 0" />
                            </svg>
                        </button>
                    </div>
                </div>
            </div>
        </nav>

        <main>
            <div class="mx-auto max-w-7xl px-4 py-6 sm:px-6 lg:px-8">
                <h1 class="text-3xl font-bold tracking-tight text-gray-900">{{ $heading }}</h1>
            </div>
            <div class="mx-auto max-w-7xl px-4 py-6 sm:px-6 lg:px-8">
                {{ $slot }}
            </div>
        </main>
    </div>
</body>
</html>
```

### Actualizando las vistas con slots

Ahora en cada uno de los siguientes archivos: home, about y contact agregamos lo siguiente según corresponda:

**home.blade.php:**
```html
<x-layout>
    <x-slot:heading>
        Home Page
    </x-slot:heading>

    <h1>Hello from the Home Page.</h1>
</x-layout>
```

**about.blade.php:**
```html
<x-layout>
    <x-slot:heading>
        About Page
    </x-slot:heading>

    <h1>Hello from the About Page.</h1>
</x-layout>
```

**contact.blade.php:**
```html
<x-layout>
    <x-slot:heading>
        Contact Page
    </x-slot:heading>

    <h1>Hello from the Contact Page.</h1>
</x-layout>
```

### Resultado final

Al finalizar el episodio 04, la página debe verse con un diseño profesional utilizando Tailwind CSS, con una navegación moderna y responsiva.

![Pagina Web responsiva en ejecución con estilos](./images/01.PNG "Pagina web en ejecución responsiva")

## Episodio 05 - Style the Currently Active Navigation Link

### Modificando el layout principal

Realizamos cambios en el archivo `layout.blade.php` para mejorar la estructura del HTML:

```html
<html lang="en" class="h-full bg-gray-100">
<body class="h-full">
```

### Creando el componente nav-link

Creamos un componente personalizado para los enlaces de navegación. Archivo: `nav-link.blade.php` en la carpeta `components`:

```blade
@props(['active' => false])
<a class="{{ $active ? 'bg-gray-900 text-white': 'text-gray-300 hover:bg-gray-700 hover:text-white'}} rounded-md px-3 py-2 text-sm font-medium"
   aria-current="{{ $active ? 'page': 'false' }}"
   {{ $attributes }}
>{{ $slot }}</a>
```

### Implementando la navegación activa

Reemplazamos los enlaces de navegación HTML estático por componentes dinámicos que detectan la página actual en el archivo `layout.blade.php`:

**Antes:**
```html
<!-- Current: "bg-gray-900 text-white", Default: "text-gray-300 hover:bg-gray-700 hover:text-white" -->
<a href="/" class="bg-gray-900 text-white rounded-md px-3 py-2 text-sm font-medium" aria-current="page">Home</a>
<a href="/about" class="text-gray-300 hover:bg-gray-700 hover:text-white rounded-md px-3 py-2 text-sm font-medium">About</a>
<a href="/contact" class="text-gray-300 hover:bg-gray-700 hover:text-white rounded-md px-3 py-2 text-sm font-medium">Contact</a>
```

**Después:**
```blade
<x-nav-link href="/" :active="request()->is('/')">Home</x-nav-link>
<x-nav-link href="/about" :active="request()->is('about')">About</x-nav-link>
<x-nav-link href="/contact" :active="request()->is('contact')">Contact</x-nav-link>
```

**Resultado:** La barra de navegación ahora cambia el estilo cuando se pasa el mouse por encima de los enlaces.

![Pagina web en ejecución](./images/02.PNG "Pagina web resaltado de la barra de navegacion al pasar el mouse")

## Episodio 06 - View Data and Route Wildcards

### Configuración inicial

Agregamos el helper `Arr` de Laravel en el archivo `web.php` ubicado en el carpeta routes:

```php
use Illuminate\Support\Arr;
```

### Eliminando la ruta About

Comentamos o eliminamos la ruta anterior de about:

```php
// Route::get('/about', function () {
//     return view('about');
// });
```

### Creando la ruta Jobs con datos

Agregamos una nueva ruta que pasa un array de trabajos a la vista:

```php
Route::get('/jobs', function () {
    return view('jobs', [
        'jobs' => [
            [
                'id' => 1,
                'title' => 'Director',
                'salary' => '$50,000'
            ],
            [
                'id' => 2,
                'title' => 'Programmer',
                'salary' => '$10,000'
            ],
            [
                'id' => 3,
                'title' => 'Teacher',
                'salary' => '$40,000'
            ]
        ]
    ]);
});
```

### Creando ruta con wildcards

Implementamos una ruta dinámica que acepta un parámetro `id` para mostrar trabajos individuales:

```php
Route::get('/jobs/{id}', function ($id) {
    $jobs = [
        [
            'id' => 1,
            'title' => 'Director',
            'salary' => '$50,000'
        ],
        [
            'id' => 2,
            'title' => 'Programmer',
            'salary' => '$10,000'
        ],
        [
            'id' => 3,
            'title' => 'Teacher',
            'salary' => '$40,000'
        ]
    ];
    
    $job = Arr::first($jobs, fn($job) => $job['id'] == $id);
    return view('job', ['job' => $job]);
});
```

### Creando la vista Jobs

Renombramos `about.blade.php` a `jobs.blade.php` con el siguiente contenido:

```blade
<x-layout>
    <x-slot:heading>
        Job Listings
    </x-slot:heading>
    <ul>
        @foreach ($jobs as $job)
            <li>
                <a href="/jobs/{{ $job['id'] }}" class="text-blue-500 hover:underline">
                    <strong>{{ $job['title'] }}:</strong> Pays {{ $job['salary'] }} per year.
                </a>
            </li>
        @endforeach
    </ul>
</x-layout>
```

### Creando la vista Job individual

Creamos un nuevo archivo `job.blade.php` (singular) para mostrar trabajos individuales:

```blade
<x-layout>
    <x-slot:heading>
        Job
    </x-slot:heading>
    <h2 class="font-bold text-lg">{{ $job['title'] }}</h2>
    <p>
        This job pays {{ $job['salary'] }} per year.
    </p>
</x-layout>
```

### Actualizando la navegación

Modificamos el componente layout para cambiar el enlace de "About" por "Jobs":

```blade
<!-- Antes -->
<x-nav-link href="/about" :active="request()->is('about')">About</x-nav-link>

<!-- Después -->
<x-nav-link href="/jobs" :active="request()->is('jobs')">Jobs</x-nav-link>
```

### Resultado final

Al completar el episodio 6, la aplicación ahora:
- Muestra una lista de trabajos con sus salarios
- Permite hacer clic en cada trabajo para ver los detalles
- Utiliza wildcards en las rutas para pasar parámetros dinámicos
- Demuestra cómo pasar datos desde las rutas a las vistas

**Nota:** Los datos están hardcodeados por ahora. En episodios posteriores se hablara de eso a la base de datos.

![En página de jobs se muestra un listado de trabajos](./images/03.PNG "Seccion de Jobs funcionando")
![Página que muestra detalles de un trabjo especifico](./images/04.PNG "ID de Jobs en la ruta")

## Episodio 07 - Autoloading, Namespaces, and Models

### Actualizando el archivo web.php

Modificamos el archivo `web.php` para usar el modelo Job en lugar de datos hardcodeados:

```php
<?php
use Illuminate\Support\Facades\Route;
use App\Models\Job;

Route::get('/', function () {
    return view('home');
});

Route::get('/jobs', function () {
    return view('jobs', [
        'jobs' => Job::all()
    ]);
});

Route::get('/jobs/{id}', function ($id) {
    $job = Job::find($id);
    return view('job', ['job' => $job]);
});
```

### Buscando el directorio Models

Buscamos la carpeta `Models` dentro del directorio `app`:
```
app/
├── Models/
│   └── Job.php
```

### Creando el modelo Job

Creamos el archivo `Job.php` en `app/Models/` con el siguiente contenido:

```php
<?php
namespace App\Models;

use Illuminate\Support\Arr;

class Job {
    public static function all(): array
    {
        return [
            [
                'id' => 1,
                'title' => 'Director',
                'salary' => '$50,000'
            ],
            [
                'id' => 2,
                'title' => 'Programmer',
                'salary' => '$10,000'
            ],
            [
                'id' => 3,
                'title' => 'Teacher',
                'salary' => '$40,000'
            ]
        ];
    }

    public static function find(int $id): array
    {
        $job = Arr::first(static::all(), fn($job) => $job['id'] == $id);
        
        if (! $job) {
            abort(404);
        }
        
        return $job;
    }
}
```

### Conceptos clave del episodio

- **Autoloading**: Laravel automáticamente carga las clases siguiendo el estándar PSR-4
- **Namespaces**: Uso de `namespace App\Models;` para organizar el código
- **Modelos**: Separación de la lógica de datos en clases dedicadas
- **Métodos estáticos**: `all()` y `find()` como métodos de clase
- **Manejo de errores**: Uso de `abort(404)` cuando no se encuentra un trabajo
- **Reutilización**: El método `find()` utiliza `static::all()` para reutilizar la lógica

### Beneficios de esta refactorización

1. **Organización**: El código está mejor estructurado y separado por responsabilidades
2. **Reutilización**: Los datos se centralizan en el modelo
3. **Mantenibilidad**: Es más fácil modificar la lógica de datos en un solo lugar
4. **Escalabilidad**: Preparación para la futura integración con base de datos

# Unidad II - Eloquent

## Episodio 08 - Introduction to Migrations

### Introducción a las migraciones

Las migraciones son una característica fundamental de Laravel que permite versionar y gestionar cambios en la estructura de la base de datos. Esto elimina la necesidad de actualizar manualmente las tablas.

### Comando básico de migración

Laravel ya incluye migraciones predeterminadas. Para ejecutarlas usamos:

```bash
php artisan migrate
```

### Modificando migraciones existentes

Modificamos el archivo `create_users_table.php` ubicado en `database/migrations/`:

**Eliminamos esta línea:**
```php
$table->string('name');
```

**Agregamos estas dos líneas:**
```php
$table->string('first_name');
$table->string('last_name');
```

### Creando nuevas migraciones

Para crear una nueva migración para los trabajos, ejecutamos:

```bash
php artisan make:migration create_job_listings_table
```

Una vez hecho esto deberia verse asi.

![Migraciones](./images/05.PNG "Migraciones")

### Configuración del entorno

El comando se ejecuta en la máquina virtual webserver:

```bash
vagrant@webserver:~/sites/30days.isw811.xyz$
```

**Ubicación de la máquina virtual en la máquina anfitriona:**
```
/ISW811/M/VMs/webserver/
```

### Modificando la migración creada

El archivo creado desde la terminal debe modificarse para incluir la estructura de la tabla:

```php
<?php
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    /**
     * Run the migrations.
     */
    public function up(): void
    {
        Schema::create('job_listings', function (Blueprint $table) {
            $table->id();
            $table->string('title');
            $table->string('salary');
            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     */
    public function down(): void
    {
        Schema::dropIfExists('job_listings');
    }
};
```

### Ejecutando la migración

Ejecutamos el comando para aplicar la migración:

```bash
vagrant@webserver:~/sites/30days.isw811.xyz$ php artisan migrate
```

**Salida esperada:**
```
 INFO  Running migrations.
  2025_07_06_151255_create_job_listings_table .................. 147.05ms DONE
```

### Verificando en la base de datos

En MariaDB, dentro de la base de datos `30days`, ejecutamos:

```sql
show tables;
```

Veremos que se ha creado la tabla `job_listings`.

![Tablas de la base de datos en nuestro servidor de base de datos](./images/06.PNG "Tabla Job ha sido emigrada")

### Conceptos clave

- **Versionado**: Las migraciones permiten rastrear cambios en la base de datos
- **Colaboración**: Facilita el trabajo en equipo al sincronizar estructuras de BD
- **Reversibilidad**: Posibilidad de revertir cambios mediante rollbacks
- **Automatización**: Elimina la necesidad de cambios manuales en la base de datos

## Episodio 09 - Meet Eloquent

### Introducción a Eloquent

Eloquent es el ORM (Object-Relational Mapping) de Laravel que permite interactuar con la base de datos de forma elegante y expresiva.

### Iniciando Tinker

En la terminal ejecutamos:

```bash
vagrant@webserver:~/sites/30days.isw811.xyz$ php artisan tinker
```

### Primer intento de crear un registro

Intentamos crear un registro con:

```php
App\Models\Job::create(['title' => 'Acme Director', 'salary' => '$1,000,000']);
```

**Resultado:** Se produce un error por temas de seguridad que Laravel proporciona desde el inicio.

![Error al intentar crear un trabajo](./images/07.PNG "Error al intentar crear un trabajo")

### Configurando el modelo Job para Eloquent

Modificamos el archivo `Job.php` en la carpeta `models` para extender de Eloquent Model:

```php
<?php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Job extends Model {
    protected $table = 'job_listings';
    protected $fillable = ['title', 'salary'];
}
```

### Creando registros con Eloquent

Después de la configuración salimos del tinker con el comando `quit` y volvemos a ingresar `php artisan tinker` para que reconozca los cambios y ejecutamos nuevamente:

```php
App\Models\Job::create(['title' => 'Acme Director', 'salary' => '$1,000,000']);
```

**Resultado:** Se crea exitosamente el registro.

![Registro creado exitosamente](./images/08.PNG "Trabajo creado exitosamente")

### Agregando más registros

Continuamos creando más trabajos:

```php
App\Models\Job::create(['title' => 'Director', 'salary' => '50,000']);
App\Models\Job::create(['title' => 'Programmer', 'salary' => '$60,000']);
App\Models\Job::create(['title' => 'Teacher', 'salary' => '$50,000']);
```

### Consultando todos los registros

Para obtener todos los trabajos:

```php
App\Models\Job::all();
```

![Se muestran todos los trabajos anteriormente creados](./images/09.PNG "Todos los trabajos")

**Resultado:** Muestra todos los trabajos con id, título, salario y fechas de creación y actualización.

### Buscando por ID

Para buscar un trabajo específico:

```php
App\Models\Job::find(1);
```

![Se muestra un trabajo especifico](./images/10.PNG "Busqueda de Job por ID")

### Eliminando registros

Para eliminar un trabajo:

```php
$job->delete();
```

**Resultado:** Devuelve `true` si la eliminación fue exitosa.

### Conceptos clave de Eloquent

- **Fillable**: Protege contra asignación masiva especificando campos permitidos
- **Table**: Especifica el nombre de la tabla cuando no sigue la convención
- **Timestamps**: Maneja automáticamente `created_at` y `updated_at`
- **Métodos básicos**: `create()`, `all()`, `find()`, `delete()`

Con esto tenemos una base sólida de Eloquent para interactuar con la base de datos.

## Episodio 10 - Model Factories

**Parte de la serie:** 30 Days to Learn Laravel  
**Unidad:** II - Eloquent

## Introducción a Model Factories

Las Model Factories son una característica poderosa de Laravel que permite generar datos falsos de manera consistente y eficiente para testing y desarrollo.

## Actualizando UserFactory

Como anteriormente se modificó la tabla users en la migración reemplazando `name` por `first_name` y `last_name`, se debe actualizar UserFactory para evitar errores al generar datos falsos.

**Ubicación:** `database/factories/UserFactory.php`

```php
return [
    'first_name' => $this->faker->firstName(),
    'last_name' => $this->faker->lastName(),
    'email' => $this->faker->unique()->safeEmail(),
    'email_verified_at' => now(),
    'password' => bcrypt('password'),
    'remember_token' => Str::random(10),
];
```

> **Nota importante:** Si no hace esta modificación, al ejecutar `User::factory()->create()` se obtendrá un error por columna inexistente.

## Usando Factories con Tinker

### Iniciando Tinker

En la terminal ejecutamos:

```bash
vagrant@webserver:~/sites/30days.isw811.xyz$ php artisan tinker
```

### Crear un usuario

```php
App\Models\User::factory()->create();
```

### Crear múltiples usuarios

```php
App\Models\User::factory()->count(100)->create();
```

## Creando una Factory para el modelo Job

### Generando la factory

Creamos una nueva factory para el modelo Job:

```bash
php artisan make:factory JobFactory --model=Job
```

![JobFactory creado correctamente](./images/11.PNG "JobFactory creado")

### Configurando JobFactory

**Ubicación:** `database/factories/JobFactory.php`

Modificamos la función existente por:

```php
public function definition(): array
{
    return [
        'title' => $this->faker->jobTitle(),
        'employer_id' => Employer::factory(),
        'salary' => '$50,000 USD',
    ];
}
```

## Creando el modelo y migración para Employer

### Generando modelo y migración

```bash
php artisan make:model Employer -m
```
![Migración y modelo Employer creado correctamente](./images/12.PNG "Migración y modelo Employer creados")

### Configurando la migración

**Archivo:** `create_employers_table.php`

Modificamos la función `up` en el método `create` añadiendo `$table->string('name');`:

```php
public function up(): void
{
    Schema::create('employers', function (Blueprint $table) {
        $table->id();
        $table->string('name');
        $table->timestamps();
    });
}
```

### Eliminando modelo duplicado

Procedemos a borrar el modelo de Employer que está ubicado en la carpeta `app/Models` ya que lo crearemos nuevamente con la factory.

### Creando modelo con factory

```bash
php artisan make:model Employer -f
```
![EmployerFactory y modelo Employer creado correctamente](./images/13.PNG "EmployerFactory y modelo Employer creados")

### Configurando EmployerFactory

Modificamos la función dentro de nuestro archivo de `EmployerFactory` para añadir `'name' => fake()->company()`:

```php
public function definition(): array
{
    return [
        'name' => fake()->company(),
    ];
}
```

## Configurando la referencia en la migración de Jobs

Para que la relación entre Jobs y Employers funcione correctamente, necesitamos agregar la referencia de clave foránea en la migración de la tabla `job_listings`.

**Archivo:** `create_job_listings_table.php`

Modificamos la función `up` para incluir la referencia:

```php
public function up(): void
{
    Schema::create('job_listings', function (Blueprint $table) {
        $table->id();
        $table->foreignIdFor(\App\Models\Employer::class);
        $table->string(column: 'title');
        $table->string(column: 'salary');
        $table->timestamps();
    });
}
```

> **Nota:** `foreignIdFor()` automáticamente crea la columna `employer_id` con la referencia de clave foránea apropiada.

## Ejecutando las migraciones

Una vez configuradas las migraciones y factories, ejecutamos:

```bash
php artisan migrate:refresh
```
Advertencia: Este comando elimina todas las tablas y las vuelve a crear desde cero, perdiendo todos los datos existentes.

## Probando las Factories - Creando datos de prueba

### Usando Tinker para crear registros

Iniciamos Tinker:

```bash
php artisan tinker
```

### Creando 10 registros de cada modelo

```php
// Crear 10 employers
App\Models\Employer::factory()->count(10)->create();

// Crear 10 users
App\Models\User::factory()->count(10)->create();

// Crear 10 jobs (automáticamente creará employers si no existen)
App\Models\Job::factory()->count(10)->create();
```

### Verificando los datos creados

```php
// Verificar que se crearon los registros
App\Models\Employer::count(); // Debería mostrar 10 o más
App\Models\User::count(); // Debería mostrar 10 o más
App\Models\Job::count(); // Debería mostrar 10
```

## Conceptos clave

- **Factories**: Generan datos falsos consistentes para desarrollo y testing
- **Faker**: Biblioteca para generar datos falsos realistas
- **Comandos Artisan**: `-m` para migración, `-f` para factory
- **Consistencia**: Mantener la estructura de datos coherente entre migraciones y factories
- **Asignación masiva**: Uso de `fake()` para generar datos realistas
- **Relaciones**: Las factories pueden crear automáticamente modelos relacionados
- **Claves foráneas**: `foreignIdFor()` simplifica la creación de referencias entre tablas

## Beneficios de usar Model Factories

1. **Desarrollo eficiente**: Genera datos de prueba rápidamente
2. **Testing**: Facilita la creación de datos para pruebas
3. **Consistencia**: Mantiene la estructura de datos uniforme
4. **Flexibilidad**: Permite personalizar los datos generados según necesidades específicas
5. **Relaciones automáticas**: Crea automáticamente los modelos relacionados necesarios

## Episodio 11 - Eloquent Relationships

## Introducción a las Relaciones de Eloquent

Las relaciones de Eloquent son una característica fundamental de Laravel que permite definir y trabajar con conexiones entre diferentes modelos de base de datos de manera elegante y eficiente.

## Definiendo la relación One-to-Many (Uno a Muchos)

### Configurando el modelo Employer

En el modelo `Employer` ubicado en `app/Models/Employer.php`, añadimos la siguiente función para definir la relación:

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Employer extends Model
{
    use HasFactory;

    public function jobs()
    {
        return $this->hasMany(Job::class);
    }
}
```

### Entendiendo la relación hasMany

- **hasMany**: Define una relación uno a muchos
- **Job::class**: Especifica el modelo relacionado
- **Convención**: Laravel automáticamente busca la columna `employer_id` en la tabla `jobs`

## Trabajando con relaciones en Tinker

### Iniciando Tinker

```bash
php artisan tinker
```

### Obteniendo un empleador

```php
$employer = App\Models\Employer::first();
```

### Accediendo a los trabajos del empleador

```php
// Obtener todos los trabajos de un empleador
$employer->jobs;
```
![Trabajos de un empleador](./images/14.PNG "Trabajos de un empleador")

Este comando devuelve una **Collection** con todos los trabajos asociados al empleador.

### Diferentes formas de acceder a los datos

#### 1. Acceso como array

```php
// Obtener el primer trabajo usando índice de array
$employer->jobs[0];
```

#### 2. Usando métodos de Collection

```php
// Obtener el primer trabajo usando el método first()
$employer->jobs->first();

// Obtener el último trabajo
$employer->jobs->last();

// Contar los trabajos
$employer->jobs->count();
```

### Explorando métodos de Collection

Las Collections de Laravel ofrecen muchos métodos útiles:

```php
// Verificar si la colección está vacía
$employer->jobs->isEmpty();

// Verificar si la colección tiene elementos
$employer->jobs->isNotEmpty();

// Obtener solo los títulos de los trabajos
$employer->jobs->pluck('title');

// Filtrar trabajos por salario
$employer->jobs->where('salary', '>', 50000);

// Obtener el primer trabajo que coincida con una condición
$employer->jobs->firstWhere('title', 'Developer');
```

## Definiendo la relación inversa (belongsTo)

### Configurando el modelo Job

En el modelo `Job` ubicado en `app/Models/Job.php`, añadimos la relación inversa:

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Job extends Model
{
    use HasFactory;

    public function employer()
    {
        return $this->belongsTo(Employer::class);
    }
}
```

### Usando la relación belongsTo

```php
// Obtener un trabajo
$job = App\Models\Job::first();

// Acceder al empleador de ese trabajo
$job->employer;

// Acceder al nombre del empleador
$job->employer->name;
```

## Ventajas de usar Eloquent Relationships

### 1. Lazy Loading
```php
// Solo se ejecuta la consulta cuando accedes a la relación
$employer = Employer::first();
$jobs = $employer->jobs; // Consulta SQL ejecutada aquí
```

### 2. Eager Loading
```php
// Cargar empleadores con sus trabajos en una sola consulta
$employers = Employer::with('jobs')->get();
```

### 3. Consultas dinámicas
```php
// Obtener empleadores que tienen trabajos
$employersWithJobs = Employer::has('jobs')->get();

// Contar trabajos por empleador
$employersWithJobCount = Employer::withCount('jobs')->get();
```

## Ejemplos prácticos de uso

### Creando trabajos para un empleador específico

```php
// Obtener un empleador
$employer = Employer::first();

// Crear un nuevo trabajo para este empleador
$job = new Job();
$job->title = 'Senior Developer';
$job->salary = '$80,000 USD';
$employer->jobs()->save($job);
```

### Usando create() con relaciones

```php
// Crear un trabajo directamente asociado a un empleador
$employer->jobs()->create([
    'title' => 'Project Manager',
    'salary' => '$70,000 USD'
]);
```

### Consultando datos relacionados

```php
// Obtener todos los trabajos de un empleador específico
$googleJobs = Employer::where('name', 'Google')->first()->jobs;

// Obtener empleadores con más de 5 trabajos
$busyEmployers = Employer::has('jobs', '>', 5)->get();
```

## Conceptos clave

- **hasMany**: Relación uno a muchos (un empleador tiene muchos trabajos)
- **belongsTo**: Relación inversa (un trabajo pertenece a un empleador)
- **Collection**: Estructura de datos que contiene múltiples modelos
- **Lazy Loading**: Las relaciones se cargan solo cuando se accede a ellas
- **Eager Loading**: Cargar relaciones de manera anticipada para optimizar consultas
- **Métodos de Collection**: `first()`, `last()`, `count()`, `pluck()`, `where()`, etc.

## Beneficios de las relaciones Eloquent

1. **Sintaxis limpia**: Acceso intuitivo a datos relacionados
2. **Optimización automática**: Laravel optimiza las consultas SQL
3. **Flexibilidad**: Múltiples formas de acceder y manipular datos
4. **Consistencia**: Mantiene la integridad de los datos relacionados
5. **Productividad**: Reduce significativamente el código necesario para trabajar con relaciones

## Episodio 12 - Pivot Tables and Many-to-Many Relationships

### Introducción a las Relaciones Many-to-Many

Las relaciones muchos a muchos (many-to-many) son fundamentales en las bases de datos cuando necesitamos conectar dos modelos donde cada uno puede estar relacionado con múltiples registros del otro. En nuestro caso, un trabajo puede tener múltiples etiquetas y una etiqueta puede estar asociada a múltiples trabajos.

## Creando el modelo Tag con migración y factory

### Generando el modelo completo

Para crear el modelo Tag junto con su migración y factory, ejecutamos:

```bash
php artisan make:model Tag -mf
```

Este comando genera:
- `app/Models/Tag.php` (el modelo)
- `database/migrations/create_tags_table.php` (la migración)
- `database/factories/TagFactory.php` (la factory)

## Configurando la migración de Tags

### Modificando la migración principal

**Archivo:** `create_tags_table.php`

Modificamos la función `up` para incluir el campo `name`:

```php
public function up(): void
{
    Schema::create('tags', function (Blueprint $table) {
        $table->id();
        $table->string('name');
        $table->timestamps();
    });
}
```

### Creando la tabla pivot

Dentro de la misma migración, después de la creación de la tabla `tags`, agregamos la tabla pivot:

```php
public function up(): void
{
    Schema::create('tags', function (Blueprint $table) {
        $table->id();
        $table->string('name');
        $table->timestamps();
    });

    Schema::create('job_tag', function (Blueprint $table) {
        $table->id();
        $table->foreignIdFor(\App\Models\Job::class, 'job_listing_id')->constrained()->cascadeOnDelete();
        $table->foreignIdFor(\App\Models\Tag::class)->constrained()->cascadeOnDelete();
        $table->timestamps();
    });
}
```

### Configurando el método down

Para el rollback, actualizamos la función `down`:

```php
public function down(): void
{
    Schema::dropIfExists('job_tag');
    Schema::dropIfExists('tags');
}
```

> **Nota:** Es importante eliminar primero la tabla pivot (`job_tag`) antes que las tablas principales debido a las restricciones de claves foráneas.

## Entendiendo las tablas pivot

### ¿Qué es una tabla pivot?

Una tabla pivot es una tabla intermedia que conecta dos modelos en una relación muchos a muchos. En nuestro caso:

- **Tabla `job_listings`**: Contiene los trabajos
- **Tabla `tags`**: Contiene las etiquetas
- **Tabla `job_tag`**: Conecta trabajos con etiquetas

### Estructura de la tabla pivot

```sql
job_tag:
- id
- job_listing_id (clave foránea hacia job_listings)
- tag_id (clave foránea hacia tags)
- created_at
- updated_at
```

### Restricciones de integridad

Las restricciones `constrained()->cascadeOnDelete()` garantizan:

1. **Integridad referencial**: No se pueden crear relaciones con IDs inexistentes
2. **Eliminación en cascada**: Si se elimina un trabajo o etiqueta, sus relaciones se eliminan automáticamente
3. **Prevención de registros huérfanos**: Evita datos inconsistentes en la tabla pivot

## Ejecutando las migraciones

### Aplicando los cambios

Para aplicar los cambios realizados en la migración:

```bash
php artisan migrate:rollback && php artisan migrate
```

Este comando:
1. Revierte la última migración
2. Ejecuta nuevamente todas las migraciones

### Verificando en la base de datos

En MariaDB, verificamos que las tablas se crearon correctamente:

```sql
SHOW TABLES;
```

Deberíamos ver:
- `tags`
- `job_tag`

## Consideraciones con SQLite

Si trabajas con SQLite directamente (por ejemplo, con Herd), es necesario activar las restricciones de claves foráneas:

```sql
PRAGMA foreign_keys = ON;
```

> **Nota:** Laravel maneja esto automáticamente en la mayoría de entornos, pero es útil conocerlo para desarrollo local.

## Definiendo las relaciones en los modelos

### Configurando el modelo Job

En `app/Models/Job.php`, agregamos la relación many-to-many:

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Job extends Model
{
    use HasFactory;

    protected $table = 'job_listings';
    protected $fillable = ['title', 'salary'];

    public function employer()
    {
        return $this->belongsTo(Employer::class);
    }

    public function tags()
    {
        return $this->belongsToMany(Tag::class, foreignPivotKey: "job_listing_id");
    }
}
```

### Configurando el modelo Tag

En `app/Models/Tag.php`, definimos la relación inversa:

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Tag extends Model
{
    use HasFactory;

    protected $fillable = ['name'];

    public function jobs()
    {
        return $this->belongsToMany(Job::class, relatedPivotKey: "job_listing_id");
    }
}
```

## Entendiendo los parámetros de belongsToMany

### Parámetros utilizados

- **`foreignPivotKey`**: Especifica la clave foránea del modelo actual en la tabla pivot
- **`relatedPivotKey`**: Especifica la clave foránea del modelo relacionado en la tabla pivot

### ¿Por qué necesitamos estos parámetros?

Laravel sigue convenciones de nomenclatura, pero nuestro caso es especial:

- **Convención esperada**: `job_id` en la tabla pivot
- **Nuestro caso**: `job_listing_id` porque nuestra tabla se llama `job_listings`

## Trabajando con relaciones Many-to-Many

### Usando Tinker para probar las relaciones

```bash
php artisan tinker
```

### Asociando tags a trabajos

## Asociando tags a trabajos

```php
// Obtener un trabajo
$job = App\Models\Job::first();

// Asociar etiquetas al trabajo usando attach
$job->tags()->attach([1, 2, 3]);

// O usando el método sync para reemplazar todas las etiquetas
$job->tags()->sync([1, 2]);
```

### Consultando relaciones

```php
// Obtener todas las etiquetas de un trabajo
$job->tags;

// Obtener todos los trabajos de una etiqueta
$phpTag = App\Models\Tag::find(1);
$phpTag->jobs;

// Verificar si un trabajo tiene una etiqueta específica
$job->tags->contains($phpTag);
```

## Métodos útiles para relaciones Many-to-Many

### Métodos de manipulación

```php
// Asociar etiquetas (mantiene las existentes)
$job->tags()->attach([1, 2, 3]);

// Desasociar etiquetas específicas
$job->tags()->detach([1, 2]);

// Desasociar todas las etiquetas
$job->tags()->detach();

// Sincronizar (reemplaza todas las etiquetas)
$job->tags()->sync([1, 2, 3]);

// Alternar etiquetas (asocia las que no están, desasocia las que sí)
$job->tags()->toggle([1, 2, 3]);
```

### Métodos de consulta

```php
// Contar etiquetas de un trabajo
$job->tags()->count();

// Verificar si tiene etiquetas
$job->tags()->exists();

// Obtener trabajos que tienen etiquetas específicas
$jobsWithPHP = App\Models\Job::whereHas('tags', function($query) {
    $query->where('name', 'PHP');
})->get();
```

## Conceptos clave

- **Tabla Pivot**: Tabla intermedia que conecta dos modelos en relaciones many-to-many
- **belongsToMany**: Método para definir relaciones muchos a muchos
- **foreignPivotKey**: Clave foránea del modelo actual en la tabla pivot
- **relatedPivotKey**: Clave foránea del modelo relacionado en la tabla pivot
- **Restricciones en cascada**: `cascadeOnDelete()` elimina automáticamente relaciones cuando se elimina un modelo
- **Integridad referencial**: `constrained()` garantiza que las claves foráneas sean válidas

## Beneficios de las relaciones Many-to-Many

1. **Flexibilidad**: Permite relaciones complejas entre modelos
2. **Normalización**: Evita duplicación de datos
3. **Integridad**: Mantiene consistencia en la base de datos
4. **Eficiencia**: Optimiza consultas y almacenamiento
5. **Escalabilidad**: Facilita el crecimiento de la aplicación.

## Capítulo 13: Eager Loading and the N+1 Problem

### Mejorando la Vista de Trabajos

### Actualización de jobs.blade.php

Comenzamos mejorando la presentación de nuestra vista de trabajos. Navegamos al archivo `resources/views/jobs.blade.php` y reemplazamos el código existente por:

```blade
<x-layout>
    <x-slot:heading>
        Job Listings
    </x-slot:heading>
    <div class="space-y-4">
        @foreach ($jobs as $job)
        <a href="/jobs/{{ $job['id'] }}" class="block px-4 py-6 border border-gray-200 rounded-lg">
            <div class="font-bold text-blue-500 text-sm">{{ $job->employer->name }}</div>
            <div>
                <strong>{{ $job['title'] }}:</strong> Pays {{ $job['salary'] }} per year.
            </div>
        </a>
        @endforeach
    </div>
</x-layout>
```

Este cambio hace que nuestra vista se vea más elegante y profesional, con un diseño de tarjetas que mejora la experiencia del usuario.

## Instalación de Laravel Debugbar

Para monitorear el rendimiento de nuestra aplicación, especialmente las consultas a la base de datos, instalamos Laravel Debugbar:

```bash
composer require barryvdh/laravel-debugbar --dev
```

### Configuración del Debug

Es importante asegurarse de que el debugging esté habilitado en el archivo `.env`:

```env
APP_DEBUG=true
```

Una vez instalado, veremos una barra de depuración en la parte inferior de nuestras páginas que nos proporciona información valiosa sobre:
- Consultas a la base de datos
- Tiempo de respuesta
- Uso de memoria
- Variables de sesión
- Y mucho más

## Optimización con Eager Loading

### Problema del N+1 Query

Inicialmente, nuestra ruta en `routes/web.php` tenía un problema de rendimiento conocido como "N+1 Query Problem":

```php
Route::get('/jobs', function () {
    $jobs = Job::all(); // Una consulta para obtener todos los jobs
    return view('jobs', [
        'jobs' => $jobs
    ]);
});
```

Con este código, cuando mostramos `$job->employer->name` en la vista, Laravel ejecuta una consulta adicional por cada trabajo para obtener el empleador correspondiente.

### Solución: Eager Loading

Para solucionar este problema, actualizamos la ruta para usar **eager loading**:

```php
Route::get('/jobs', function () {
    $jobs = Job::with('employer')->get();
    return view('jobs', [
        'jobs' => $jobs
    ]);
});
```

El método `with('employer')` le dice a Laravel que cargue la relación `employer` junto con los trabajos en una sola consulta adicional, reduciendo significativamente el número de consultas a la base de datos.

## Prevención de Lazy Loading

### Configuración en AppServiceProvider

Para detectar y prevenir problemas de lazy loading durante el desarrollo, añadimos la siguiente configuración en `app/Providers/AppServiceProvider.php`:

```php
<?php

namespace App\Providers;

use Illuminate\Support\ServiceProvider;
use Illuminate\Database\Eloquent\Model;

class AppServiceProvider extends ServiceProvider
{
    public function boot()
    {
        Model::preventLazyLoading();
    }
}
```

### Beneficios de Prevenir Lazy Loading

- **Detección temprana**: Nos alerta cuando estamos haciendo consultas lazy loading no intencionadas
- **Mejor rendimiento**: Nos fuerza a ser explícitos sobre qué relaciones necesitamos cargar
- **Código más limpio**: Hace que nuestro código sea más predecible y fácil de optimizar

## Impacto en el Rendimiento

Con la implementación de eager loading, observamos una mejora significativa en el rendimiento:

- **Antes**: N+1 consultas (1 consulta para trabajos + 1 consulta por cada trabajo para obtener el empleador)
- **Después**: 2 consultas totales (1 para trabajos + 1 para todos los empleadores)

Esta optimización es especialmente importante cuando tenemos muchos registros, ya que la diferencia puede ser dramática (por ejemplo, de 101 consultas a solo 2 consultas para 100 trabajos).

### Episodio 14 - All You Need to Know About Pagination

### Introducción a la paginación

La paginación es una característica esencial en aplicaciones web que permite dividir grandes conjuntos de datos en páginas más pequeñas y manejables. Laravel proporciona un sistema de paginación integrado y fácil de implementar.

### Modificando la ruta Jobs

Actualizamos la ruta en `web.php` para implementar paginación:

```php
Route::get('/jobs', function () {
    $jobs = Job::with('employer')->paginate(3);
    return view('jobs', [
        'jobs' => $jobs
    ]);
});
```

Este código:
- Recupera 3 registros de trabajos por página
- Incluye los empleadores usando eager loading para evitar el problema N+1
- Utiliza el método `paginate()` en lugar de `all()`

### Actualizando la vista Jobs

Modificamos el archivo `jobs.blade.php` para incluir los enlaces de paginación:

```blade
<x-layout>
    <x-slot:heading>
        Job Listings
    </x-slot:heading>
    <div class="space-y-4">
        @foreach ($jobs as $job)
        <a href="/jobs/{{ $job['id'] }}" class="block px-4 py-6 border border-gray-200 rounded-lg">
            <div class="font-bold text-blue-500 text-sm">{{ $job->employer->name }}</div>
            <div>
                <strong>{{ $job['title'] }}:</strong> Pays {{ $job['salary'] }} per year.
            </div>
        </a>
        @endforeach
        <div>
            {{ $jobs->links() }}
        </div>
    </div>
</x-layout>
```

**Cambios principales:**
- Agregamos `{{ $jobs->links() }}` para mostrar los enlaces de paginación
- Mantenemos la estructura del loop `@foreach` existente
- Los enlaces se muestran debajo de la lista de trabajos

### Personalizar las vistas de paginación

Si deseas modificar el diseño o usar otro framework como Bootstrap, puedes publicar las vistas:

```bash
php artisan vendor:publish --tag=laravel-pagination
```

Esto copiará las vistas a:
```
resources/views/vendor/pagination
```

### Usando Bootstrap en lugar de Tailwind

Para cambiar el framework CSS de paginación, agrega esto en `AppServiceProvider`:

```php
use Illuminate\Pagination\Paginator;

public function boot()
{
    Paginator::useBootstrapFive();
}
```

### Tipos de paginación

Laravel ofrece diferentes tipos de paginación según tus necesidades:

| Tipo | Descripción | Método |
|------|-------------|---------|
| **Paginación estándar** | Números de página + enlaces prev/sig | `paginate()` |
| **Simple** | Solo muestra "Anterior" y "Siguiente" | `simplePaginate()` |
| **Cursor** | Usa un cursor codificado, más eficiente | `cursorPaginate()` |

**Ejemplos de uso:**

```php
// Paginación simple
Job::with('employer')->simplePaginate(3);

// Paginación con cursor
Job::with('employer')->cursorPaginate(3);
```

### Funcionamiento interno

- **`paginate()`**: Utiliza `LIMIT` y `OFFSET` en SQL para obtener los registros
- **`cursorPaginate()`**: Evita el uso de `OFFSET` y mejora el rendimiento con grandes volúmenes de datos, especialmente útil para datasets que crecen constantemente

### Conceptos clave del episodio

- **Paginación automática**: Laravel maneja automáticamente los parámetros de consulta
- **Eager loading**: Combinación con `with()` para optimizar consultas
- **Flexibilidad**: Múltiples tipos de paginación según las necesidades
- **Personalización**: Posibilidad de modificar el diseño y comportamiento
- **Rendimiento**: Diferentes estrategias para diferentes casos de uso

## Episodio 15 - Understanding Database Seeders

En este episodio, se introduce el concepto de "seeders" en Laravel, que son clases utilizadas para poblar la base de datos con datos iniciales. Se muestra cómo crear un seeder para el modelo `Job` y `User` y cómo utilizarlo para generar múltiples registros en la tabla `jobs_listings`.

### Creación de un Seeder para el modelo `Job`

```bash
php artisan make:seeder JobSeeder
```
### Implementación del Seeder
```php
public function run(): void
    {
        Job::factory(100)->create();
    }
```
### Uso del Seeder en `DatabaseSeeder.php`
```php
public function run(): void
    {
        // User::factory(10)->create();

        User::factory()->create([
            'first_name' => 'Guillermo',
            'last_name' => 'Solórzano',
            'email' => 'test@example.com',
        ]);

        $this->call(JobSeeder::class);
    }
```

### Ejecución del Seeder
+ Para ejecutar el seeder y poblar la base de datos, utiliza el siguiente comando:
```bash
php artisan db:seed
```
+ Para reiniciar la base de datos y volver a ejecutar todos los seeders, puedes usar el siguiente comando:
```bash
php artisan migrate:fresh --seed
```
+ Para ejecutar un seeder específico, puedes usar el siguiente comando:
```bash
php artisan db:seed --class=JobSeeder
```

### Verificación de los datos insertados
Puedes verificar los datos insertados en la base de datos desde DBeaver:
![Datos](./images/16.PNG)

## Episodio 15 - Understanding Database Seeders

### Introducción a los Seeders

Los **seeders** en Laravel permiten poblar la base de datos con datos de prueba de forma automatizada. Son útiles para desarrollo, pruebas y creación rápida de entornos consistentes.

---

### Creando un seeder para el modelo Job

Ejecutamos el comando para generar un seeder:

```bash
php artisan make:seeder JobSeeder
```

Esto creará un archivo en: `database/seeders/JobSeeder.php`.

---

### Implementando el JobSeeder

Editamos el archivo generado para usar la factory de `Job` y crear múltiples registros:

```php
use App\Models\Job;

public function run(): void
{
    Job::factory(100)->create();
}
```

Esto genera 100 trabajos usando datos falsos.

---

### Usando el seeder en DatabaseSeeder

Editamos el archivo `database/seeders/DatabaseSeeder.php` para llamar a `JobSeeder` y generar también un usuario de ejemplo:

```php
use App\Models\User;
use Illuminate\Database\Seeder;

public function run(): void
{
    // Crear un usuario de prueba
    User::factory()->create([
        'first_name' => 'Guillermo',
        'last_name' => 'Solórzano',
        'email' => 'test@example.com',
    ]);

    // Llamar al seeder de trabajos
    $this->call(JobSeeder::class);
}
```

---

### Ejecutando los seeders

#### 1. Ejecutar todos los seeders
```bash
php artisan db:seed
```

#### 2. Ejecutar un seeder específico
```bash
php artisan db:seed --class=JobSeeder
```

#### 3. Reiniciar base de datos y seedear desde cero
```bash
php artisan migrate:fresh --seed
```

Este comando elimina todas las tablas, las migra de nuevo y ejecuta los seeders.

### Verificando los datos

Podemos inspeccionar los datos generados usando herramientas como DBeaver o el comando:

```php
App\Models\Job::count();
```

Con DBeaver

![Datos creados con seeders](./images/16.PNG "Datos creados por seeders")

### Conceptos clave del episodio

- **Seeders**: Automatizan la inserción de datos de prueba
- **Factories + Seeders**: Combinación poderosa para poblar modelos relacionados
- **DatabaseSeeder**: Punto de entrada para ejecutar múltiples seeders
- **Datos consistentes**: Facilitan pruebas repetibles y entornos de desarrollo confiables

---

### Beneficios del uso de Seeders

1. **Agiliza el desarrollo**: Crea entornos completos en segundos  
2. **Facilita testing**: Proporciona datos para pruebas automatizadas  
3. **Evita errores humanos**: No requiere inserciones manuales  
4. **Escenarios realistas**: Genera múltiples combinaciones de datos  
5. **Repetibilidad**: Reestablece siempre los mismos datos en todos los equipos

_Documentación realizada por Guillermo Antonio Solórzano Ochoa - ISW811_