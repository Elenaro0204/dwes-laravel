# 17-02-2025

---

## Iniciación Laravel

Creación del repositorio en github

# 18-02-2025

---

## Instalación Larabel

Estamos siguiendo el curso de Youtube con la siguiente dirección: https://www.youtube.com/watch?v=A-BL8Ir7puE&list=PLZ2ovOgdI-kWWS9aq8mfUDkJRfYib-SvF

### Pasos

1. Ir a la siguiente ruta para descargarlo: https://getcomposer.org/
2. Descargar y dejar toda la configuración predeterminada
3. Desde Git Bash acceder a la carpeta donde se van a guardar los archivos (en mi caso: /c/xampp/htdocs/laravel)
4. Escribir el siguiente comando: `composer global require laravel/installer`
5. Modificar tambien la direccion del XAMPP
6. Para crear un proyecto, desde la carpeta htdocs en la consola ‘Git Bash’, ejecutar el siguiente comando, que creara la carpeta del proyecto con la estructura de directorios y ficheros iniciales: `Laravel new nombreProyecto`
7. Una vez instalado, entrar en el proyecto y escribir el siguiente comando: `code .`
8. Iniciar el proyecto con `php artisan serve`
9. Creación del proyecto y escribir el siguiente comando: `Laravel new nombreProyecto` o `composer create-project laravel/laravel nombreProyecto`

# 21/02/2025

---

## Rutas

Una **ruta** en Laravel es una regla definida en el archivo `routes/web.php` que asocia una **URL** con una **acción específica** dentro de la aplicación.

Cada ruta indica:

1. **El método HTTP** (GET, POST, PUT, DELETE, etc.).
2. **La URL** que el usuario ingresa en el navegador.
3. **La acción que se ejecutará**, que puede ser:
   - Una función anónima.
   - Un método de un controlador.
   - Una vista directa.
   - Una redirección.

### Ejemplo de rutas:

```php
Route::get('hola', function () { return 'Hello World'; }); // Ruta simple
Route::get('hola/{nombre}', function ($nombre) { return 'Hello ' . $nombre; }); // Ruta con parámetro
Route::view('/error', 'error'); // Ruta que devuelve una vista
Route::redirect('/inicio', '/home'); // Ruta que redirige
```

### Rutas con controlador:

```php
Route::get('productos', [ProductoController::class, 'index'])->name('productos.index');
```

Esta ruta responde a `GET /productos` y llama al método `index()` de `ProductoController`.

Las rutas se ejecutan **de arriba a abajo**, y cuando se encuentra una coincidencia, Laravel deja de buscar más opciones.

## Controladores

En una aplicación **CRUD**, cada **tabla/modelo** de la base de datos tiene su propio **controlador**, ubicado en `app/Http/Controllers/`, con los métodos necesarios para gestionar los datos.

### Creación de un controlador con Artisan:

```bash
php artisan make:controller NombreController
```

Esto genera automáticamente el archivo en `app/Http/Controllers/`.

### Importar el controlador en `routes/web.php`:

Después de crearlo, se debe importar con:

```php
use App\Http\Controllers\NombreController;
```

### Definir rutas con un controlador:

- **Si no se especifica un método**, se llama por defecto a `__invoke()`:
  ```php
  Route::get('/', HomeController::class);
  ```
- **Para llamar a un método específico** del controlador:
  ```php
  Route::get('cursos', [CursoController::class, 'index']);
  ```

### Métodos en el controlador:

Para completar el **CRUD**, se crean métodos en el controlador que, tras procesar los datos, devuelven una **vista** correspondiente.

### Redirección desde un método del controlador:

En lugar de devolver una vista, se puede redirigir a otra ruta:

```php
return redirect()->route('inicio'); // Redirige a la ruta con nombre 'inicio'
```

## Vistas

Las **vistas** en Laravel se crean en la carpeta `resources/views/` y contienen la estructura **HTML** de la página.

### Devolver una vista desde un controlador:

Para mostrar una vista desde un **método del controlador**, se usa:

```php
return view('nombreVista');
```

**No es necesario** indicar la carpeta `resources/views/` ni la extensión `.blade.php`.

### Convención de nombres:

Se recomienda que el nombre de la vista coincida con el **método del controlador** que la devuelve y con la **tabla** con la que opera.  
Ejemplo en `CursoController`:

```php
return view('cursos.create'); // Devuelto por el método create()
```

### Pasar parámetros a la vista:

Se usa un **array asociativo** como segundo parámetro de `view()`:

```php
return view('nombreRuta', ['curso' => $curso]);
```

Si el **nombre del parámetro** coincide con la variable, se puede simplificar con `compact()`:

```php
return view('nombreRuta', compact('curso'));
```
