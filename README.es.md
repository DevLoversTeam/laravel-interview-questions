**Read in other languages: [English 🇺🇸](README.en.md),
[Polska 🇵🇱](README.pl.md), [German 🇩🇪](README.de.md), [French 🇫🇷](README.fr.md),
[Spanish 🇪🇸](README.es.md), [Українська 🇺🇦](README.md).**

<h1>
  Laravel <img src="./assets/laravel.svg" width="40" height="40" alt="Laravel logo"/>
</h1>

<h2>Las preguntas y respuestas más populares de entrevistas sobre Laravel</h2>

<details>
<summary>1. ¿Qué es Laravel y por qué se usa?</summary>

#### Laravel

Laravel es un framework web moderno de PHP enfocado en la productividad del desarrollador, una arquitectura limpia y código mantenible.

1. **Qué es Laravel**

- Un framework de código abierto construido sobre componentes de Symfony.
- Lo suficientemente opinado para ofrecer buenas convenciones por defecto, pero flexible para una arquitectura personalizada.

2. **Por qué se usa**

- Acelera el desarrollo con enrutamiento, validación, autenticación, colas, correo, eventos y caché integrados.
- Fomenta código limpio mediante el contenedor de servicios, middleware, Eloquent ORM y herramientas de testing.
- Proporciona tooling oficial (`Artisan`, migraciones, scheduler, Horizon, Telescope) para aplicaciones listas para producción.

3. **Casos de uso típicos**

- APIs REST y servicios backend.
- Aplicaciones web renderizadas en servidor.
- Paneles de administración, productos SaaS y plataformas de marketplace.
- Procesamiento de trabajos en segundo plano e integraciones con servicios de terceros.

En resumen, Laravel se utiliza para crear aplicaciones PHP seguras, escalables y mantenibles más rápido y con menos boilerplate.

</details>

<details>
<summary>2. ¿Cuáles son las principales ventajas de Laravel en comparación con otros frameworks PHP?</summary>

#### Laravel

Las principales ventajas de Laravel provienen de una excelente experiencia de desarrollador, funciones integradas ricas y un gran ecosistema.

1. **Experiencia de desarrollador**

- Diseño de API consistente y expresivo en todos los componentes del framework.
- Excelente documentación y onboarding.
- Generación rápida de estructura y flujos CLI mediante `Artisan`.

2. **Incluye funcionalidades clave**

- Soporte de primera clase para routing, validación, auth, colas, eventos, notificaciones, caché y scheduling.
- ORM (Eloquent) y migraciones de esquema incluidos por defecto.

3. **Arquitectura y mantenibilidad**

- El contenedor de servicios y la inyección de dependencias están profundamente integrados.
- Middleware y service providers hacen explícitas las preocupaciones transversales.
- Fuerte soporte de testing con integración de PHPUnit/Pest.

4. **Fortaleza del ecosistema**

- Herramientas oficiales: Forge, Vapor, Horizon, Telescope, Octane, Sanctum, Passport, Cashier.
- Paquetes de comunidad maduros y estabilidad del ecosistema a largo plazo.

5. **Productividad operativa**

- Flujos de CI/CD y despliegue fluidos.
- Gran soporte para colas, caché, Redis y monitoreo.

Laravel suele elegirse cuando los equipos quieren entregar funcionalidades de negocio rápido sin sacrificar calidad de código ni mantenibilidad a largo plazo.

</details>

<details>
<summary>3. ¿Cómo sigue Laravel la arquitectura MVC?</summary>

#### Laravel

Laravel sigue MVC (Model-View-Controller) separando la lógica de dominio/datos, el manejo de solicitudes y la presentación.

1. **Modelo (M)**

- Normalmente modelos Eloquent en `app/Models`.
- Representan entidades de dominio y registros de base de datos.
- Contienen relaciones, scopes, casts y comportamiento de dominio.

2. **Vista (V)**

- Plantillas Blade en `resources/views`.
- Responsables solo de la presentación.
- Reciben datos preparados desde controladores/view models.

3. **Controlador (C)**

- Clases en `app/Http/Controllers`.
- Gestionan solicitudes HTTP, coordinan validación/servicios y devuelven respuestas.
- Deben mantenerse ligeros: orquestación, no lógica de negocio pesada.

4. **Flujo de solicitud en términos MVC**

- La ruta mapea la URL a una acción del controlador.
- El controlador usa modelos/servicios para ejecutar el caso de uso.
- El controlador devuelve una vista (HTML) o una respuesta JSON (API).

Laravel también admite clases de servicio, actions, repositories y capas de dominio sobre MVC para aplicaciones grandes.

</details>

<details>
<summary>4. Describe el ciclo de vida de una solicitud en una aplicación Laravel.</summary>

#### Laravel

El ciclo de vida de una solicitud en Laravel describe cómo una solicitud HTTP entrante se transforma en una respuesta.

1. **Punto de entrada**

- El servidor web apunta a `public/index.php`.
- Se cargan el autoloader de Composer y el bootstrap de la aplicación Laravel.

2. **Inicio del kernel HTTP**

- Se inicializa el contenedor de servicios.
- Se preparan los stacks de middleware global y de rutas.

3. **Service providers**

- Los providers se registran y se inicializan (boot).
- Los servicios core y bindings de la app quedan disponibles.

4. **Fase de routing**

- El router hace match entre método + URI y una ruta.
- Se ejecuta el pipeline de middleware de ruta.

5. **Ejecución del controlador/handler**

- Se ejecuta la acción del controlador, closure o clase invokable.
- Las dependencias se resuelven automáticamente desde el contenedor.
- Ocurren validación, autorización, lógica de negocio y acceso a datos.

6. **Creación de la respuesta**

- El handler devuelve `Response`, `JsonResponse`, vista, redirección o datos serializables.
- Laravel normaliza la salida a un objeto de respuesta HTTP.

7. **Fase de terminación**

- La respuesta se envía al cliente.
- Se ejecutan middleware terminables y hooks post-respuesta.

Este ciclo de vida ofrece a Laravel un modelo de ejecución predecible y puntos claros de extensión.

</details>

<details>
<summary>5. ¿Qué es el contenedor de servicios de Laravel?</summary>

#### Laravel

El contenedor de servicios de Laravel es un contenedor IoC (Inversión de Control) responsable de crear objetos y gestionar dependencias.

1. **Rol principal**

- Lugar central donde clases/interfaces se vinculan con implementaciones concretas.
- Resuelve automáticamente dependencias de constructor mediante reflexión.

2. **Por qué importa**

- Reduce el cableado manual de objetos.
- Habilita la inversión de dependencias (depender de interfaces, no de clases concretas).
- Mejora la testabilidad al poder intercambiar implementaciones (por ejemplo, fakes/mocks).

3. **Dónde se usa**

- Controladores, middleware, jobs, listeners, comandos y clases de servicio.
- Internals del framework y arquitectura personalizada de la aplicación.

4. **APIs comunes**

- `bind()` para bindings transitorios.
- `singleton()` para una instancia compartida.
- `make()` / `app()` para resolver servicios.

5. **Efecto práctico**

- Constructores más limpios, menos acoplamiento y mejor diseño modular.

En Laravel, el contenedor de servicios es uno de los fundamentos principales para una arquitectura de aplicación escalable.

</details>

<details>
<summary>6. Explica la diferencia entre binding, singleton binding y resolving en el contenedor de servicios.</summary>

#### Laravel

Estos términos describen operaciones distintas dentro del ciclo de vida del contenedor de Laravel.

1. **Binding (`bind`)**

- Registra cómo el contenedor debe construir un tipo.
- Crea una **nueva instancia en cada resolución** (ciclo de vida transitorio).

```php
$this->app->bind(PaymentGateway::class, StripeGateway::class);
```

2. **Singleton binding (`singleton`)**

- Registra un tipo como **instancia compartida**.
- La primera resolución la crea; las siguientes devuelven el mismo objeto.

```php
$this->app->singleton(CacheClient::class, fn () => new CacheClient());
```

3. **Resolving (`make` / auto-injection)**

- Es el acto de pedir al contenedor que proporcione una instancia.
- Puede ocurrir de forma explícita (`app()->make(...)`) o implícita mediante inyección por constructor.

```php
$gateway = app()->make(PaymentGateway::class);
```

4. **Regla práctica**

- Usa `bind` para servicios ligeros/sin estado.
- Usa `singleton` para clientes de infraestructura compartidos/pesados/con estado.
- Prefiere resolución automática mediante inyección de dependencias en clases gestionadas por el framework.

</details>

<details>
<summary>7. ¿Qué es el contextual binding y cuándo lo usarías?</summary>

#### Laravel

El contextual binding permite proporcionar diferentes implementaciones de la misma interfaz según qué clase se esté resolviendo.

1. **Problema que resuelve**

- Múltiples consumidores necesitan el mismo contrato pero con comportamiento concreto diferente.

2. **Escenario de ejemplo**

- `PhotoController` debe usar `S3Filesystem`.
- `ReportController` debe usar `LocalFilesystem`.
- Ambos dependen de `FilesystemInterface`.

3. **API del contenedor**

```php
$this->app->when(PhotoController::class)
    ->needs(FilesystemInterface::class)
    ->give(S3Filesystem::class);

$this->app->when(ReportController::class)
    ->needs(FilesystemInterface::class)
    ->give(LocalFilesystem::class);
```

4. **Cuándo usarlo**

- Integraciones multi-tenant o multi-región.
- Distintos adaptadores para distintos casos de uso.
- Mantener diseño basado en interfaces sin conflictos de binding global.

El contextual binding es útil cuando un único binding global no basta y el comportamiento debe variar según el contexto del consumidor.

</details>

<details>
<summary>8. ¿Qué son los Service Providers y cuál es su propósito?</summary>

#### Laravel

Los Service Providers son el mecanismo central de bootstrap en Laravel para registrar y configurar servicios de la aplicación.

1. **Propósito principal**

- Registrar bindings en el contenedor.
- Configurar servicios de paquete/aplicación durante el arranque.

2. **Qué suele colocarse allí**

- Bindings de interfaz a implementación.
- Registros singleton para servicios de infraestructura.
- Registro de eventos/listeners (o en un provider separado).
- Bootstrap de paquetes y conexión de configuración.

3. **Ejemplos por defecto**

- `AppServiceProvider`
- `RouteServiceProvider`
- Providers de paquetes

4. **Por qué importa**

- Crea una capa de arranque predecible.
- Mantiene la lógica de bootstrap fuera de controladores/modelos.
- Mejora modularidad y mantenibilidad en aplicaciones grandes.

Los Service Providers son, en la práctica, la composition root de una aplicación Laravel.

</details>

<details>
<summary>9. ¿Cuál es la diferencia entre registrar e inicializar (boot) en un service provider?</summary>

#### Laravel

En un Service Provider, `register()` y `boot()` se ejecutan en etapas distintas y tienen responsabilidades diferentes.

1. **`register()`**

- Se usa solo para vincular elementos en el contenedor.
- Debe estar libre de efectos secundarios y no depender de servicios de otros providers ya inicializados.

```php
public function register(): void
{
    $this->app->singleton(PaymentGateway::class, StripeGateway::class);
}
```

2. **`boot()`**

- Se ejecuta después de que todos los providers se registran.
- Se usa para acciones que requieren servicios ya disponibles: rutas, view composers, observers, wiring de eventos, macros.

```php
public function boot(): void
{
    Schema::defaultStringLength(191);
}
```

3. **Distinción práctica**

- `register()` = declarar dependencias.
- `boot()` = ejecutar lógica de integración del framework.

Usar correctamente esta separación evita bugs de orden de arranque y mantiene predecible el comportamiento inicial.

</details>

<details>
<summary>10. ¿Qué son los Contracts de Laravel?</summary>

#### Laravel

Los Contracts de Laravel son interfaces PHP definidas por el framework que describen capacidades de servicios core independientemente de sus implementaciones.

1. **Qué son**

- Interfaces bajo `Illuminate\Contracts\...`.
- Ejemplos: `Cache\Repository`, `Queue\Queue`, `Auth\Guard`, `Mail\Mailer`.

2. **Por qué existen**

- Desacoplan tu código de clases concretas del framework.
- Permiten una inversión de dependencias limpia y testing más sencillo.
- Facilitan reemplazar implementaciones con cambios mínimos de código.

3. **Cómo se usan**

- Tipa un contract en el constructor/método.
- Deja que el contenedor resuelva la implementación actual.

```php
use Illuminate\Contracts\Cache\Repository as Cache;

final class UserService
{
    public function __construct(private Cache $cache) {}
}
```

4. **Beneficio práctico**

- Arquitectura más mantenible y límites más claros.
- Mejores mocks/fakes en tests.
- Migración más simple de detalles de infraestructura.

Los Contracts son un bloque clave para escribir código Laravel compatible con el framework pero agnóstico a implementaciones.

</details>

<details>
<summary>11. ¿Cuál es la diferencia entre un Contract y un Facade?</summary>

#### Laravel

Contracts y Facades están relacionados con servicios de Laravel, pero resuelven problemas diferentes.

1. **Contract**

- Una interfaz PHP (normalmente en `Illuminate\Contracts\...`).
- Define comportamiento/capacidad sin detalles de implementación.
- Se usa para inversión de dependencias y arquitectura limpia.

2. **Facade**

- Un proxy estilo estático a un servicio resuelto desde el contenedor.
- Proporciona una sintaxis concisa para llamar servicios del framework.
- Ejemplo: `Cache::get('key')`, `Log::info('...')`.

3. **Diferencia clave**

- Contract = límite de abstracción (dependencia de diseño).
- Facade = capa de acceso conveniente (API en estilo de llamada).

4. **Impacto en testing**

- Los Contracts son fáciles de mockear mediante DI.
- Las Facades también pueden mockearse (`Facade::shouldReceive()`), pero siguen un estilo de apariencia estática.

5. **Cuándo preferir cada uno**

- Prefiere Contracts en servicios de dominio/aplicación.
- Usa Facades en controladores, glue code pequeño o zonas centradas en framework donde ayuda la brevedad.

En resumen: el Contract define *qué* hace un servicio, la Facade define *qué tan cómodamente* lo llamas.

</details>

<details>
<summary>12. Explica la diferencia entre Facades y funciones helper en Laravel.</summary>

#### Laravel

Tanto las Facades como los helpers ofrecen sintaxis concisa, pero difieren en estructura, descubribilidad y semántica de testing.

1. **Facades**

- Proxy estático basado en clase (`Cache::`, `DB::`, `Bus::`).
- Mapeadas a servicios del contenedor.
- Soportan APIs de mocking/faking de facades.
- Mejor descubribilidad en IDE mediante métodos de clase.

2. **Funciones helper**

- Funciones globales como `app()`, `route()`, `now()`, `config()`, `request()`, `response()`.
- Muy cortas y convenientes en plantillas/controladores.
- No están ligadas a un nombre de clase en el uso.

3. **Diferencias clave**

- Facade: superficie de servicio explícita mediante clase.
- Helper: atajo global ligero.

4. **Testing y arquitectura**

- En código de negocio core, la DI por constructor suele ser más limpia que ambos estilos.
- Para glue code del framework, ambos son válidos; las facades pueden ser más explícitas, los helpers más concisos.

5. **Guía práctica**

- Prefiere DI + contracts en servicios de dominio.
- Usa facades/helpers de forma pragmática en controladores, jobs, vistas y código de integración con el framework.

</details>

<details>
<summary>13. ¿Cómo funciona la Inyección de Dependencias en Laravel?</summary>

#### Laravel

La Inyección de Dependencias (DI) en Laravel está impulsada por el contenedor de servicios, que resuelve automáticamente las dependencias de clase.

1. **Inyección por constructor**

- Defines dependencias con type-hint en el constructor.
- Laravel las resuelve e inyecta al crear la clase.

```php
final class OrderController
{
    public function __construct(private OrderService $service) {}
}
```

2. **Inyección en métodos**

- Funciona en acciones de controladores, handlers de jobs, listeners, comandos, etc.
- Los parámetros con type-hint pueden resolverse automáticamente.

```php
public function store(StoreOrderRequest $request, OrderService $service): JsonResponse
{
    // ...
}
```

3. **Inyección de interfaces**

- Si inyectas una interfaz, vincúlala a una clase concreta en un provider.

```php
$this->app->bind(PaymentGateway::class, StripeGateway::class);
```

4. **Por qué DI importa**

- Bajo acoplamiento.
- Testing fácil con mocks/fakes.
- Dependencias claras y mejor mantenibilidad.

En Laravel, DI es la forma por defecto de conectar servicios de aplicación de manera limpia.

</details>

<details>
<summary>14. ¿Cómo usa Laravel IoC (Inversión de Control)?</summary>

#### Laravel

Laravel aplica IoC delegando la creación de objetos y el cableado de dependencias al contenedor de servicios en lugar de hardcodear dependencias dentro de las clases.

1. **Tradicional (sin IoC)**

- La clase instancia sus propias dependencias (`new StripeGateway()`), generando acoplamiento fuerte.

2. **Con IoC en Laravel**

- Las clases declaran las abstracciones requeridas (interfaces/tipos).
- El contenedor proporciona implementaciones concretas.

3. **Dónde aparece IoC**

- Controladores, middleware, jobs, eventos/listeners, comandos, policies y servicios personalizados.
- Los internals del framework también dependen del mismo mecanismo.

4. **Beneficios**

- Implementaciones intercambiables (por ejemplo, Stripe vs PayPal).
- Mejor testing unitario y arquitectura modular.
- Configuración centralizada del grafo de objetos en providers.

IoC en Laravel es la base arquitectónica detrás de DI, contracts y testabilidad.

</details>

<details>
<summary>15. ¿Qué son los middleware en Laravel?</summary>

#### Laravel

Los middleware son clases que inspeccionan, filtran o transforman solicitudes/respuestas HTTP mientras atraviesan el pipeline de la solicitud.

1. **Propósito**

- Ejecutar preocupaciones transversales antes/después de la lógica del controlador.

2. **Casos de uso comunes**

- Comprobaciones de autenticación/autorización.
- Rate limiting.
- Protección CSRF.
- Logging de solicitudes y headers de seguridad.
- Localización y configuración de tenant/contexto.

3. **Modelo de ejecución**

- La solicitud entra en el stack de middleware.
- Cada middleware decide continuar (`$next($request)`) o detenerse (devolver respuesta/redirección/error).
- La respuesta también puede modificarse en el camino de regreso.

4. **Tipos**

- Middleware global (para todas las solicitudes).
- Middleware de ruta (asignado a rutas/grupos específicos).

Los middleware mantienen los controladores enfocados al mover preocupaciones HTTP reutilizables a capas dedicadas del pipeline.

</details>

<details>
<summary>16. ¿Cómo registras y asignas middleware?</summary>

#### Laravel

En Laravel moderno, el middleware normalmente se configura en la configuración de bootstrap de la aplicación y se asigna por alias, grupo o clase directa.

1. **Registrar aliases/grupos de middleware**

- Define aliases y la composición de grupos en la configuración de middleware del bootstrap de la aplicación.
- Los aliases típicos incluyen `auth`, `verified`, `throttle`, etc.

2. **Middleware global**

- Se agrega al stack global para que se ejecute en cada solicitud.

3. **Asignación a rutas**

- Por ruta:

```php
Route::get('/profile', ProfileController::class)
    ->middleware('auth');
```

- Por grupo:

```php
Route::middleware(['auth', 'verified'])->group(function () {
    Route::get('/dashboard', DashboardController::class);
});
```

4. **Por nombre de clase**

- También puedes adjuntar la clase de middleware directamente en lugar del alias cuando sea necesario.

En la práctica: usa aliases para mejorar legibilidad y consistencia en toda la base de código.

</details>

<details>
<summary>17. ¿Cómo funciona el middleware con parámetros?</summary>

#### Laravel

El middleware en Laravel puede aceptar parámetros desde las definiciones de rutas, lo que permite un comportamiento configurable sin duplicar clases de middleware.

1. **Uso en ruta**

```php
Route::get('/admin', AdminController::class)
    ->middleware('role:admin');
```

2. **Firma del middleware**

```php
public function handle(Request $request, Closure $next, string $role): Response
{
    if (! $request->user() || ! $request->user()->hasRole($role)) {
        abort(403);
    }

    return $next($request);
}
```

3. **Múltiples parámetros**

- Se pasan separados por comas: `'throttle:60,1'`, `'ability:update,post'`.

4. **Cuándo es útil**

- Reglas de autorización por rol/permiso.
- Limitación configurable por endpoint.
- Validaciones reutilizables con pequeñas variaciones.

Los parámetros convierten un middleware en una herramienta reutilizable y flexible para control de acceso y políticas de solicitud.

</details>

<details>
<summary>18. ¿Qué son los grupos de rutas, los prefijos y los grupos de middleware?</summary>

#### Laravel

La agrupación de rutas ayuda a organizar rutas y aplicar una configuración compartida una sola vez.

1. **Grupos de rutas**

- Combinan rutas bajo atributos comunes (`middleware`, `prefix`, `name`, `namespace`, etc.).

2. **Prefijos**

- Añaden un prefijo URI a todas las rutas del grupo.

```php
Route::prefix('api/v1')->group(function () {
    Route::get('/users', [UserController::class, 'index']);
});
```

3. **Prefijos de nombre**

- Añaden un prefijo común al nombre de ruta.

```php
Route::name('admin.')->group(function () {
    Route::get('/dashboard', [AdminController::class, 'dashboard'])->name('dashboard');
});
// Nombre de ruta: admin.dashboard
```

4. **Grupos de middleware**

- Un conjunto nombrado de middleware (por ejemplo `web`, `api`) que se puede aplicar en conjunto.
- Reducen repetición y estandarizan el comportamiento en secciones de rutas.

5. **Por qué importa**

- Archivos de rutas más limpios.
- Reglas consistentes de seguridad y manejo de solicitudes.
- Mantenimiento más fácil a medida que crece la aplicación.

</details>

<details>
<summary>19. ¿Qué es el route model binding?</summary>

#### Laravel

El route model binding resuelve automáticamente parámetros de ruta en instancias de modelos Eloquent.

1. **Qué hace**

- Convierte un segmento de ruta como `{user}` en un objeto del modelo `User`.
- Si no se encuentra, Laravel devuelve `404` automáticamente.

2. **Ejemplo**

```php
Route::get('/users/{user}', [UserController::class, 'show']);

public function show(User $user): View
{
    return view('users.show', compact('user'));
}
```

3. **Beneficios**

- Elimina boilerplate repetitivo de `findOrFail()`.
- Mejora legibilidad y seguridad de tipos.
- Ofrece control centralizado sobre el comportamiento de búsqueda.

El route model binding simplifica controladores y hace más explícita la intención de las rutas.

</details>

<details>
<summary>20. Explica el route model binding implícito vs explícito.</summary>

#### Laravel

Ambos enfoques resuelven parámetros de ruta a modelos, pero difieren en el estilo de configuración.

1. **Binding implícito**

- Laravel infiere el binding por nombre de parámetro + type-hint.
- Configuración mínima.

```php
Route::get('/posts/{post}', fn (Post $post) => $post);
```

2. **Binding explícito**

- Defines manualmente cómo un parámetro se mapea a un modelo.
- Útil para lógica personalizada o resolución no estándar.

```php
Route::bind('post', function (string $value) {
    return Post::where('slug', $value)->firstOrFail();
});
```

3. **Cuándo elegir cada uno**

- Usa binding implícito por defecto (limpio y convencional).
- Usa binding explícito para reglas especiales de búsqueda, transformaciones personalizadas o casos límite.

4. **Personalización relacionada**

- En muchos casos, sobrescribir `getRouteKeyName()` en el modelo (por ejemplo, slug) es suficiente sin binding explícito completo.

Implícito = binding automático por convención. Explícito = comportamiento de binding controlado manualmente.

</details>

<details>
<summary>21. ¿Qué es el rate limiting en Laravel y cómo funciona?</summary>

#### Laravel

El rate limiting controla cuántas solicitudes puede hacer un cliente en una ventana de tiempo para proteger APIs contra abuso y sobrecarga.

1. **Qué hace**

- Limita la frecuencia de solicitudes por clave (ID de usuario, IP, token o identificador personalizado).
- Devuelve `429 Too Many Requests` cuando se supera el límite.

2. **Cómo lo implementa Laravel**

- Usa limitadores nombrados definidos con `RateLimiter::for(...)`.
- Aplica el limitador mediante middleware (comúnmente `throttle`).
- Guarda contadores usando backend de caché (Redis/Memcached/caché de base de datos según configuración).

3. **Ejemplo básico**

```php
RateLimiter::for('api', function (Request $request) {
    return Limit::perMinute(60)->by($request->user()?->id ?: $request->ip());
});
```

4. **Dónde aplicarlo**

- Endpoints públicos de API.
- Login, OTP, restablecimiento de contraseña y otros endpoints sensibles.
- Operaciones costosas (búsqueda, exportación, generación de reportes).

El rate limiting es una capa de seguridad y estabilidad esencial para aplicaciones Laravel orientadas a producción.

</details>

<details>
<summary>22. ¿Qué son los controladores invocables?</summary>

#### Laravel

Los controladores invocables son clases de controlador con un único método `__invoke()`, diseñadas para una acción específica.

1. **Estructura**

```php
final class PublishPostController
{
    public function __invoke(Post $post): JsonResponse
    {
        // ...
    }
}
```

2. **Routing**

```php
Route::post('/posts/{post}/publish', PublishPostController::class);
```

3. **Beneficios**

- Responsabilidad muy enfocada.
- Mapeo ruta-acción más limpio.
- Funciona bien con arquitectura orientada a acciones.

4. **Cuándo es útil**

- Endpoints con propósito único y claro.
- Estilo CQRS/basado en acciones.
- Codebases grandes donde clases más pequeñas mejoran la navegación.

Los controladores invocables son una forma práctica de mantener la capa HTTP explícita y modular.

</details>

<details>
<summary>23. ¿Qué son los Single Action Controllers?</summary>

#### Laravel

Los Single Action Controllers son el mismo concepto que los controladores invocables: una clase de controlador maneja una acción mediante `__invoke()`.

1. **Idea central**

- Una clase = un caso de uso.
- Sin múltiples métodos como `index/store/update` en el mismo controlador.

2. **Por qué los equipos los usan**

- Mejor separación de responsabilidades.
- Testing más sencillo por endpoint.
- Menos conflictos de merge en equipos grandes.

3. **Casos de uso de ejemplo**

- `ApproveInvoiceController`
- `SendWelcomeEmailController`
- `GenerateReportController`

4. **Tradeoff**

- Más archivos/clases.
- Pero normalmente mejor mantenibilidad a largo plazo en proyectos medianos/grandes.

Los Single Action Controllers son, esencialmente, una elección de estilo arquitectónico que prioriza claridad y escalabilidad.

</details>

<details>
<summary>24. ¿Cuál es la diferencia entre Resource Controllers y API Resource Controllers?</summary>

#### Laravel

La diferencia es principalmente sobre las acciones generadas y el estilo de respuesta esperado.

1. **Resource Controller (`Route::resource`)**

- Genera rutas CRUD web completas:
  `index`, `create`, `store`, `show`, `edit`, `update`, `destroy`.
- Incluye rutas `create` y `edit`, típicamente para formularios/vistas HTML.

2. **API Resource Controller (`Route::apiResource`)**

- Genera rutas CRUD enfocadas en API:
  `index`, `store`, `show`, `update`, `destroy`.
- Excluye `create` y `edit` (páginas de formularios UI no necesarias para APIs).

3. **Uso típico**

- `resource`: aplicaciones web renderizadas en servidor.
- `apiResource`: APIs JSON, backends móviles, backends para SPA.

4. **Concepto relacionado**

- Las respuestas API suelen formatearse con clases `JsonResource` para contratos de salida consistentes.

</details>

<details>
<summary>25. ¿Cómo creas comandos personalizados de Artisan?</summary>

#### Laravel

Los comandos personalizados de Artisan son clases CLI usadas para automatización, mantenimiento, importaciones y flujos operativos.

1. **Generar la clase del comando**

```bash
php artisan make:command SyncInvoicesCommand
```

2. **Definir signature y descripción**

```php
protected $signature = 'billing:sync {--dry-run}';
protected $description = 'Sync invoices from billing provider';
```

3. **Implementar la lógica en `handle()`**

```php
public function handle(): int
{
    // command logic
    return self::SUCCESS;
}
```

4. **Usar DI en el comando**

- Inyecta servicios vía constructor o resolución a nivel de método.

5. **Ejecutar comando**

```bash
php artisan billing:sync --dry-run
```

6. **Programación opcional**

- Regístralo en el scheduler para ejecutarlo automáticamente con cron.

Los comandos personalizados son ideales para operaciones backend repetibles y automatización compatible con DevOps.

</details>

<details>
<summary>26. ¿Qué son los macros y cuándo son útiles?</summary>

#### Laravel

Los macros te permiten agregar métodos personalizados a clases del framework en runtime (clases macroables) sin modificar el código fuente del framework.

1. **Objetivos macroables comunes**

- `Collection`, `Str`, `ResponseFactory`, `Route`, etc.

2. **Ejemplo**

```php
use Illuminate\Support\Collection;

Collection::macro('toKeyValue', function (string $key, string $value) {
    return $this->mapWithKeys(fn ($item) => [$item[$key] => $item[$value]]);
});
```

3. **Cuándo son útiles**

- Lógica utilitaria repetida en toda la base de código.
- Helpers de colección/string específicos del dominio.
- APIs expresivas más limpias para transformaciones comunes.

4. **Buenas prácticas**

- Registra macros en un service provider.
- Mantén nombres claros para evitar colisiones.
- No abusar; para comportamiento complejo, prefiere clases normales.

Los macros son mejores para extensiones pequeñas y reutilizables del framework con alta frecuencia de uso.

</details>

<details>
<summary>27. ¿Qué son las Actions en la arquitectura Laravel y cuándo se usan?</summary>

#### Laravel

Las Actions son clases enfocadas que encapsulan un único caso de uso de negocio (operación de aplicación).

1. **Qué es una Action**

- Una clase como `CreateOrderAction`, `PublishPostAction`, `RefundPaymentAction`.
- Normalmente expone un solo método (`handle()` o `execute()`).

2. **Por qué usar Actions**

- Saca la lógica de negocio de controladores/modelos.
- Reutilizables desde controladores HTTP, jobs, comandos de consola y listeners.
- Testing unitario más fácil con entrada/salida claras.

3. **Estructura típica**

```php
final class CreateOrderAction
{
    public function __construct(private OrderRepository $orders) {}

    public function handle(CreateOrderData $data): Order
    {
        // business logic
    }
}
```

4. **Cuándo usarlas**

- Casos de uso no triviales con reglas de orquestación.
- Lógica reutilizada en múltiples puntos de entrada.
- Equipos que adoptan arquitectura de servicios/actions o estilo CQRS.

Las Actions mejoran la modularidad y hacen explícitos los flujos de negocio.

</details>

<details>
<summary>28. Explica el patrón Repository y sus beneficios.</summary>

#### Laravel

El patrón Repository abstrae el acceso a datos detrás de interfaces para que la lógica de negocio no quede fuertemente acoplada a detalles de ORM/consultas.

1. **Idea central**

- Definir un contrato (por ejemplo, `OrderRepository`).
- Proporcionar una implementación (por ejemplo, `EloquentOrderRepository`).
- Inyectar el repositorio en servicios/actions.

2. **Beneficios**

- Separación clara entre lógica de dominio/aplicación y persistencia.
- Testing más fácil con repositorios fake/en memoria.
- Lógica compleja de consultas y estrategias de caché centralizadas.
- Cambios futuros de fuente de datos más sencillos.

3. **Tradeoffs**

- Capa extra de abstracción y más boilerplate.
- No siempre necesario para apps simples centradas en CRUD.

4. **Guía pragmática**

- Usa repositorios cuando el acceso a datos sea complejo o compartido.
- Evita sobreingeniería en módulos simples.

El patrón Repository aporta valor cuando reduce acoplamiento y complejidad, no cuando solo añade indirección.

</details>

<details>
<summary>29. ¿Qué son los Traits en PHP y cómo se usan en Laravel?</summary>

#### Laravel

Los Traits son unidades del lenguaje PHP para reutilización horizontal de código entre clases sin herencia.

1. **Qué proporcionan los traits**

- Métodos/propiedades reutilizables incluidos mediante `use`.
- Comportamiento compartido para clases no relacionadas.

2. **Ejemplos de uso en Laravel**

- Traits del framework como `SoftDeletes`, `HasFactory`, `Notifiable`, `AuthorizesRequests`, `DispatchesJobs`, `ValidatesRequests`.

3. **Ejemplo en modelo**

```php
use Illuminate\Database\Eloquent\SoftDeletes;

class Post extends Model
{
    use SoftDeletes;
}
```

4. **Buenas prácticas**

- Mantén los traits pequeños y cohesivos.
- Usa traits para reutilizar comportamiento, no para ocultar responsabilidades sobredimensionadas en clases.
- Prefiere composición/servicios para lógica de dominio compleja.

Los Traits son un mecanismo práctico de reutilización, muy usado en los internals de Laravel y en código de aplicación.

</details>

<details>
<summary>30. ¿Cuáles son las diferencias entre Laravel y Lumen, y sigue siendo relevante Lumen en 2026?</summary>

#### Laravel

Laravel y Lumen comparten raíces, pero apuntan a distintos compromisos de desarrollo.

1. **Diferencias principales**

- **Laravel**: framework completo (ecosistema amplio, paquetes oficiales, convenciones extensas, soporte de integración amplio).
- **Lumen**: variante micro-framework enfocada en una huella mínima y configuraciones API más simples.

2. **Arquitectura y ecosistema**

- Laravel tiene mayor compatibilidad con paquetes oficiales y tooling de desarrollo más completo.
- Lumen es intencionalmente más liviano y no busca compatibilidad total con toda la superficie de paquetes de Laravel.

3. **Contexto de rendimiento**

- Históricamente Lumen se elegía para APIs ligeras.
- En versiones modernas, el rendimiento de Laravel mejoró significativamente, reduciendo la brecha práctica en muchas cargas.

4. **¿Es relevante Lumen en 2026?**

- **Para proyectos nuevos:** por lo general **no recomendado** por la guía del ecosistema Laravel.
- **Para sistemas existentes:** sigue siendo relevante si ya está en producción y estable.
- **Elección por defecto en 2026:** Laravel (con optimización adecuada) para la mayoría de nuevos backends API y web.

5. **Regla práctica de decisión**

- Inicia productos nuevos con Laravel.
- Mantén Lumen solo al sostener servicios legacy con razones operativas claras.

</details>

<details>
<summary>31. ¿Qué es Eloquent ORM?</summary>

#### Laravel

Eloquent ORM es la implementación Active Record de Laravel para trabajar con bases de datos mediante objetos PHP en lugar de SQL crudo.

1. **Qué ofrece**

- Mapeo modelo-tabla.
- Integración con query builder.
- Gestión de relaciones.
- Casting de atributos, accessors/mutators, scopes y eventos.

2. **Por qué los equipos lo usan**

- Desarrollo más rápido con sintaxis expresiva.
- Código de dominio más limpio para flujos CRUD comunes.
- Convenciones integradas que reducen boilerplate.

3. **Ejemplo**

```php
$users = User::query()
    ->where('is_active', true)
    ->latest()
    ->take(10)
    ->get();
```

4. **Nota importante**

- Eloquent es excelente para la mayoría de casos de uso de aplicación.
- Para consultas muy especializadas/de reporting, SQL crudo o query builder puede seguir siendo mejor.

Eloquent es la capa de acceso a datos por defecto en aplicaciones Laravel.

</details>

<details>
<summary>32. ¿Qué son los modelos Eloquent?</summary>

#### Laravel

Los modelos Eloquent son clases PHP que representan tablas de base de datos y encapsulan el comportamiento de los datos.

1. **Rol principal**

- Cada modelo normalmente mapea a una tabla.
- Las instancias del modelo representan filas individuales.

2. **Qué suelen contener los modelos**

- Atributos fillable/guarded.
- Casts y manejo de fechas.
- Relaciones.
- Scopes y métodos específicos del dominio.

3. **Ejemplo básico**

```php
final class Post extends Model
{
    protected $fillable = ['title', 'body', 'published_at'];

    protected function casts(): array
    {
        return [
            'published_at' => 'datetime',
        ];
    }
}
```

4. **Por qué importa**

- Centraliza reglas de datos cerca de la entidad.
- Mantiene lógica de persistencia expresiva y reutilizable.

Los modelos Eloquent son una piedra angular de la capa de dominio/persistencia en aplicaciones Laravel.

</details>

<details>
<summary>33. Explica las relaciones one-to-one, one-to-many, many-to-many y polimórficas.</summary>

#### Laravel

Las relaciones de Eloquent definen cómo los modelos se conectan en el modelo de datos.

1. **One-to-one (`hasOne` / `belongsTo`)**

- Un registro se relaciona con exactamente un registro.
- Ejemplo: `User` tiene un `Profile`.

2. **One-to-many (`hasMany` / `belongsTo`)**

- Un padre tiene múltiples hijos.
- Ejemplo: `Post` tiene muchos `Comment`.

3. **Many-to-many (`belongsToMany`)**

- Ambos lados pueden tener muchos registros relacionados.
- Requiere tabla pivote.
- Ejemplo: `User` pertenece a muchos `Role`.

4. **Polimórfica**

- Un modelo puede pertenecer a más de un tipo de padre mediante una interfaz compartida.
- Ejemplo: `Comment` puede pertenecer a `Post` o `Video`.

5. **Por qué importa**

- Las relaciones permiten expresar claramente la estructura del dominio.
- Eloquent puede cargar datos relacionados, restringir consultas y simplificar joins.

Elegir el tipo de relación correcto es clave para un diseño de esquema limpio y consultas eficientes.

</details>

<details>
<summary>34. ¿Qué son las relaciones polimórficas y cuándo las usarías?</summary>

#### Laravel

Las relaciones polimórficas permiten que un modelo se relacione con múltiples tipos de modelos usando un par de columnas (normalmente `*_type` y `*_id`).

1. **Cómo funciona**

- La tabla hija guarda el tipo del padre + el ID del padre.
- Un modelo hijo puede apuntar a diferentes modelos padre.

2. **Ejemplos comunes**

- `Comment` en `Post`, `Video`, `Product`.
- `Image` adjunta a `User`, `Team`, `Article`.
- `Activity` dirigida a múltiples tipos de entidad.

3. **Métodos de relación en Laravel**

- `morphTo` en el hijo.
- `morphMany` / `morphOne` en el padre.
- `morphToMany` / `morphedByMany` para many-to-many polimórfico.

4. **Cuándo usarla**

- Cuando el comportamiento se comparte entre entidades padre heterogéneas.
- Cuando quieres una tabla hija reutilizable en lugar de muchas tablas paralelas.

5. **Tradeoff**

- Esquema más flexible, pero puede aumentar la complejidad de consultas y requerir indexación cuidadosa.

Usa relaciones polimórficas cuando reducen duplicación y encajan de forma natural con el modelo de dominio.

</details>

<details>
<summary>35. ¿Qué es eager loading?</summary>

#### Laravel

Eager loading significa cargar modelos relacionados por adelantado como parte del flujo de consulta principal, en lugar de cargar cada relación después por elemento.

1. **Cómo hacerlo**

```php
$posts = Post::with(['author', 'comments'])->latest()->get();
```

2. **Por qué importa**

- Reduce el número total de consultas.
- Evita problemas de consultas N+1.
- Mejora el tiempo de respuesta y la eficiencia de la base de datos.

3. **Variantes útiles**

- Eager loading anidado: `with('comments.user')`.
- Eager loading con restricciones mediante closures.
- Eager loads por defecto vía `$with` del modelo cuando siempre se necesitan.

El eager loading es una práctica de optimización central para aplicaciones basadas en Eloquent.

</details>

<details>
<summary>36. ¿Qué es el problema de consultas N+1 y cómo se soluciona?</summary>

#### Laravel

N+1 ocurre cuando ejecutas 1 consulta para una lista y luego una consulta adicional por cada elemento para datos relacionados.

1. **Escenario típico**

- Consultas 100 posts.
- Accedes a `$post->author` dentro de un bucle.
- Resultado: 101 consultas (1 + 100).

2. **Por qué es malo**

- Gran cantidad de consultas.
- Mayor latencia y carga de base de datos.
- Escalabilidad deficiente bajo tráfico.

3. **Cómo resolverlo en Laravel**

- Usa eager loading con `with()`.

```php
$posts = Post::with('author')->get();
```

- Usa `load()` / `loadMissing()` cuando ya tienes colecciones de modelos.
- Usa herramientas de profiling de consultas (Telescope/Debugbar/logging) para detectar puntos críticos.

4. **Buena práctica**

- Anticipa las relaciones necesarias en el momento de la consulta.
- Revisa bucles sobre modelos para detectar lazy loads ocultos.

Resolver N+1 es una de las mejoras de rendimiento de Eloquent con mayor impacto.

</details>

<details>
<summary>37. ¿Qué es lazy eager loading?</summary>

#### Laravel

Lazy eager loading carga relaciones después de que los modelos ya fueron recuperados, pero aún en bloque y no por modelo individual.

1. **Cuándo se usa**

- Primero obtuviste los modelos.
- Después decides qué relaciones necesitas.

2. **Métodos**

- `load()` carga las relaciones especificadas.
- `loadMissing()` carga solo las relaciones que aún no están cargadas.

```php
$posts = Post::latest()->take(50)->get();
$posts->load('author', 'comments');
```

3. **Por qué ayuda**

- Evita N+1 manteniendo un flujo de control flexible.
- Útil en lógica condicional o servicios por capas.

4. **Diferencia frente a eager loading**

- Eager loading: `with()` antes de ejecutar la consulta.
- Lazy eager loading: `load()` después de ejecutar la consulta.

Lazy eager loading es un punto medio práctico entre flexibilidad y rendimiento.

</details>

<details>
<summary>38. ¿Qué son los global scopes y local scopes?</summary>

#### Laravel

Los scopes son restricciones de consulta reutilizables en Eloquent.

1. **Global scopes**

- Se aplican automáticamente a todas las consultas de un modelo.
- Buenos para restricciones transversales (por ejemplo, aislamiento por tenant, comportamiento de soft delete, registros solo activos).

2. **Local scopes**

- Se llaman explícitamente en las consultas cuando se necesitan.
- Definen filtros reutilizables y enfocados.

```php
public function scopePublished(Builder $query): Builder
{
    return $query->whereNotNull('published_at');
}

$posts = Post::published()->get();
```

3. **Cuándo elegir**

- Global scope: regla de negocio por defecto que debe aplicarse casi siempre.
- Local scope: filtro opcional para casos de uso específicos.

4. **Precaución**

- El uso excesivo de global scopes puede ocultar datos inesperadamente; documéntalos con claridad.

Los scopes mejoran la consistencia y reducen condiciones repetidas en consultas.

</details>

<details>
<summary>39. ¿Qué son los query scopes?</summary>

#### Laravel

Los query scopes son métodos del modelo que encapsulan restricciones de consulta reutilizables para lograr consultas más limpias y composables.

1. **Patrón de local query scope**

- El nombre del método empieza con `scope`.
- Se invoca sin el prefijo.

```php
public function scopeActive(Builder $query): Builder
{
    return $query->where('is_active', true);
}

public function scopeRecent(Builder $query): Builder
{
    return $query->latest('created_at');
}

$users = User::active()->recent()->get();
```

2. **Beneficios**

- Filtros reutilizables.
- Cadenas de consulta más legibles.
- Lógica de restricciones centralizada.

3. **Uso práctico**

- Filtros de estado (`active`, `published`, `archived`).
- Ventanas de fechas (`recent`, `betweenDates`).
- Restricciones de negocio (`visibleTo`, `forTenant`).

Los query scopes son una herramienta clave para mantener consultas Eloquent expresivas y mantenibles.

</details>

<details>
<summary>40. ¿Qué son los accessors y mutators?</summary>

#### Laravel

Los accessors y mutators definen cómo se transforman los atributos del modelo al leer y escribir.

1. **Accessor**

- Transforma un valor cuando se recupera del modelo.

2. **Mutator**

- Transforma un valor antes de guardarlo en el modelo.

3. **Estilo moderno (`Attribute`)**

```php
use Illuminate\Database\Eloquent\Casts\Attribute;

protected function title(): Attribute
{
    return Attribute::make(
        get: fn (string $value) => ucfirst($value),
        set: fn (string $value) => strtolower(trim($value)),
    );
}
```

4. **Casos de uso típicos**

- Normalizar entrada (trim/formato de mayúsculas-minúsculas).
- Presentar valores calculados/formateados.
- Manejar transformaciones de cifrado/descifrado.

5. **Diferencia frente a casts**

- Los casts manejan conversión de tipos comunes.
- Accessors/mutators manejan transformaciones personalizadas específicas del dominio.

Ayudan a mantener la lógica de transformación de atributos centralizada y consistente.

</details>

<details>
<summary>41. ¿Qué son los casts en Eloquent?</summary>

#### Laravel

Los casts definen cómo Eloquent convierte atributos del modelo entre valores crudos de base de datos y tipos PHP.

1. **Qué hacen los casts**

- Convierten valores automáticamente al leer/escribir.
- Mantienen el manejo de atributos consistente y type-safe.

2. **Tipos de cast comunes**

- `integer`, `float`, `decimal:2`, `boolean`
- `datetime`, `immutable_datetime`
- `array`, `json`, `object`, `collection`
- `encrypted`, `hashed`

3. **Ejemplo**

```php
protected function casts(): array
{
    return [
        'is_active' => 'boolean',
        'meta' => 'array',
        'published_at' => 'datetime',
    ];
}
```

4. **Por qué importa**

- Menos parsing manual en toda la app.
- Comportamiento predecible de atributos.
- Código de dominio más limpio.

Los casts son una forma central de mantener tipos de datos consistentes en modelos Eloquent.

</details>

<details>
<summary>42. ¿Qué son los objetos Attribute en Laravel moderno?</summary>

#### Laravel

Los objetos `Attribute` son la forma moderna de definir accessors y mutators en un solo lugar para un campo del modelo.

1. **Idea central**

- Un método devuelve `Attribute::make(get: ..., set: ...)`.
- Encapsula claramente las transformaciones de lectura/escritura.

2. **Ejemplo**

```php
use Illuminate\Database\Eloquent\Casts\Attribute;

protected function name(): Attribute
{
    return Attribute::make(
        get: fn (string $value) => ucwords($value),
        set: fn (string $value) => strtolower(trim($value)),
    );
}
```

3. **Beneficios**

- Más limpio que los métodos legacy `getXxxAttribute` / `setXxxAttribute`.
- Agrupa comportamiento getter/setter en un solo método.
- Más fácil de leer, testear y mantener.

4. **Cuándo usarlo**

- Formateo personalizado, normalización, lógica de cifrado o mapeo a value objects en atributos específicos.

Los objetos Attribute son el patrón moderno preferido para accessors/mutators en versiones actuales de Laravel.

</details>

<details>
<summary>43. ¿Qué son las Eloquent Collections?</summary>

#### Laravel

Las Eloquent Collections son objetos de colección especializados devueltos por consultas Eloquent, que extienden la `Collection` base de Laravel con comportamiento consciente de modelos.

1. **Qué son**

- Devueltas por métodos como `get()` y cargas de relaciones.
- Contienen instancias de modelos, no arrays planos.

2. **Capacidades extra**

- Heredan una API rica de colecciones (`map`, `filter`, `groupBy`, `pluck`, etc.).
- Agregan helpers específicos de Eloquent como `load()`, `loadMissing()`, `modelKeys()`, `fresh()`.

3. **Ejemplo**

```php
$users = User::where('is_active', true)->get(); // Eloquent Collection
$users->load('roles');
```

4. **Por qué importan**

- Ofrecen manipulación de datos en memoria expresiva.
- Mantienen semántica orientada a modelos en operaciones en lote.

Las Eloquent Collections hacen más fluido el trabajo con conjuntos de modelos en Laravel.

</details>

<details>
<summary>44. ¿Cuál es la diferencia entre arrays y collections?</summary>

#### Laravel

Los arrays son estructuras de datos nativas de PHP, mientras que las Collections son envoltorios de objetos con API fluida para transformaciones.

1. **Arrays**

- Estructura nativa rápida.
- Acceso mediante sintaxis del lenguaje.
- Menos helpers de transformación de alto nivel por defecto.

2. **Collections**

- Objeto `Illuminate\Support\Collection`.
- Métodos encadenables: `map`, `filter`, `reduce`, `sortBy`, `groupBy`, etc.
- Más expresivas y legibles para pipelines de datos complejos.

3. **Ejemplo**

```php
$names = collect($users)
    ->filter(fn ($u) => $u->is_active)
    ->pluck('name')
    ->values();
```

4. **Cuándo usar cada una**

- Usa arrays para operaciones simples y de bajo nivel.
- Usa collections para legibilidad y transformaciones componibles.

Las collections intercambian una pequeña sobrecarga por una ergonomía mucho mejor en código de aplicación.

</details>

<details>
<summary>45. ¿Qué son las Lazy Collections?</summary>

#### Laravel

Las Lazy Collections procesan elementos como un stream (basado en generadores) en lugar de cargar todos los elementos en memoria al mismo tiempo.

1. **Propiedad central**

- Iteración eficiente en memoria sobre datasets muy grandes.

2. **Cómo funcionan**

- Los elementos se generan y procesan uno por uno.
- La cadena de transformaciones se ejecuta de forma perezosa durante la iteración.

3. **Fuentes típicas**

- Consultas con `lazy()`.
- `cursor()` de Eloquent/query builder.
- Generadores personalizados envueltos en `LazyCollection`.

4. **Cuándo usarlas**

- Scripts de migración de datos.
- Exportaciones/importaciones grandes.
- Jobs en segundo plano sobre millones de filas.

5. **Tradeoff**

- Algunas operaciones de colección que requieren materialización completa son menos adecuadas.

Las Lazy Collections son ideales cuando la seguridad de memoria importa más que la conveniencia de acceso aleatorio.

</details>

<details>
<summary>46. ¿Cuál es el propósito del método cursor()?</summary>

#### Laravel

`cursor()` devuelve un iterable perezoso de resultados, permitiendo recorrer registros uno a uno con bajo uso de memoria.

1. **Por qué usarlo**

- Evita cargar todo el conjunto de resultados en RAM.
- Procesa tablas grandes eficientemente.

2. **Ejemplo**

```php
foreach (User::where('is_active', true)->cursor() as $user) {
    // process user
}
```

3. **Características**

- Iteración basada en generador.
- Bueno para pipelines de lectura/procesamiento.
- Funciona bien con colas y jobs de larga duración.

4. **Cuándo no es ideal**

- Si necesitas acceso aleatorio a todos los resultados a la vez.
- Si necesitas materializar grafos completos con eager loading pesado para todos los registros.

`cursor()` es una herramienta clave para procesamiento escalable registro por registro.

</details>

<details>
<summary>47. ¿Qué es chunking y cuándo debes usar chunk() o lazy()?</summary>

#### Laravel

Chunking significa procesar resultados de consulta en lotes pequeños en lugar de cargar todo de una vez.

1. **`chunk()`**

- Obtiene registros en lotes de tamaño fijo y ejecuta un callback por cada lote.

```php
User::query()->chunk(1000, function ($users) {
    foreach ($users as $user) {
        // process
    }
});
```

2. **`lazy()`**

- Internamente usa chunking, pero se expone como un único stream perezoso.
- Más componible para código estilo pipeline.

```php
User::query()->lazy(1000)->each(function (User $user) {
    // process
});
```

3. **Cuándo elegir**

- Usa `chunk()` para operaciones explícitas por lote.
- Usa `lazy()` para transformaciones de streaming fluidas.

4. **Nota importante**

- Al actualizar filas durante la iteración, prefiere variantes basadas en ID (`chunkById`, `lazyById`) para evitar omitir/duplicar filas.

El chunking es esencial para procesar datasets grandes con uso de memoria controlado.

</details>

<details>
<summary>48. Explica el query builder en Laravel.</summary>

#### Laravel

El Query Builder de Laravel es una API fluida para construir consultas SQL que funciona por encima de PDO y por debajo de los modelos Eloquent.

1. **Qué es**

- Interfaz de consulta agnóstica de base de datos vía `DB::table(...)`.
- Soporta select, joins, cláusulas where, agrupación, ordenamiento, paginación, inserts/updates/deletes.

2. **Ejemplo**

```php
$users = DB::table('users')
    ->select('id', 'name', 'email')
    ->where('is_active', true)
    ->orderByDesc('created_at')
    ->limit(20)
    ->get();
```

3. **Por qué usarlo**

- Más control sobre SQL que los patrones ORM de alto nivel.
- Excelente para consultas de reporting y joins complejos.
- Aún soporta bindings y manejo de parámetros seguro contra SQL injection.

4. **Eloquent vs builder**

- Eloquent: centrado en modelos, funciones de dominio ricas.
- Query Builder: centrado en tablas/consultas, más de bajo nivel y a menudo más ligero.

Query Builder es la capa fluida central para trabajo SQL preciso en Laravel.

</details>

<details>
<summary>49. ¿Cómo mostrar consultas SQL crudas en Laravel?</summary>

#### Laravel

Puedes inspeccionar SQL y bindings de varias formas según la profundidad de depuración.

1. **`toSql()` + `getBindings()`**

```php
$query = User::where('email', 'like', '%@example.com%');

$sql = $query->toSql();
$bindings = $query->getBindings();
```

2. **`toRawSql()` (Laravel moderno)**

- Devuelve SQL con bindings interpolados para facilitar la lectura.

```php
$sql = User::where('id', 5)->toRawSql();
```

3. **Query listener**

```php
DB::listen(function ($query) {
    logger()->debug($query->sql, $query->bindings);
});
```

4. **Herramientas**

- Laravel Telescope / Debugbar pueden mostrar consultas ejecutadas y tiempos.

Usa estos métodos en desarrollo/depuración, no como salida permanente en producción.

</details>

<details>
<summary>50. ¿Qué métodos agregados están disponibles en query builder?</summary>

#### Laravel

Laravel Query Builder proporciona helpers agregados estándar de SQL.

1. **Métodos agregados principales**

- `count()`
- `sum($column)`
- `avg($column)` / `average($column)`
- `min($column)`
- `max($column)`

2. **Ejemplos**

```php
$totalUsers = DB::table('users')->count();
$totalRevenue = DB::table('orders')->sum('amount');
$avgOrder = DB::table('orders')->avg('amount');
$firstDate = DB::table('orders')->min('created_at');
$latestDate = DB::table('orders')->max('created_at');
```

3. **Con consultas agrupadas**

- Combina `selectRaw(...)` + `groupBy(...)` para agregados por grupo.

4. **Por qué son útiles**

- Cálculos eficientes del lado del servidor.
- Evitan transferir filas innecesarias a la memoria de la aplicación.

Los agregados son esenciales para dashboards, analítica y endpoints de métricas de negocio.

</details>

<details>
<summary>51. ¿Qué son las transacciones de base de datos y cómo se usan?</summary>

#### Laravel

Una transacción de base de datos agrupa múltiples operaciones en una unidad atómica: o todas se completan o todas se revierten.

1. **Por qué se necesitan transacciones**

- Preservan la consistencia de datos entre escrituras relacionadas.
- Evitan actualizaciones parciales cuando ocurre una excepción.

2. **Uso en Laravel**

```php
DB::transaction(function () use ($orderData) {
    $order = Order::create($orderData);
    Inventory::reserveForOrder($order);
    Payment::captureForOrder($order);
});
```

3. **Control manual (opcional)**

```php
DB::beginTransaction();

try {
    // operations
    DB::commit();
} catch (Throwable $e) {
    DB::rollBack();
    throw $e;
}
```

4. **Buenas prácticas**

- Mantén el alcance de la transacción pequeño y rápido.
- Evita llamadas HTTP externas largas dentro de una transacción.
- Combina con bloqueo de filas cuando sea necesario para flujos sensibles a concurrencia.

Las transacciones son críticas para flujos de negocio confiables de finanzas, inventario y procesos de múltiples pasos.

</details>

<details>
<summary>52. ¿Qué son las migraciones y por qué son importantes?</summary>

#### Laravel

Las migraciones son archivos PHP versionados que definen cambios del esquema de base de datos a lo largo del tiempo.

1. **Qué hacen las migraciones**

- Crear/modificar/eliminar tablas, columnas, índices y restricciones.
- Mantener cambios de esquema reproducibles entre entornos.

2. **Por qué son importantes**

- Colaboración de equipo sobre esquema con code review.
- Deploys y rollbacks determinísticos.
- Enfoque de infraestructura como código para la evolución de base de datos.

3. **Estructura típica de migración**

- `up()` aplica cambios.
- `down()` revierte cambios.

4. **Valor operativo**

- Onboarding y configuración de CI más simples.
- Menor deriva de base de datos tipo “works on my machine”.

Las migraciones son la base de una gestión mantenible del ciclo de vida del esquema en Laravel.

</details>

<details>
<summary>53. ¿Cómo generas y haces rollback de migraciones?</summary>

#### Laravel

Laravel proporciona comandos Artisan para crear y gestionar la ejecución de migraciones.

1. **Generar migración**

```bash
php artisan make:migration create_orders_table
php artisan make:migration add_status_to_orders_table --table=orders
```

2. **Ejecutar migraciones**

```bash
php artisan migrate
```

3. **Rollback del último lote**

```bash
php artisan migrate:rollback
```

4. **Rollback de múltiples pasos**

```bash
php artisan migrate:rollback --step=3
```

5. **Otros comandos útiles**

- `php artisan migrate:reset` (rollback de todo)
- `php artisan migrate:refresh` (reset + migrate)
- `php artisan migrate:fresh` (elimina todas las tablas + migrate)

Usa comandos de rollback/refresh con cuidado en entornos de producción.

</details>

<details>
<summary>54. ¿Qué son seeders y factories?</summary>

#### Laravel

Los seeders y factories ayudan a generar e insertar datos de prueba o iniciales de forma eficiente.

1. **Seeders**

- Clases que rellenan la base de datos con conjuntos de datos conocidos.
- Útiles para datos base/de referencia (roles, permisos, configuraciones).

2. **Factories**

- Plantillas para generar instancias de modelos con datos falsos o personalizados.
- Útiles para tests y datos de demo/desarrollo.

3. **Cómo trabajan juntos**

- El seeder llama factories para crear muchos registros rápidamente.

```php
User::factory()->count(50)->create();
```

4. **Casos de uso**

- Bootstrap de desarrollo local.
- Configuración de tests automatizados.
- Generación de entornos de staging/demo.

Los seeders definen qué insertar; las factories definen cómo se generan los datos del modelo.

</details>

<details>
<summary>55. ¿Cómo funcionan las factories en Laravel moderno?</summary>

#### Laravel

Las factories modernas de Laravel están basadas en clases y centradas en modelos, normalmente en `database/factories`.

1. **Factory basada en `definition`**

- `definition()` devuelve atributos fake por defecto.

```php
final class UserFactory extends Factory
{
    public function definition(): array
    {
        return [
            'name' => fake()->name(),
            'email' => fake()->unique()->safeEmail(),
            'password' => bcrypt('password'),
        ];
    }
}
```

2. **States**

- Variantes nombradas para escenarios específicos.

```php
public function admin(): static
{
    return $this->state(fn () => ['is_admin' => true]);
}
```

3. **Uso**

```php
User::factory()->admin()->count(3)->create();
User::factory()->make(); // no persistido
```

4. **Relaciones**

- Las factories soportan creación de relaciones vía `has()`, `for()` y callbacks.

Las factories hacen que la generación de datos para tests sea expresiva, componible y determinista.

</details>

<details>
<summary>56. ¿Qué es database seeding?</summary>

#### Laravel

Database seeding es el proceso de insertar datos predefinidos o generados en la base de datos.

1. **Propósito**

- Preparar la app con datos iniciales requeridos.
- Proporcionar datasets realistas para desarrollo/testing.

2. **Cómo se ejecuta**

- Las clases seeder se ejecutan vía Artisan.

```bash
php artisan db:seed
php artisan db:seed --class=UserSeeder
```

3. **Flujo común**

- `DatabaseSeeder` orquesta otros seeders.
- Se usan factories para registros sintéticos masivos.

4. **Buenas prácticas**

- Mantén determinísticos los datos de referencia core.
- Evita lógica destructiva de seeding en producción salvo intención explícita.
- Versiona seeders junto con la base de código.

El seeding asegura que los entornos sean reproducibles y estén listos para desarrollo o tests.

</details>

<details>
<summary>57. ¿Qué son los soft deletes?</summary>

#### Laravel

Los soft deletes marcan registros como eliminados sin borrarlos físicamente de la tabla.

1. **Cómo funciona**

- Usa una columna timestamp `deleted_at`.
- Al eliminar, se establece `deleted_at`; la fila permanece en la base de datos.
- Las consultas por defecto excluyen filas con soft delete.

2. **Habilitar en el modelo**

```php
use Illuminate\Database\Eloquent\SoftDeletes;

class Post extends Model
{
    use SoftDeletes;
}
```

3. **Helpers clave de consulta**

- `withTrashed()` incluye filas eliminadas.
- `onlyTrashed()` solo filas eliminadas.
- `restore()` recupera el registro.
- `forceDelete()` elimina permanentemente.

4. **Por qué es útil**

- Recuperación de datos y mejor trazabilidad de auditoría.
- Flujos de negocio más seguros donde el riesgo de borrado accidental es alto.

Los soft deletes son un compromiso práctico entre semántica de borrado y recuperabilidad.

</details>

<details>
<summary>58. ¿Cómo optimizas consultas Eloquent para rendimiento?</summary>

#### Laravel

La optimización de rendimiento en Eloquent se centra sobre todo en reducir cantidad de consultas, tamaño de filas y trabajo innecesario de modelos.

1. **Evitar N+1**

- Usa `with()` / `load()` para relaciones.

2. **Seleccionar solo columnas necesarias**

```php
User::query()->select('id', 'name')->get();
```

3. **Usar agregados/comprobaciones de existencia en SQL**

- `count`, `sum`, `exists`, `withCount` en lugar de cargar colecciones completas.

4. **Procesar datasets grandes eficientemente**

- Usa `chunkById`, `lazyById`, `cursor` para iteración segura en memoria.

5. **Estrategia de índices**

- Añade índices correctos en la BD para filtros/ordenamientos/joins frecuentes.

6. **Evitar hidratación excesiva de modelos**

- Usa Query Builder para consultas pesadas de reporting cuando no necesitas comportamiento de modelo completo.

7. **Medir y perfilar**

- Usa Telescope, Debugbar o logs de consultas para encontrar hotspots reales.

Optimizar Eloquent es principalmente diseñar acceso a datos para menos trabajo y mejor localidad de consultas.

</details>

<details>
<summary>59. ¿Qué son los API Resources en Laravel?</summary>

#### Laravel

Los API Resources son capas de transformación que convierten modelos/colecciones en estructuras JSON de respuesta consistentes.

1. **Qué hacen**

- Controlan la forma de salida.
- Ocultan campos internos.
- Formatean/componen datos relacionados de manera predecible.

2. **Ejemplo**

```php
final class UserResource extends JsonResource
{
    public function toArray($request): array
    {
        return [
            'id' => $this->id,
            'name' => $this->name,
            'email' => $this->email,
        ];
    }
}
```

3. **Uso**

```php
return new UserResource($user);
return UserResource::collection($users);
```

4. **Por qué son importantes**

- Contratos API estables.
- Separación entre modelo de persistencia y formato de transporte.
- Versionado de API y control de políticas de respuesta más fáciles.

Los API Resources son la forma nativa y de primera clase de Laravel para estandarizar respuestas JSON de API.

</details>

<details>
<summary>60. ¿Cuál es la diferencia entre API Resources y Transformers?</summary>

#### Laravel

Ambos dan forma a los datos de salida, pero “API Resources” es el estándar встроєний de Laravel, mientras que “Transformers” suele referirse a capas externas/personalizadas de mapeo.

1. **API Resources (integrados)**

- Funcionalidad nativa de Laravel (`JsonResource`).
- Integración estrecha con el framework y uso simple.
- Buena opción por defecto para la mayoría de APIs Laravel.

2. **Transformers (patrón genérico / paquetes)**

- Concepto arquitectónico para mapear datos de dominio a DTOs de respuesta.
- Pueden ser clases personalizadas o soluciones basadas en paquetes (por ejemplo, patrones estilo Fractal).
- Útiles cuando el equipo necesita pipelines de transformación agnósticos al framework o muy personalizados.

3. **Diferencia práctica**

- Resource = enfoque oficial de Laravel.
- Transformer = patrón más amplio que puede o no usar primitivas nativas de Laravel.

4. **Cuál elegir**

- En apps centradas en Laravel, prefiere API Resources por defecto.
- Usa capa de transformers personalizada cuando los límites dominio/API requieren desacoplamiento adicional.

</details>

<details>
<summary>61. ¿Cómo funciona la autenticación en Laravel?</summary>

#### Laravel

La autenticación en Laravel verifica la identidad del usuario y la mantiene entre solicitudes usando guards y providers.

1. **Bloques principales**

- **Guards** definen cómo se autentican usuarios por solicitud (sesión, token, etc.).
- **Providers** definen cómo se recuperan usuarios (normalmente modelo Eloquent).

2. **Flujo basado en sesión (web)**

- El usuario envía credenciales.
- Laravel valida credenciales contra el provider.
- Si es exitoso, el ID del usuario se guarda en sesión.
- Las solicitudes posteriores resuelven el usuario actual desde sesión/cookie.

3. **Flujo basado en token (API)**

- El cliente envía token (por ejemplo, token bearer de Sanctum/Passport).
- El guard valida el token y resuelve el usuario autenticado.

4. **Helpers del framework**

- `Auth::attempt()`, `Auth::user()`, `auth()->check()`.
- Middleware como `auth` protege rutas.

5. **Buena práctica**

- Usa scaffolding/paquetes de autenticación integrados para flujos comunes.
- Mantén la lógica de auth centralizada y evita manejo custom de criptografía/sesión salvo necesidad.

La autenticación en Laravel está dirigida por guards y es consistente entre puntos de entrada web y API.

</details>

<details>
<summary>62. ¿Cuál es la diferencia entre autenticación y autorización?</summary>

#### Laravel

Autenticación y autorización están relacionadas, pero son preocupaciones de seguridad distintas.

1. **Autenticación**

- Responde: “¿Quién eres?”
- Verifica identidad (login/sesión/token).

2. **Autorización**

- Responde: “¿Qué tienes permitido hacer?”
- Comprueba permisos/habilidades sobre acciones/recursos.

3. **Mapeo en Laravel**

- Autenticación: guards, providers, middleware `auth`.
- Autorización: gates, policies, middleware `can`, directivas Blade `@can`.

4. **Ejemplo**

- El usuario está autenticado (logueado) pero aun así puede tener prohibido eliminar el post de otro usuario.

La autenticación establece identidad; la autorización aplica reglas de control de acceso.

</details>

<details>
<summary>63. ¿Qué son Gates y Policies?</summary>

#### Laravel

Gates y Policies son mecanismos de autorización de Laravel.

1. **Gates**

- Reglas de autorización basadas en closures.
- Buenas para habilidades simples no ligadas estrechamente a un modelo.

2. **Policies**

- Autorización basada en clases organizada por modelo/recurso.
- Métodos como `view`, `create`, `update`, `delete`, etc.

3. **Cuándo usar cada uno**

- Usa **Gates** para comprobaciones pequeñas/globales.
- Usa **Policies** para autorización centrada en modelo y apps más grandes.

4. **Ejemplos de uso**

- `Gate::allows('export-reports')`
- `$this->authorize('update', $post)`

Gates ofrecen comprobaciones ligeras; Policies ofrecen autorización estructurada y escalable.

</details>

<details>
<summary>64. ¿Cómo funcionan las directivas Blade @can y @cannot?</summary>

#### Laravel

`@can` y `@cannot` son directivas Blade que renderizan markup de forma condicional según comprobaciones de autorización.

1. **`@can`**

- Renderiza contenido si el usuario está autorizado para una habilidad dada.

```blade
@can('update', $post)
    <a href="{{ route('posts.edit', $post) }}">Edit</a>
@endcan
```

2. **`@cannot`**

- Renderiza contenido si el usuario no está autorizado.

```blade
@cannot('delete', $post)
    <span>You cannot delete this post.</span>
@endcannot
```

3. **Cómo evalúan**

- Internamente llaman a la lógica de autorización de gate/policy.
- Usan el contexto del usuario autenticado actual.

4. **Por qué son útiles**

- Mantienen la UI alineada con las reglas de permisos del backend.
- Evitan mostrar acciones que los usuarios no pueden ejecutar.

Estas directivas simplifican el renderizado de UI sensible a permisos en plantillas Blade.

</details>

<details>
<summary>65. ¿Qué es multi-authentication y cómo puedes implementarla?</summary>

#### Laravel

Multi-authentication significa soportar múltiples tipos de usuario/guards en la misma aplicación (por ejemplo `web`, `admin`, `api`).

1. **Escenarios típicos**

- Portales separados para admin y cliente.
- Acceso de personal interno y partners externos.
- Estrategias de auth diferentes por canal.

2. **Cómo implementarlo**

- Define múltiples guards/providers en la configuración de auth.
- Asigna middleware con guard específico: `auth:admin`, `auth:web`, `auth:sanctum`.
- Opcionalmente usa flujos de login/controladores/rutas separados por guard.

3. **Ejemplo de protección de ruta**

```php
Route::middleware('auth:admin')->group(function () {
    Route::get('/admin/dashboard', AdminDashboardController::class);
});
```

4. **Buenas prácticas**

- Aísla grupos de rutas y flujos de sesión específicos por guard.
- Mantén reglas de autorización explícitas por tipo de usuario.

Multi-auth ofrece separación clara de identidades y permisos entre dominios de la aplicación.

</details>

<details>
<summary>66. Compara Laravel Sanctum y Laravel Passport.</summary>

#### Laravel

Sanctum y Passport ofrecen autenticación para APIs, pero están orientados a niveles de complejidad distintos.

1. **Sanctum**

- Autenticación ligera por token + autenticación por sesión para SPA.
- Personal access tokens y abilities simples.
- Configuración sencilla, mínima complejidad OAuth.

2. **Passport**

- Implementación completa de servidor OAuth2.
- Soporta authorization code, client credentials, password (uso legacy), refresh tokens y scopes.
- Mejor para escenarios de autorización delegada con terceros.

3. **Tradeoff de complejidad**

- Sanctum: más simple y rápido para apps first-party.
- Passport: más potente, pero más pesado de configurar/operar.

4. **Ajuste típico**

- Sanctum: SPA/app móvil + backend propio.
- Passport: APIs de ecosistema/plataforma con clientes OAuth externos.

Elige según requisitos del protocolo de auth, no solo por popularidad del paquete.

</details>

<details>
<summary>67. ¿Cuándo elegirías Sanctum en lugar de Passport?</summary>

#### Laravel

Elige Sanctum cuando necesites autenticación first-party directa sin flujos OAuth2 completos.

1. **Buenos casos para Sanctum**

- SPA + backend Laravel usando auth por sesión/cookie.
- Clientes móviles o internos usando personal access tokens.
- APIs pequeñas/medianas donde la delegación OAuth2 no es necesaria.

2. **Por qué Sanctum**

- Implementación más rápida.
- Menor complejidad operativa.
- Menos piezas móviles para gestión de tokens.

3. **Cuándo no alcanza**

- Apps de terceros necesitan autorización delegada de usuario.
- Requieres flujos OAuth2 completos y capacidades de auth server a nivel estándar.

4. **Regla de decisión**

- Usa Sanctum por defecto en apps first-party.
- Pasa a Passport solo cuando los requisitos OAuth2 sean explícitos.

Sanctum es el valor por defecto pragmático para la mayoría de APIs de producto en Laravel.

</details>

<details>
<summary>68. ¿Cómo protege Laravel contra SQL Injection?</summary>

#### Laravel

Laravel reduce el riesgo de SQL injection usando parameter binding y abstracciones de consulta seguras por defecto.

1. **Prepared statements/bindings**

- Query Builder y Eloquent usan parámetros vinculados en lugar de SQL concatenado como strings.

2. **Ejemplos seguros**

```php
User::where('email', $email)->first();
DB::table('orders')->where('status', $status)->get();
```

3. **Dónde sigue habiendo riesgo**

- Concatenación insegura de strings en SQL crudo.

```php
// riesgoso si $input no es confiable
DB::select("SELECT * FROM users WHERE email = '$input'");
```

4. **Uso seguro de SQL crudo**

- Usa placeholders y bindings:

```php
DB::select('SELECT * FROM users WHERE email = ?', [$input]);
```

5. **Buenas prácticas**

- Prefiere Eloquent/Query Builder.
- Valida entrada y evita composición manual de SQL con valores no confiables.

Laravel es seguro por defecto en este punto, pero un mal uso de SQL crudo puede reintroducir riesgo de inyección.

</details>

<details>
<summary>69. ¿Cómo protege Laravel contra ataques CSRF?</summary>

#### Laravel

Laravel protege contra CSRF exigiendo un token CSRF válido para solicitudes web que cambian estado.

1. **Cómo funciona**

- Se genera un token por sesión y se guarda del lado del servidor.
- Los formularios incluyen el token (`@csrf`).
- Middleware verifica el token en solicitudes entrantes POST/PUT/PATCH/DELETE.

2. **Uso en Blade**

```blade
<form method="POST" action="/profile">
    @csrf
    <!-- fields -->
</form>
```

3. **AJAX/SPAs**

- El token puede enviarse por header (por ejemplo, `X-CSRF-TOKEN`) para flujos de sesión same-site.

4. **Por qué es efectivo**

- Los atacantes no pueden falsificar un token válido ligado a la sesión desde el contexto de otro sitio.

5. **Nota de alcance**

- CSRF aplica principalmente a solicitudes de navegador autenticadas por cookie/sesión, no a APIs típicas stateless con bearer token.

El middleware CSRF es una capa de seguridad web core por defecto en Laravel.

</details>

<details>
<summary>70. ¿Cómo protege Laravel contra ataques XSS?</summary>

#### Laravel

Laravel ayuda a prevenir XSS principalmente mediante escape de salida y defaults seguros de templating.

1. **Escape por defecto en Blade**

- `{{ $value }}` se escapa automáticamente en HTML.
- Evita que HTML/JS no confiable se renderice/ejecute.

2. **Precaución con salida no escapada**

- `{!! $value !!}` renderiza HTML crudo y debe usarse solo con contenido confiable/sanitizado.

3. **Protecciones adicionales**

- Validación y normalización de entrada reducen propagación de payloads inseguros.
- Headers CSP/de seguridad (vía middleware/configuración del servidor) añaden defensa en profundidad.

4. **Consideraciones frontend/API**

- Devolver JSON es más seguro que renderizar snippets HTML crudos.
- Al renderizar contenido de usuario en frontend, sanitizarlo según contexto.

5. **Buenas prácticas**

- Mantener escaping por defecto.
- Minimizar renderizado HTML crudo.
- Aplicar sanitización específica por contexto al mostrar contenido rico de usuario.

Laravel ofrece buenas defensas por defecto contra XSS, pero la disciplina de output encoding sigue siendo esencial.

</details>

<details>
<summary>71. ¿Cómo funciona el cifrado en Laravel?</summary>

#### Laravel

Laravel ofrece cifrado simétrico mediante la fachada `Crypt` usando la clave de tu aplicación.

1. **Cómo funciona**

- Usa la clave de aplicación desde entorno/configuración.
- Cifra datos e incluye protección de integridad para detectar manipulación.
- Descifra solo con la misma clave.

2. **Uso común**

```php
$encrypted = Crypt::encryptString('secret-value');
$plain = Crypt::decryptString($encrypted);
```

3. **Dónde se usa**

- Valores sensibles almacenados en DB/payloads configurados.
- Internals del framework como cookies cifradas (cuando está habilitado).

4. **Buenas prácticas**

- Mantén `APP_KEY` secreta y estable por entorno.
- Rota claves cuidadosamente con estrategia de migración.
- No cifres lo que debe hashearse (por ejemplo, contraseñas).

El cifrado de Laravel ofrece protección segura en reposo para datos sensibles reversibles de forma sencilla.

</details>

<details>
<summary>72. ¿Cómo se hashean las contraseñas en Laravel?</summary>

#### Laravel

Laravel hashea contraseñas usando hashing unidireccional mediante la fachada `Hash`, no cifrado reversible.

1. **Enfoque por defecto**

- Usa algoritmos modernos de hash de contraseñas (normalmente `bcrypt` o `argon2id` según configuración).
- Guarda solo el hash, nunca la contraseña en texto plano.

2. **Crear hash**

```php
$hash = Hash::make($password);
```

3. **Verificar contraseña**

```php
if (Hash::check($plainPassword, $user->password)) {
    // valid
}
```

4. **Rehashing**

- `Hash::needsRehash()` ayuda a actualizar hashes cuando cambian configuración/costos.

5. **Buenas prácticas**

- Nunca almacenes ni registres contraseñas en crudo.
- Usa políticas de validación fuertes e intentos de login con rate limit.

El hashing de contraseñas en Laravel es seguro por defecto cuando se usan correctamente las APIs integradas.

</details>

<details>
<summary>73. ¿Qué buenas prácticas de seguridad debe seguir toda aplicación Laravel?</summary>

#### Laravel

Toda aplicación Laravel debe combinar defaults del framework con disciplina operativa estricta.

1. **Auth y control de acceso**

- Aplica autenticación en rutas protegidas.
- Usa gates/policies para comprobaciones de autorización.
- Aplica diseño de permisos con mínimo privilegio.

2. **Seguridad de entrada/salida**

- Valida todos los datos entrantes de solicitudes.
- Escapa salida por defecto (Blade `{{ }}`).
- Evita concatenación de SQL crudo; usa bindings.

3. **Seguridad de sesión y cookies**

- Habilita `HttpOnly`, `Secure` y configuración `SameSite` adecuada.
- Regenera sesiones en login/logout.

4. **Secretos y configuración**

- Protege `.env`, rota secretos y separa entornos.
- Nunca subas credenciales a git.

5. **Transporte y headers**

- Fuerza HTTPS.
- Añade headers de seguridad (CSP, HSTS, X-Frame-Options, etc.).

6. **Higiene de dependencias y plataforma**

- Mantén Laravel/PHP/paquetes actualizados.
- Monitorea vulnerabilidades y aplica parches rápido.

7. **Protección contra abuso**

- Usa rate limiting para auth y endpoints sensibles.
- Registra y monitorea actividad sospechosa.

8. **Protección de datos**

- Hashea contraseñas, cifra datos sensibles reversibles.
- Haz backups y prueba procedimientos de restauración.

La seguridad no es una sola función; es una práctica por capas y continua entre código y operaciones.

</details>

<details>
<summary>74. ¿Cómo funcionan las signed URLs en Laravel?</summary>

#### Laravel

Las signed URLs incluyen una firma criptográfica que prueba que la URL fue generada por tu app y no fue manipulada.

1. **Qué protegen**

- Integridad de path URL + parámetros de query.
- Expiración opcional para enlaces con tiempo limitado.

2. **Generar signed URL**

```php
$url = URL::signedRoute('unsubscribe', ['user' => $user->id]);
$temporary = URL::temporarySignedRoute('download', now()->addMinutes(30), ['file' => $fileId]);
```

3. **Validar firma**

- Usa middleware `signed` en la ruta, o valida vía helper de request.

```php
Route::get('/unsubscribe/{user}', UnsubscribeController::class)
    ->name('unsubscribe')
    ->middleware('signed');
```

4. **Casos de uso**

- Enlaces de unsubscribe.
- Acciones de verificación de email.
- Enlaces temporales de descarga o acciones.

Las signed URLs son una forma simple de asegurar enlaces públicos sin requerir sesiones autenticadas completas.

</details>

<details>
<summary>75. ¿Qué son las encrypted cookies y signed cookies?</summary>

#### Laravel

Las encrypted cookies y signed cookies protegen integridad de cookies, pero el cifrado además protege confidencialidad.

1. **Encrypted cookies**

- El valor de la cookie se cifra y autentica.
- El cliente no puede leer ni alterar el valor original.
- Middleware de Laravel puede cifrar/descifrar automáticamente.

2. **Signed cookies (enfoque en integridad)**

- El valor permanece legible pero incluye/verifica firma.
- Detecta manipulación, pero no oculta contenido.

3. **Comportamiento por defecto en Laravel**

- Laravel suele usar cookies cifradas para cookies de aplicación mediante su stack middleware de cookies.

4. **Cuándo usar**

- Usa cookies cifradas para valores sensibles/con estado.
- Usa semántica solo firmada cuando la transparencia sea aceptable pero se requiera detección de manipulación.

5. **Nota de seguridad**

- Define siempre atributos `Secure`, `HttpOnly` y `SameSite` adecuados.

En la práctica, las cookies cifradas suelen ser el default más seguro para aplicaciones web Laravel.

</details>

<details>
<summary>76. Explica el sistema de colas de Laravel.</summary>

#### Laravel

El sistema de colas de Laravel mueve tareas que consumen tiempo fuera del ciclo de solicitud HTTP hacia procesamiento asíncrono en segundo plano.

1. **Por qué se usan colas**

- Respuestas más rápidas para usuarios.
- Mejor escalabilidad bajo carga.
- Ejecución confiable para reintentos y manejo de fallos.

2. **Cómo funciona**

- La aplicación despacha un job a un backend de cola.
- Un proceso worker consume jobs y los ejecuta.
- Los jobs fallidos pueden reintentarse o moverse a almacenamiento de fallos.

3. **Tareas típicas en cola**

- Emails, notificaciones, generación de reportes.
- Integraciones API y webhooks.
- Procesamiento de imagen/video e importaciones/exportaciones pesadas.

4. **Herramientas core del ecosistema**

- Workers `queue:work`.
- Seguimiento en `failed_jobs`.
- Horizon (para colas Redis) para monitoreo y control.

La arquitectura de colas es esencial para aplicaciones Laravel responsivas y resilientes.

</details>

<details>
<summary>77. ¿Qué son jobs y queue workers?</summary>

#### Laravel

Jobs y workers son los componentes productor-consumidor centrales del procesamiento asíncrono en Laravel.

1. **Jobs**

- Clases de tareas encapsuladas (normalmente en `app/Jobs`).
- Representan una unidad de trabajo para ejecutar ahora o después.
- A menudo implementan `ShouldQueue` para ejecución asíncrona.

2. **Queue workers**

- Procesos de larga ejecución que ejecutan jobs en cola.
- Se inician vía Artisan (`php artisan queue:work`).
- Soportan opciones de reintentos, timeout, sleep y selección de cola.

3. **Flujo**

- El código despacha job (`dispatch(...)`).
- El payload del job se envía al backend de cola seleccionado.
- El worker toma el job y ejecuta `handle()`.

4. **Confiabilidad**

- Reintentos automáticos en fallos transitorios.
- Seguimiento de jobs fallidos para inspección y re-ejecución.

Jobs definen qué trabajo hacer; workers proveen el motor de ejecución en background.

</details>

<details>
<summary>78. ¿Qué drivers de colas están disponibles en Laravel?</summary>

#### Laravel

Laravel soporta múltiples backends de cola mediante drivers configurables.

1. **Drivers integrados comunes**

- `sync`
- `database`
- `redis`
- `sqs` (Amazon SQS)
- `null`

2. **Características generales**

- `sync`: ejecución inmediata en la solicitud actual.
- `database`: almacena jobs en tablas de base de datos.
- `redis`: backend de colas rápido en memoria.
- `sqs`: servicio de colas cloud administrado.
- `null`: descarta jobs (útil en algunos escenarios local/testing).

3. **Configuración**

- Definida en `config/queue.php` y variables de entorno.

Elige el driver según confiabilidad, throughput, infraestructura y necesidades de operación.

</details>

<details>
<summary>79. ¿Cuál es la diferencia entre los drivers de cola sync, database, Redis y SQS?</summary>

#### Laravel

Estos drivers difieren en modelo de ejecución, rendimiento, características de confiabilidad y operación.

1. **`sync`**

- Ejecuta el job inmediatamente durante la solicitud.
- No requiere worker en background.
- Bueno para desarrollo local/flujos simples, no para cargas async pesadas en producción.

2. **`database`**

- Persiste jobs en una tabla relacional.
- Fácil de configurar, durable, pero más lento con alto throughput de cola.

3. **`redis`**

- Backend de cola en memoria y de alto rendimiento.
- Excelente para workloads de alto throughput/baja latencia.
- Suele combinarse con Horizon para monitoreo.

4. **`sqs`**

- Servicio de colas AWS totalmente gestionado.
- Altamente escalable y durable.
- Bueno para arquitecturas distribuidas/cloud-native; introduce consideraciones de latencia/costo cloud.

5. **Selección práctica**

- Pequeño/simple: `database`.
- Stack de alto throughput con Redis: `redis`.
- Sistemas distribuidos nativos de AWS: `sqs`.
- Local o ejecución inline forzada: `sync`.

La elección del driver debe ajustarse al perfil de tráfico y estrategia de infraestructura.

</details>

<details>
<summary>80. ¿Cómo manejas jobs fallidos?</summary>

#### Laravel

Laravel ofrece mecanismos integrados para registrar, inspeccionar, reintentar y limpiar jobs en cola fallidos.

1. **Registro de fallos**

- Configura almacenamiento de failed jobs (comúnmente tabla `failed_jobs`).
- Las excepciones durante la ejecución marcan el job como fallido tras agotar el límite de reintentos.

2. **Comportamiento de reintentos**

- Controla reintentos con propiedades/opciones del job (`tries`, estrategias de backoff).

3. **Comandos útiles**

```bash
php artisan queue:failed
php artisan queue:retry all
php artisan queue:forget <id>
php artisan queue:flush
```

4. **Manejo a nivel de job**

- Implementa método `failed(Throwable $e)` para lógica de limpieza/alertas/compensación.

5. **Buenas prácticas**

- Haz jobs idempotentes.
- Añade logging estructurado y alertas.
- Separa manejo de fallos transitorios vs permanentes.

Un manejo sólido de jobs fallidos es crítico para sistemas asíncronos confiables.

</details>

<details>
<summary>81. ¿Qué es job batching?</summary>

#### Laravel

Job batching agrupa múltiples jobs en un solo batch rastreable con callbacks de ciclo de vida compartidos y monitoreo de progreso.

1. **Qué te aporta batching**

- Despachar muchos jobs como una unidad lógica.
- Rastrear progreso, finalización y fallos.
- Ejecutar callbacks para `then`, `catch`, `finally`.

2. **Concepto de ejemplo**

- Importación de archivo dividida en muchos jobs de procesamiento por chunks dentro de un batch.

3. **Casos de uso comunes**

- Importaciones/exportaciones de datos.
- Operaciones grandes de reindexado.
- Workloads fan-out donde importa la finalización global.

4. **Beneficios operativos**

- Mejor observabilidad y orquestación para flujos multi-job.
- Cancelación/monitoreo más fácil desde UI/herramientas de administración.

Batching es útil cuando muchos jobs paralelos pertenecen al mismo proceso de negocio.

</details>

<details>
<summary>82. ¿Qué son los queued listeners?</summary>

#### Laravel

Los queued listeners son listeners de eventos que se ejecutan de forma asíncrona a través del sistema de colas en lugar de ejecutarse inline durante el dispatch del evento.

1. **En qué difieren de listeners normales**

- El listener normal se ejecuta inmediatamente.
- El queued listener se envía a la cola y lo procesa un worker.

2. **Cómo habilitarlo**

- El listener implementa `ShouldQueue`.

3. **Por qué usarlos**

- Mantener rápido el dispatch de eventos y el ciclo de solicitud.
- Delegar efectos secundarios pesados (emails, llamadas API externas, escritura de analítica).

4. **Buenas prácticas**

- Asegura que la lógica del listener sea idempotente.
- Configura reintentos/timeouts adecuadamente.
- Maneja fallos de dependencias externas con gracia.

Los queued listeners son clave para procesamiento de eventos escalable sin bloquear solicitudes de usuario.

</details>

<details>
<summary>83. ¿Qué son events y listeners en Laravel?</summary>

#### Laravel

Events y listeners implementan comunicación estilo publish-subscribe dentro de una aplicación Laravel.

1. **Event**

- Representa algo que ocurrió en el dominio/aplicación.
- Ejemplo: `OrderPaid`, `UserRegistered`, `InvoiceOverdue`.

2. **Listener**

- Clase que reacciona al evento y ejecuta un efecto secundario.
- Ejemplo: enviar email, actualizar CRM, encolar job downstream.

3. **Por qué este patrón es útil**

- Desacopla el flujo principal de efectos secundarios.
- Mejora modularidad y mantenibilidad.
- Permite múltiples reacciones a un evento sin cambiar el productor del evento.

4. **Dispatch y manejo**

- Despacha el evento desde servicio/controlador.
- El framework enruta el evento a listeners registrados.

Los events modelan hechos; los listeners implementan reacciones.

</details>

<details>
<summary>84. ¿Cómo generas events y listeners?</summary>

#### Laravel

Laravel ofrece generadores Artisan y patrones de registro automático para events y listeners.

1. **Generar event**

```bash
php artisan make:event OrderPaid
```

2. **Generar listener**

```bash
php artisan make:listener SendOrderReceipt --event=OrderPaid
```

3. **Registrar mapeo**

- Mapea el event al listener en el event service provider o usa configuración de descubrimiento del framework.

4. **Despachar event**

```php
event(new OrderPaid($order));
```

5. **Encolar listener si es necesario**

- Implementa `ShouldQueue` en el listener para manejo asíncrono.

Generación + registro claro mantiene los flujos de eventos explícitos y mantenibles.

</details>

<details>
<summary>85. ¿Qué es la arquitectura orientada a eventos en Laravel?</summary>

#### Laravel

La arquitectura orientada a eventos (EDA) en Laravel organiza el comportamiento de la aplicación alrededor de eventos de dominio/aplicación y reacciones asíncronas.

1. **Principio central**

- Emite eventos cuando ocurren hechos importantes.
- Listeners independientes manejan acciones posteriores.

2. **Beneficios**

- Bajo acoplamiento entre módulos.
- Extensión de funcionalidades más simple sin modificar el flujo core.
- Mejor escalabilidad cuando los listeners están en cola.

3. **Patrón típico**

- Se completa una acción transaccional.
- Se despacha un evento (`OrderPaid`).
- Se ejecutan múltiples listeners (email, analítica, sincronización de fulfillment).

4. **Guía de diseño**

- Mantén nombres de eventos con significado de negocio.
- Evita poner lógica de negocio pesada directamente en listeners salvo intención explícita.
- Asegura idempotencia y observabilidad en listeners asíncronos.

EDA en Laravel ayuda a construir sistemas modulares y escalables que evolucionan limpiamente con el tiempo.

</details>

<details>
<summary>86. ¿Qué es Laravel Broadcasting?</summary>

#### Laravel

Laravel Broadcasting es la capa de entrega de eventos en tiempo real de Laravel para enviar eventos del servidor a clientes frontend por WebSockets (o drivers compatibles).

1. **Qué hace**

- Difunde eventos Laravel seleccionados a canales.
- Permite que clientes se suscriban y reaccionen al instante.

2. **Casos de uso típicos**

- Notificaciones en vivo.
- Chat e indicadores de presencia.
- Dashboards y actualizaciones de estado en tiempo real.

3. **Conceptos core**

- Canales: `public`, `private`, `presence`.
- Autorización para canales private/presence.
- Clases de eventos que implementan comportamiento de broadcasting.

4. **Vista general del stack**

- El backend emite un evento broadcast.
- El driver de broadcasting envía por infraestructura websocket.
- El frontend (normalmente Laravel Echo) escucha y actualiza UI.

Broadcasting permite una UX responsiva y orientada a eventos sin arquitecturas pesadas de polling.

</details>

<details>
<summary>87. ¿Cómo funciona Laravel Echo?</summary>

#### Laravel

Laravel Echo es una librería cliente JavaScript que se suscribe a canales broadcast y escucha eventos Laravel en el navegador.

1. **Rol en el stack realtime**

- Proporciona una API frontend conveniente sobre transporte websocket.
- Se integra con convenciones de nombres de canales y eventos de Laravel.

2. **Cómo funciona**

- La app inicializa Echo con configuración del broadcaster.
- El cliente se une a canales (`channel`, `private`, `presence`).
- Escucha eventos broadcast del servidor y ejecuta callbacks.

3. **Concepto de ejemplo**

```js
Echo.private(`orders.${orderId}`)
  .listen('OrderShipped', (payload) => {
    // update UI
  });
```

4. **Por qué los equipos lo usan**

- API limpia para suscripciones realtime.
- Menos boilerplate en manejo de eventos websocket.
- Funciona bien con flujo de broadcasting/auth de Laravel.

Echo es el puente frontend estándar para funcionalidades realtime de Laravel.

</details>

<details>
<summary>88. ¿Qué es Laravel Reverb y por qué es importante en Laravel moderno?</summary>

#### Laravel

Laravel Reverb es el servidor WebSocket first-party de Laravel para broadcasting en tiempo real.

1. **Qué ofrece Reverb**

- Infraestructura websocket nativa gestionada por Laravel.
- Integración estrecha con broadcasting de Laravel, auth de canales y Echo.

2. **Por qué es importante**

- Reduce dependencia de proveedores realtime de terceros para muchos casos de uso.
- Mejora desarrollo local y consistencia operativa en stacks centrados en Laravel.
- Da a los equipos control directo sobre escalado, despliegue y observabilidad.

3. **Dónde encaja**

- Notificaciones en tiempo real.
- Funcionalidades de colaboración en vivo.
- Dashboards operativos y streams de eventos.

4. **Impacto práctico**

- Apps Laravel modernas pueden mantener más arquitectura realtime dentro del ecosistema Laravel con menos fronteras de integración.

Reverb es una parte clave de la historia realtime moderna en Laravel.

</details>

<details>
<summary>89. ¿Qué es Laravel Horizon?</summary>

#### Laravel

Laravel Horizon es un dashboard de monitoreo y gestión de colas para colas basadas en Redis.

1. **Qué hace**

- Visualiza throughput de colas, tiempo de ejecución, fallos y tiempos de espera.
- Proporciona gestión de configuración de workers/supervisores.
- Ayuda a ajustar rendimiento y confiabilidad de colas.

2. **Características clave**

- Métricas y tendencias de jobs.
- Inspección de jobs fallidos.
- Estrategias de balanceo de colas.
- Definiciones de supervisores por entorno.

3. **Por qué importa**

- Mejor visibilidad operativa.
- Respuesta a incidentes más rápida para cargas async.
- Escalado más seguro del procesamiento en background.

Horizon es la capa operativa principal de producción para cargas de colas Redis en Laravel.

</details>

<details>
<summary>90. ¿Qué es task scheduling en Laravel?</summary>

#### Laravel

El task scheduling de Laravel es una capa de orquestación tipo cron definida en código para comandos/jobs recurrentes.

1. **Idea central**

- Define el schedule en código de aplicación.
- El cron del SO dispara el scheduler de Laravel cada minuto.

2. **Uso típico**

- Sincronizaciones periódicas de datos.
- Jobs de limpieza.
- Generación de reportes.
- Resúmenes de notificaciones.

3. **Beneficios**

- Definiciones de schedule centralizadas y versionadas.
- Más limpio que gestionar muchas entradas cron separadas del servidor.
- Soporta prevención de solapamiento, restricciones por entorno y control de frecuencia.

4. **Flujo operativo**

- Configura una entrada cron para `schedule:run`.
- Laravel decide qué tareas programadas deben ejecutarse ahora.

Task scheduling brinda automatización recurrente predecible y mantenible en apps Laravel.

</details>

<details>
<summary>91. ¿Cómo funciona la concurrencia en colas?</summary>

#### Laravel

La concurrencia en colas se logra ejecutando múltiples workers (y/o múltiples colas) en paralelo, permitiendo procesar muchos jobs simultáneamente.

1. **Modelo de concurrencia**

- Cada worker procesa jobs de forma independiente.
- Más workers = mayor throughput paralelo (dentro de límites de infraestructura).

2. **Palancas de control**

- Número de procesos worker.
- Separación por prioridad de cola (`high`, `default`, `low`).
- Configuración de timeout, retry y memoria del worker.
- Estrategias de balanceo de Horizon (para Redis).

3. **Requisitos de seguridad**

- Los jobs deben ser idempotentes.
- Recursos compartidos pueden requerir locking/operaciones atómicas.
- Manejar condiciones de carrera en transiciones de estado.

4. **Patrón de escalado**

- Escala workers horizontalmente bajo carga.
- Monitorea lag de cola y métricas de fallos para ajustar concurrencia.

La concurrencia mejora throughput, pero la corrección depende del diseño de jobs y controles de consistencia de datos.

</details>

<details>
<summary>92. ¿Qué es idempotencia en jobs en cola?</summary>

#### Laravel

La idempotencia significa que ejecutar el mismo job varias veces produce el mismo efecto final que ejecutarlo una sola vez.

1. **Por qué importa en colas**

- Los jobs pueden reintentarse tras fallos/timeouts.
- Puede haber dispatch duplicado.
- Workers pueden caerse tras progreso parcial.

2. **Cómo implementarla**

- Usa claves de negocio únicas/claves de idempotencia.
- Verifica estado actual antes de aplicar efectos secundarios.
- Usa restricciones de BD u operaciones atómicas.
- Haz llamadas externas con soporte de idempotencia del proveedor cuando exista.

3. **Ejemplos**

- “Enviar email de factura una vez por ID de factura.”
- “Capturar pago solo si el estado sigue pendiente.”

4. **Buena práctica**

- Diseña idempotencia a nivel de caso de uso, no como idea tardía.

Jobs idempotentes son esenciales para sistemas asíncronos confiables y seguros ante reintentos.

</details>

<details>
<summary>93. ¿Cómo funciona el caching en Laravel?</summary>

#### Laravel

El caching en Laravel almacena datos calculados en almacenamiento rápido para reducir operaciones costosas repetidas.

1. **Idea central**

- Lee primero desde caché.
- Si no existe, calcula el dato y guárdalo con TTL.

2. **API principal**

- `Cache::get()`, `put()`, `remember()`, `rememberForever()`, `forget()`.

3. **Patrón típico**

```php
$users = Cache::remember('users.active', 300, function () {
    return User::where('is_active', true)->get();
});
```

4. **Dónde se usa**

- Caché de resultados de consultas.
- Búsquedas de configuración/metadatos.
- Almacenamiento relacionado con rate-limit y sesión (según driver).

5. **Objetivo**

- Menor carga de BD, menor latencia, mejor throughput.

El caching es una palanca principal de rendimiento en sistemas Laravel de producción.

</details>

<details>
<summary>94. ¿Qué drivers de caché están disponibles?</summary>

#### Laravel

Laravel soporta múltiples backends de caché mediante drivers configurables.

1. **Drivers comunes**

- `array` (solo runtime, no persistente)
- `file`
- `database`
- `redis`
- `memcached`
- `dynamodb` (cuando está configurado)
- `null`

2. **Características de drivers**

- `array`: útil para tests/runtime local únicamente.
- `file`/`database`: configuración simple, menor rendimiento.
- `redis`/`memcached`: caché de producción de alto rendimiento.
- `null`: deshabilita comportamiento de caché.

3. **Regla de selección**

- Para producción de alta carga, normalmente se prefieren Redis o Memcached.

La elección del driver depende de infraestructura, requisitos de latencia y preferencias operativas.

</details>

<details>
<summary>95. ¿Qué estrategias de caché usarías en una aplicación Laravel de alta carga?</summary>

#### Laravel

Una estrategia de caché para alta carga debe combinar disciplina de capa de datos, capa de aplicación e invalidación.

1. **Cache-aside (`remember`)**

- Patrón read-through para consultas/cómputos costosos.
- Define TTLs razonables según volatilidad de datos.

2. **Enfoque multinivel**

- Datos hot key/value en Redis.
- Caché HTTP/CDN para respuestas públicas cuando sea posible.

3. **Prevenir stampedes**

- Usa locks (`Cache::lock`) alrededor de regeneración para hot keys críticas.
- Escalona TTLs o usa jitter.

4. **Invalidación por tags (si se soporta)**

- Agrupa keys relacionadas por dominio y limpia conjuntos específicos.

5. **Optimizar payloads**

- Cachea proyecciones compactas DTO/array, no grafos de objetos sobredimensionados.

6. **Medir continuamente**

- Rastrea hit rate, latencia p95, churn de keys y uso de memoria.

7. **Fallback y resiliencia**

- Diseña comportamiento elegante ante cache misses/caídas de caché.

En sistemas de alta carga, la estrategia de invalidación y observabilidad es tan importante como la velocidad bruta de caché.

</details>

<details>
<summary>96. ¿Qué son cache tags?</summary>

#### Laravel

Los cache tags te permiten agrupar entradas de caché lógicamente e invalidarlas juntas.

1. **Qué resuelven**

- Invalidación dirigida más fácil de keys relacionadas.
- Evitar flush completo de caché para cambios de datos localizados.

2. **Concepto de ejemplo**

```php
Cache::tags(['users', 'team:42'])->put('users.team.42.list', $data, 600);
Cache::tags(['users', 'team:42'])->flush();
```

3. **Casos de uso típicos**

- Invalidar toda la caché de un tenant/proyecto/categoría.
- Agrupar fragmentos de dashboard/API por contexto de dominio.

4. **Nota importante**

- Cache tags se soportan solo en drivers específicos (comúnmente Redis/Memcached), no en todos los drivers.

Los cache tags aportan valor cuando la invalidación de caché necesita precisión y agrupación por dominio.

</details>

<details>
<summary>97. ¿Cómo limpias y calientas caché?</summary>

#### Laravel

Limpiar elimina entradas obsoletas; calentar precarga entradas hot para evitar latencia de arranque en frío.

1. **Comandos para limpiar caché**

```bash
php artisan cache:clear
php artisan config:clear
php artisan route:clear
php artisan view:clear
php artisan event:clear
```

2. **Construir/optimizar cachés**

```bash
php artisan config:cache
php artisan route:cache
php artisan view:cache
php artisan event:cache
```

3. **Estrategia de warm-up**

- Tras deploy, calcula y guarda proactivamente hot keys conocidas.
- Dispara jobs/comandos de warm-up para endpoints y dashboards críticos.

4. **Práctica operativa**

- Prefiere invalidación selectiva sobre flush global.
- Ejecuta pasos de build de caché en pipeline de despliegue.

Un buen flujo de clear/warm-up de caché reduce picos de latencia en despliegues y regresiones visibles para usuarios.

</details>

<details>
<summary>98. ¿Qué es Laravel Octane?</summary>

#### Laravel

Laravel Octane ejecuta Laravel sobre workers de aplicación de larga vida (Swoole o RoadRunner) en lugar de bootstrapear el framework en cada solicitud.

1. **Qué cambia**

- Mantiene la aplicación en memoria entre solicitudes.
- Reutiliza procesos worker para muchas solicitudes.

2. **Resultado principal**

- Menor overhead por solicitud y mayor throughput.
- Mejor latencia para cargas adecuadas.

3. **Opciones de runtime**

- Runtime basado en Swoole.
- Runtime basado en RoadRunner.

4. **Mejor encaje**

- APIs/apps web de alto tráfico donde el overhead de bootstrap por solicitud es significativo.

Octane es una capa runtime orientada a rendimiento para despliegues Laravel modernos.

</details>

<details>
<summary>99. ¿Cómo mejora Laravel Octane el rendimiento?</summary>

#### Laravel

Octane mejora el rendimiento reduciendo el bootstrap del framework por solicitud y aprovechando procesos worker de larga vida.

1. **Sin boot completo de app en cada solicitud**

- El contenedor/configuración/rutas de Laravel permanecen en memoria por worker.

2. **Mayor throughput**

- Los workers procesan muchas solicitudes sin costos repetidos de inicialización.

3. **Menor latencia**

- Tiempos de respuesta más rápidos para muchos tipos de solicitud, especialmente bajo carga sostenida.

4. **Capacidades de runtime**

- Usa modelos eficientes de event-loop/proceso de Swoole/RoadRunner.

5. **Advertencia importante**

- Las ganancias de rendimiento requieren código compatible con Octane (evitar estado mutable obsoleto entre solicitudes).

El rendimiento de Octane proviene de persistencia y eficiencia del runtime, no de optimización automática del código.

</details>

<details>
<summary>100. ¿Qué son Swoole y RoadRunner?</summary>

#### Laravel

Swoole y RoadRunner son servidores de aplicaciones de alto rendimiento usados como runtimes de Octane.

1. **Swoole**

- Extensión/runtime PHP que ofrece I/O asíncrono, corrutinas y primitivas de red de alto rendimiento.
- Muy rápido, pero requiere configuración de entorno basada en extensión.

2. **RoadRunner**

- Servidor de aplicaciones basado en Go que ejecuta workers PHP persistentes.
- No requiere extensión Swoole; modelo operativo diferente.

3. **Rol común en Laravel**

- Mantener workers de la app Laravel vivos entre solicitudes.
- Mejorar throughput y reducir latencia frente a bootstrap por solicitud clásico con PHP-FPM.

4. **Elegir entre ellos**

- Depende de experiencia operativa del equipo, restricciones de hosting, política de extensiones y ajuste al ecosistema.

Ambos runtimes habilitan la arquitectura de workers de larga vida de Octane.

</details>

<details>
<summary>101. ¿Qué problemas pueden ocurrir con la persistencia de estado en Octane?</summary>

#### Laravel

Como los workers de Octane son de larga vida, el estado mutable puede filtrarse entre solicitudes si el código no está diseñado para persistencia.

1. **Riesgos comunes**

- Estado singleton obsoleto.
- Datos específicos de solicitud/usuario cacheados accidentalmente en memoria.
- Propiedades estáticas reteniendo contexto de solicitudes previas.
- Crecimiento de memoria por referencias no liberadas.

2. **Síntomas típicos**

- Contaminación de datos entre solicitudes.
- Comportamiento inconsistente y difícil de reproducir.
- Bloat gradual de memoria e inestabilidad de workers.

3. **Cómo prevenirlo**

- Mantén servicios stateless cuando sea posible.
- Evita almacenar datos específicos de solicitud en singletons/estáticos.
- Resetea/limpia correctamente estado por solicitud.
- Testea específicamente bajo comportamiento runtime de Octane.

4. **Mitigación operativa**

- Monitorea memoria de workers.
- Usa políticas de recarga periódica de workers.

Octane requiere una disciplina de estado más estricta que apps PHP-FPM tradicionales con aislamiento por solicitud.

</details>
