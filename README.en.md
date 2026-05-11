**Read in other languages: [English 🇺🇸](README.en.md),
[Polska 🇵🇱](README.pl.md), [German 🇩🇪](README.de.md), [French 🇫🇷](README.fr.md),
[Spanish 🇪🇸](README.es.md), [Українська 🇺🇦](README.md).**

<h1>
  Laravel <img src="./assets/laravel.svg" width="40" height="40" alt="Laravel logo"/>
</h1>

<h2>Найпопулярніші питання та відповіді на співбесідах з Laravel</h2>

<details>
<summary>1. What is Laravel and why is it used?</summary>

#### Laravel

Laravel is a modern PHP web framework focused on developer productivity, clean architecture, and maintainable code.

1. **What Laravel is**

- An open-source framework built on top of Symfony components.
- Opinionated enough to give strong defaults, but flexible for custom architecture.

2. **Why it is used**

- Speeds up development with built-in routing, validation, authentication, queues, mail, events, and caching.
- Encourages clean code through service container, middleware, Eloquent ORM, and testing tools.
- Provides first-party tooling (`Artisan`, migrations, scheduler, Horizon, Telescope) for production-ready apps.

3. **Typical use cases**

- REST APIs and backend services.
- Server-rendered web applications.
- Admin panels, SaaS products, and marketplace platforms.
- Background job processing and integrations with third-party services.

In short, Laravel is used to build secure, scalable, and maintainable PHP applications faster with less boilerplate.

</details>

<details>
<summary>2. What are the main advantages of Laravel compared to other PHP frameworks?</summary>

#### Laravel

Laravel’s main advantages come from strong developer experience, rich built-in features, and a large ecosystem.

1. **Developer experience**

- Consistent, expressive API design across framework components.
- Excellent documentation and onboarding.
- Rapid scaffolding and CLI workflows via `Artisan`.

2. **Batteries included**

- First-class support for routing, validation, auth, queues, events, notifications, caching, and scheduling.
- ORM (Eloquent) and schema migrations included by default.

3. **Architecture and maintainability**

- Service container and dependency injection are deeply integrated.
- Middleware and service providers make cross-cutting concerns explicit.
- Strong testing support with PHPUnit/Pest integration.

4. **Ecosystem strength**

- Official tools: Forge, Vapor, Horizon, Telescope, Octane, Sanctum, Passport, Cashier.
- Mature community packages and long-term ecosystem stability.

5. **Operational productivity**

- Smooth CI/CD and deployment workflows.
- Great support for queues, caching, Redis, and monitoring.

Laravel is often chosen when teams want to ship business features quickly without sacrificing code quality and long-term maintainability.

</details>

<details>
<summary>3. How does Laravel follow the MVC architecture?</summary>

#### Laravel

Laravel follows MVC (Model-View-Controller) by separating domain/data logic, request handling, and presentation concerns.

1. **Model (M)**

- Usually Eloquent models in `app/Models`.
- Represent domain entities and database records.
- Contain relationships, scopes, casts, and domain-level behavior.

2. **View (V)**

- Blade templates in `resources/views`.
- Responsible for presentation only.
- Receives prepared data from controllers/view models.

3. **Controller (C)**

- Classes in `app/Http/Controllers`.
- Handle HTTP requests, coordinate validation/services, and return responses.
- Should stay thin: orchestration, not heavy business logic.

4. **Request flow in MVC terms**

- Route maps URL to controller action.
- Controller uses models/services to execute use case.
- Controller returns a view (HTML) or JSON response (API).

Laravel also supports service classes, actions, repositories, and domain layers on top of MVC for larger applications.

</details>

<details>
<summary>4. Describe the request lifecycle in a Laravel application.</summary>

#### Laravel

A Laravel request lifecycle describes how an incoming HTTP request is transformed into a response.

1. **Entry point**

- Web server points to `public/index.php`.
- Composer autoloader and Laravel application bootstrap are loaded.

2. **HTTP kernel startup**

- The service container is initialized.
- Global and route middleware stacks are prepared.

3. **Service providers**

- Providers are registered and booted.
- Core services and app bindings become available.

4. **Routing phase**

- Router matches request method + URI to a route.
- Route middleware pipeline is executed.

5. **Controller/handler execution**

- Controller action, closure, or invokable class runs.
- Dependencies are auto-resolved from the container.
- Validation, authorization, business logic, and data access occur.

6. **Response creation**

- Handler returns `Response`, `JsonResponse`, view, redirect, or serializable data.
- Laravel normalizes output to an HTTP response object.

7. **Termination phase**

- Response is sent to client.
- Terminable middleware and post-response hooks run.

This lifecycle gives Laravel a predictable execution model and clear extension points.

</details>

<details>
<summary>5. What is the Laravel service container?</summary>

#### Laravel

The Laravel service container is an IoC (Inversion of Control) container responsible for creating objects and managing dependencies.

1. **Core role**

- Central place where classes/interfaces are bound to concrete implementations.
- Automatically resolves constructor dependencies via reflection.

2. **Why it matters**

- Reduces manual object wiring.
- Enables dependency inversion (depend on interfaces, not concrete classes).
- Improves testability by swapping implementations (e.g., fakes/mocks).

3. **Where it is used**

- Controllers, middleware, jobs, listeners, commands, and service classes.
- Framework internals and custom app architecture.

4. **Common APIs**

- `bind()` for transient bindings.
- `singleton()` for one shared instance.
- `make()` / `app()` for resolving services.

5. **Practical effect**

- Cleaner constructors, less coupling, better modular design.

In Laravel, the service container is one of the main foundations for scalable application architecture.

</details>

<details>
<summary>6. Explain the difference between binding, singleton binding, and resolving in the service container.</summary>

#### Laravel

These terms describe different operations in Laravel’s container lifecycle.

1. **Binding (`bind`)**

- Registers how the container should build a type.
- Creates a **new instance on each resolve** (transient lifecycle).

```php
$this->app->bind(PaymentGateway::class, StripeGateway::class);
```

2. **Singleton binding (`singleton`)**

- Registers a type as a **shared instance**.
- First resolve creates it; subsequent resolves return the same object.

```php
$this->app->singleton(CacheClient::class, fn () => new CacheClient());
```

3. **Resolving (`make` / auto-injection)**

- The act of asking the container to provide an instance.
- Can happen explicitly (`app()->make(...)`) or implicitly via constructor injection.

```php
$gateway = app()->make(PaymentGateway::class);
```

4. **Rule of thumb**

- Use `bind` for stateless/light services.
- Use `singleton` for shared/heavy/stateful infrastructure clients.
- Prefer automatic resolving through dependency injection in framework-managed classes.

</details>

<details>
<summary>7. What is contextual binding and when would you use it?</summary>

#### Laravel

Contextual binding lets you provide different implementations of the same interface depending on which class is being resolved.

1. **Problem it solves**

- Multiple consumers need the same contract but different concrete behavior.

2. **Example scenario**

- `PhotoController` should use `S3Filesystem`.
- `ReportController` should use `LocalFilesystem`.
- Both depend on `FilesystemInterface`.

3. **Container API**

```php
$this->app->when(PhotoController::class)
    ->needs(FilesystemInterface::class)
    ->give(S3Filesystem::class);

$this->app->when(ReportController::class)
    ->needs(FilesystemInterface::class)
    ->give(LocalFilesystem::class);
```

4. **When to use**

- Multi-tenant or multi-region integrations.
- Different adapters for different use cases.
- Keeping interface-based design without global binding conflicts.

Contextual binding is useful when one global binding is not enough and behavior must vary by consumer context.

</details>

<details>
<summary>8. What are Service Providers and what is their purpose?</summary>

#### Laravel

Service Providers are the central bootstrap mechanism in Laravel for registering and configuring application services.

1. **Primary purpose**

- Register container bindings.
- Configure package/application services during startup.

2. **What typically goes there**

- Interface-to-implementation bindings.
- Singleton registrations for infrastructure services.
- Event/listener registration (or separate provider).
- Package bootstrapping and configuration wiring.

3. **Default examples**

- `AppServiceProvider`
- `RouteServiceProvider`
- Package providers

4. **Why it matters**

- Creates a predictable startup layer.
- Keeps bootstrapping logic out of controllers/models.
- Improves modularity and maintainability in large applications.

Service Providers are effectively the composition root of a Laravel application.

</details>

<details>
<summary>9. What is the difference between registering and booting in a service provider?</summary>

#### Laravel

In a Service Provider, `register()` and `boot()` run at different stages and have different responsibilities.

1. **`register()`**

- Used only to bind things into the container.
- Should be side-effect free and not depend on services from other providers being booted.

```php
public function register(): void
{
    $this->app->singleton(PaymentGateway::class, StripeGateway::class);
}
```

2. **`boot()`**

- Runs after all providers are registered.
- Used for actions requiring already-available services: routes, view composers, observers, event wiring, macros.

```php
public function boot(): void
{
    Schema::defaultStringLength(191);
}
```

3. **Practical distinction**

- `register()` = declare dependencies.
- `boot()` = execute framework integration logic.

Using this separation correctly prevents boot-order bugs and keeps startup behavior predictable.

</details>

<details>
<summary>10. What are Laravel Contracts?</summary>

#### Laravel

Laravel Contracts are framework-defined PHP interfaces that describe core service capabilities independently of implementations.

1. **What they are**

- Interfaces under `Illuminate\Contracts\...`.
- Examples: `Cache\Repository`, `Queue\Queue`, `Auth\Guard`, `Mail\Mailer`.

2. **Why they exist**

- Decouple your code from concrete framework classes.
- Enable clean dependency inversion and easier testing.
- Allow swapping implementations with minimal code changes.

3. **How they are used**

- Type-hint a contract in constructor/method.
- Let the container resolve the current implementation.

```php
use Illuminate\Contracts\Cache\Repository as Cache;

final class UserService
{
    public function __construct(private Cache $cache) {}
}
```

4. **Practical benefit**

- More maintainable architecture and clearer boundaries.
- Better mocks/fakes in tests.
- Easier migration of infrastructure details.

Contracts are a key building block for writing framework-friendly but implementation-agnostic Laravel code.

</details>

<details>
<summary>11. What is the difference between a Contract and a Facade?</summary>

#### Laravel

Contracts and Facades are related to Laravel services, but they solve different problems.

1. **Contract**

- A PHP interface (usually in `Illuminate\Contracts\...`).
- Defines behavior/capability without implementation details.
- Used for dependency inversion and clean architecture.

2. **Facade**

- A static-like proxy to a service resolved from the container.
- Provides concise syntax for calling framework services.
- Example: `Cache::get('key')`, `Log::info('...')`.

3. **Key difference**

- Contract = abstraction boundary (design-time dependency).
- Facade = convenience access layer (call-style API).

4. **Testing impact**

- Contracts are easy to mock via DI.
- Facades can be mocked too (`Facade::shouldReceive()`), but they are still a static-looking style.

5. **When to prefer which**

- Prefer Contracts in domain/application services.
- Use Facades in controllers, small glue code, or framework-centric areas where brevity helps.

In short: Contract defines *what* a service does, Facade provides *how conveniently* you call it.

</details>

<details>
<summary>12. Explain the difference between Facades and helper functions in Laravel.</summary>

#### Laravel

Both Facades and helpers provide concise syntax, but they differ in structure, discoverability, and test semantics.

1. **Facades**

- Class-based static proxy (`Cache::`, `DB::`, `Bus::`).
- Mapped to container services.
- Support facade mocking/faking APIs.
- Better IDE discoverability via class methods.

2. **Helper functions**

- Global functions like `app()`, `route()`, `now()`, `config()`, `request()`, `response()`.
- Very short and convenient in templates/controllers.
- Not tied to a class name in usage.

3. **Key differences**

- Facade: explicit service surface via class.
- Helper: lightweight global shortcut.

4. **Testing and architecture**

- In core business code, constructor DI is usually cleaner than either style.
- For framework glue code, both are acceptable; facades can be more explicit, helpers more concise.

5. **Practical guidance**

- Prefer DI + contracts in domain services.
- Use facades/helpers pragmatically in controllers, jobs, views, and framework integration code.

</details>

<details>
<summary>13. How does Dependency Injection work in Laravel?</summary>

#### Laravel

Laravel Dependency Injection (DI) is powered by the service container, which resolves class dependencies automatically.

1. **Constructor injection**

- You type-hint dependencies in a constructor.
- Laravel resolves and injects them when creating the class.

```php
final class OrderController
{
    public function __construct(private OrderService $service) {}
}
```

2. **Method injection**

- Works in controller actions, jobs handlers, listeners, commands, etc.
- Type-hinted parameters can be auto-resolved.

```php
public function store(StoreOrderRequest $request, OrderService $service): JsonResponse
{
    // ...
}
```

3. **Interface injection**

- If you inject an interface, bind it to a concrete class in a provider.

```php
$this->app->bind(PaymentGateway::class, StripeGateway::class);
```

4. **Why DI matters**

- Low coupling.
- Easy testing with mocks/fakes.
- Clear dependencies and better maintainability.

In Laravel, DI is the default way to wire application services cleanly.

</details>

<details>
<summary>14. How does Laravel use IoC (Inversion of Control)?</summary>

#### Laravel

Laravel applies IoC by delegating object creation and dependency wiring to the service container instead of hard-coding dependencies inside classes.

1. **Traditional (no IoC)**

- Class instantiates its own dependencies (`new StripeGateway()`), causing tight coupling.

2. **With IoC in Laravel**

- Classes declare required abstractions (interfaces/types).
- Container provides concrete implementations.

3. **Where IoC appears**

- Controllers, middleware, jobs, events/listeners, commands, policies, custom services.
- Framework internals also rely on the same mechanism.

4. **Benefits**

- Swappable implementations (e.g., Stripe vs PayPal).
- Better unit testing and modular architecture.
- Centralized configuration of object graph in providers.

IoC in Laravel is the architectural foundation behind DI, contracts, and testability.

</details>

<details>
<summary>15. What are middleware in Laravel?</summary>

#### Laravel

Middleware are classes that inspect, filter, or transform HTTP requests/responses as they pass through the request pipeline.

1. **Purpose**

- Execute cross-cutting concerns before/after controller logic.

2. **Common use cases**

- Authentication/authorization checks.
- Rate limiting.
- CSRF protection.
- Request logging and security headers.
- Localization and tenant/context setup.

3. **Execution model**

- Request enters middleware stack.
- Each middleware decides to continue (`$next($request)`) or stop (return response/redirect/error).
- Response can also be modified on the way back.

4. **Types**

- Global middleware (for all requests).
- Route middleware (assigned to specific routes/groups).

Middleware keep controllers focused by moving reusable HTTP concerns into dedicated pipeline layers.

</details>

<details>
<summary>16. How do you register and assign middleware?</summary>

#### Laravel

In modern Laravel, middleware is typically configured in bootstrap/application configuration and assigned by alias, group, or direct class.

1. **Register middleware aliases/groups**

- Define aliases and group composition in the application bootstrap middleware configuration.
- Typical aliases include `auth`, `verified`, `throttle`, etc.

2. **Global middleware**

- Added to the global stack so they run on every request.

3. **Assign to routes**

- Per route:

```php
Route::get('/profile', ProfileController::class)
    ->middleware('auth');
```

- Per group:

```php
Route::middleware(['auth', 'verified'])->group(function () {
    Route::get('/dashboard', DashboardController::class);
});
```

4. **By class name**

- You can also attach middleware class directly instead of alias when needed.

Practical approach: use aliases for readability and consistent usage across the codebase.

</details>

<details>
<summary>17. How does middleware work with parameters?</summary>

#### Laravel

Laravel middleware can accept parameters from route definitions, allowing configurable behavior without duplicating middleware classes.

1. **Route usage**

```php
Route::get('/admin', AdminController::class)
    ->middleware('role:admin');
```

2. **Middleware signature**

```php
public function handle(Request $request, Closure $next, string $role): Response
{
    if (! $request->user() || ! $request->user()->hasRole($role)) {
        abort(403);
    }

    return $next($request);
}
```

3. **Multiple parameters**

- Passed as comma-separated values: `middleware('throttle:60,1')`.
- Middleware receives them as additional arguments after `$next`.

4. **When useful**

- Role/permission checks.
- Rate limit variants.
- Feature or tenant constraints by route context.

Parameterized middleware improves reusability and keeps route-level intent explicit.

</details>

<details>
<summary>18. What are route groups, prefixes, and middleware groups?</summary>

#### Laravel

Route grouping helps organize routes and apply shared configuration once.

1. **Route groups**

- Combine routes under common attributes (`middleware`, `prefix`, `name`, `namespace`, etc.).

2. **Prefixes**

- Add URI prefix to all routes in the group.

```php
Route::prefix('api/v1')->group(function () {
    Route::get('/users', [UserController::class, 'index']);
});
```

3. **Name prefixes**

- Add common route name prefix.

```php
Route::name('admin.')->group(function () {
    Route::get('/dashboard', [AdminController::class, 'dashboard'])->name('dashboard');
});
// Route name: admin.dashboard
```

4. **Middleware groups**

- A named set of middleware (for example `web`, `api`) that can be applied together.
- Reduce repetition and standardize behavior across route sections.

5. **Why this matters**

- Cleaner route files.
- Consistent security and request handling rules.
- Easier maintenance as app grows.

</details>

<details>
<summary>19. What is route model binding?</summary>

#### Laravel

Route model binding automatically resolves route parameters into Eloquent model instances.

1. **What it does**

- Converts route segment like `{user}` into `User` model object.
- If not found, Laravel returns `404` automatically.

2. **Example**

```php
Route::get('/users/{user}', [UserController::class, 'show']);

public function show(User $user): View
{
    return view('users.show', compact('user'));
}
```

3. **Benefits**

- Removes repetitive `findOrFail()` boilerplate.
- Improves readability and type safety.
- Gives centralized control over lookup behavior.

4. **Advanced usage**

- Custom route keys (e.g., slug).
- Scoped/nested bindings for parent-child relations.

Route model binding is one of Laravel’s most useful conventions for concise, safe controller code.

</details>

<details>
<summary>20. Explain implicit vs explicit route model binding.</summary>

#### Laravel

Both approaches resolve route params to models, but they differ in configuration style.

1. **Implicit binding**

- Laravel infers binding from parameter name + type-hint.
- Minimal setup.

```php
Route::get('/posts/{post}', fn (Post $post) => $post);
```

2. **Explicit binding**

- You manually define how a parameter maps to a model.
- Useful for custom logic or non-standard resolution.

```php
Route::bind('post', function (string $value) {
    return Post::where('slug', $value)->firstOrFail();
});
```

3. **When to choose**

- Use implicit binding by default (clean and conventional).
- Use explicit binding for special lookup rules, custom transformations, or edge cases.

4. **Related customization**

- For many cases, overriding `getRouteKeyName()` in model (e.g., slug) is enough without full explicit binding.

Implicit = convention-based automatic binding. Explicit = manually controlled binding behavior.

</details>

<details>
<summary>21. What is rate limiting in Laravel and how does it work?</summary>

#### Laravel

Rate limiting controls how many requests a client can make in a time window to protect APIs from abuse and overload.

1. **What it does**

- Limits request frequency per key (user ID, IP, token, or custom identifier).
- Returns `429 Too Many Requests` when limit is exceeded.

2. **How Laravel implements it**

- Uses named limiters defined via `RateLimiter::for(...)`.
- Applies limiter through middleware (commonly `throttle`).
- Stores counters using cache backend (Redis/Memcached/database cache depending on setup).

3. **Basic example**

```php
RateLimiter::for('api', function (Request $request) {
    return Limit::perMinute(60)->by($request->user()?->id ?: $request->ip());
});
```

4. **Where to apply**

- Public API endpoints.
- Login, OTP, password reset, and other sensitive endpoints.
- Expensive operations (search, export, report generation).

5. **Why it matters**

- Improves reliability and fairness.
- Reduces brute-force risk and traffic spikes impact.

</details>

<details>
<summary>22. What are invokable controllers?</summary>

#### Laravel

Invokable controllers are controller classes with a single `__invoke()` method, designed for one specific action.

1. **Structure**

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

3. **Benefits**

- Very focused responsibility.
- Cleaner route-to-action mapping.
- Works well with action-oriented architecture.

4. **When useful**

- Endpoints with clear single purpose.
- CQRS/action-based style.
- Large codebases where smaller classes improve navigation.

Invokable controllers are a practical way to keep HTTP layer explicit and modular.

</details>

<details>
<summary>23. What are Single Action Controllers?</summary>

#### Laravel

Single Action Controllers are the same concept as invokable controllers: one controller class handles one action via `__invoke()`.

1. **Core idea**

- One class = one use case.
- No multiple methods like `index/store/update` in the same controller.

2. **Why teams use them**

- Better separation of concerns.
- Easier testing per endpoint.
- Reduced merge conflicts in large teams.

3. **Example use cases**

- `ApproveInvoiceController`
- `SendWelcomeEmailController`
- `GenerateReportController`

4. **Tradeoff**

- More files/classes.
- But usually better long-term maintainability for medium/large projects.

Single Action Controllers are essentially an architectural style choice that prioritizes clarity and scale.

</details>

<details>
<summary>24. What is the difference between Resource Controllers and API Resource Controllers?</summary>

#### Laravel

The difference is mostly about generated actions and intended response style.

1. **Resource Controller (`Route::resource`)**

- Generates full CRUD web routes:
  `index`, `create`, `store`, `show`, `edit`, `update`, `destroy`.
- Includes `create` and `edit` routes, typically for HTML forms/views.

2. **API Resource Controller (`Route::apiResource`)**

- Generates API-focused CRUD routes:
  `index`, `store`, `show`, `update`, `destroy`.
- Excludes `create` and `edit` (UI form pages not needed for APIs).

3. **Typical usage**

- `resource`: server-rendered web apps.
- `apiResource`: JSON APIs, mobile backends, SPA backends.

4. **Related concept**

- API responses are often formatted with `JsonResource` classes for consistent output contracts.

</details>

<details>
<summary>25. How do you create custom Artisan commands?</summary>

#### Laravel

Custom Artisan commands are CLI classes used for automation, maintenance, imports, and operational workflows.

1. **Generate command class**

```bash
php artisan make:command SyncInvoicesCommand
```

2. **Define signature and description**

```php
protected $signature = 'billing:sync {--dry-run}';
protected $description = 'Sync invoices from billing provider';
```

3. **Implement logic in `handle()`**

```php
public function handle(): int
{
    // command logic
    return self::SUCCESS;
}
```

4. **Use DI in command**

- Inject services via constructor or method-level resolution.

5. **Run command**

```bash
php artisan billing:sync --dry-run
```

6. **Optional scheduling**

- Register in scheduler to run automatically on cron.

Custom commands are ideal for repeatable backend operations and DevOps-friendly automation.

</details>

<details>
<summary>26. What are macros and when are they useful?</summary>

#### Laravel

Macros let you add custom methods to framework classes at runtime (macroable classes) without modifying framework source.

1. **Common macroable targets**

- `Collection`, `Str`, `ResponseFactory`, `Route`, etc.

2. **Example**

```php
use Illuminate\Support\Collection;

Collection::macro('toKeyValue', function (string $key, string $value) {
    return $this->mapWithKeys(fn ($item) => [$item[$key] => $item[$value]]);
});
```

3. **When useful**

- Repeating utility logic across codebase.
- Domain-specific collection/string helpers.
- Cleaner expressive APIs for common transformations.

4. **Best practices**

- Register macros in a service provider.
- Keep names clear to avoid collisions.
- Do not overuse; prefer normal classes for complex behavior.

Macros are best for small, reusable framework extensions with high call frequency.

</details>

<details>
<summary>27. What are Actions in Laravel architecture and when would you use them?</summary>

#### Laravel

Actions are focused classes that encapsulate a single business use case (application operation).

1. **What an Action is**

- A class like `CreateOrderAction`, `PublishPostAction`, `RefundPaymentAction`.
- Usually exposes one method (`handle()` or `execute()`).

2. **Why use Actions**

- Removes business logic from controllers/models.
- Reusable from HTTP controllers, jobs, console commands, and listeners.
- Easier unit testing with clear input/output.

3. **Typical structure**

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

4. **When to use**

- Non-trivial use cases with orchestration rules.
- Logic reused across multiple entry points.
- Teams adopting service/action or CQRS-like architecture.

Actions improve modularity and make business workflows explicit.

</details>

<details>
<summary>28. Explain the Repository Pattern and its benefits.</summary>

#### Laravel

Repository Pattern abstracts data access behind interfaces so business logic is not tightly coupled to ORM/query details.

1. **Core idea**

- Define contract (e.g., `OrderRepository`).
- Provide implementation (e.g., `EloquentOrderRepository`).
- Inject repository into services/actions.

2. **Benefits**

- Clear separation between domain/application logic and persistence.
- Easier testing with fake/in-memory repositories.
- Centralized complex query logic and caching strategies.
- Easier future changes to data source.

3. **Tradeoffs**

- Extra abstraction layer and more boilerplate.
- Not always necessary for simple CRUD-heavy apps.

4. **Pragmatic guidance**

- Use repositories where data access is complex or shared.
- Avoid over-engineering simple modules.

Repository Pattern is valuable when it reduces coupling and complexity, not when it only adds indirection.

</details>

<details>
<summary>29. What are Traits in PHP and how are they used in Laravel?</summary>

#### Laravel

Traits are PHP language units for horizontal code reuse across classes without inheritance.

1. **What traits provide**

- Reusable methods/properties included via `use`.
- Shared behavior for unrelated classes.

2. **Laravel usage examples**

- Framework traits such as `SoftDeletes`, `HasFactory`, `Notifiable`, `AuthorizesRequests`, `DispatchesJobs`, `ValidatesRequests`.

3. **Model example**

```php
use Illuminate\Database\Eloquent\SoftDeletes;

class Post extends Model
{
    use SoftDeletes;
}
```

4. **Best practices**

- Keep traits small and cohesive.
- Use traits for behavior reuse, not to hide oversized class responsibilities.
- Prefer composition/services for complex domain logic.

Traits are a practical reuse mechanism, heavily used in Laravel internals and application code.

</details>

<details>
<summary>30. What are the differences between Laravel and Lumen, and is Lumen still relevant in 2026?</summary>

#### Laravel

Laravel and Lumen share roots, but they target different development tradeoffs.

1. **Main differences**

- **Laravel**: full-featured framework (rich ecosystem, first-party packages, extensive conventions, broad integration support).
- **Lumen**: micro-framework variant focused on minimal footprint and simpler API-style setups.

2. **Architecture and ecosystem**

- Laravel has wider first-party package compatibility and more complete developer tooling.
- Lumen is intentionally slimmer and does not aim for full compatibility with the broader Laravel package surface.

3. **Performance context**

- Historically Lumen was chosen for lightweight APIs.
- In modern versions, Laravel performance improved significantly, reducing the practical gap for many workloads.

4. **Is Lumen relevant in 2026?**

- **For new projects:** generally **not recommended** by Laravel ecosystem guidance.
- **For existing systems:** still relevant if already in production and stable.
- **Default choice in 2026:** Laravel (with proper optimization) for most new API and web backends.

5. **Practical decision rule**

- Start new products on Laravel.
- Keep Lumen only when maintaining legacy services with clear operational reasons.

</details>

<details>
<summary>31. What is Eloquent ORM?</summary>

#### Laravel

Eloquent ORM is Laravel’s Active Record implementation for working with databases through PHP objects instead of raw SQL.

1. **What it provides**

- Model-to-table mapping.
- Query builder integration.
- Relationship management.
- Attribute casting, accessors/mutators, scopes, events.

2. **Why teams use it**

- Faster development with expressive syntax.
- Cleaner domain code for common CRUD workflows.
- Built-in conventions that reduce boilerplate.

3. **Example**

```php
$users = User::query()
    ->where('is_active', true)
    ->latest()
    ->take(10)
    ->get();
```

4. **Important note**

- Eloquent is great for most application use cases.
- For highly specialized/reporting queries, raw SQL or query builder can still be better.

Eloquent is the default data access layer in Laravel applications.

</details>

<details>
<summary>32. What are Eloquent Models?</summary>

#### Laravel

Eloquent Models are PHP classes that represent database tables and encapsulate data behavior.

1. **Core role**

- Each model typically maps to one table.
- Model instances represent individual rows.

2. **What models usually contain**

- Fillable/guarded attributes.
- Casts and date handling.
- Relationships.
- Scopes and domain-specific methods.

3. **Basic example**

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

4. **Why they matter**

- Centralize persistence logic and entity behavior.
- Improve readability and consistency in data operations.

Eloquent models are the primary building blocks for database-driven Laravel applications.

</details>

<details>
<summary>33. Explain one-to-one, one-to-many, many-to-many, and polymorphic relationships.</summary>

#### Laravel

Eloquent relationships define how models are connected in the data model.

1. **One-to-one (`hasOne` / `belongsTo`)**

- One record relates to exactly one record.
- Example: `User` has one `Profile`.

2. **One-to-many (`hasMany` / `belongsTo`)**

- One parent has multiple children.
- Example: `Post` has many `Comment`s.

3. **Many-to-many (`belongsToMany`)**

- Both sides can have many related records.
- Requires pivot table.
- Example: `User` belongs to many `Role`s.

4. **Polymorphic**

- A model can belong to more than one parent type through a shared interface.
- Example: `Comment` can belong to `Post` or `Video`.

5. **Why this matters**

- Relationships let you express domain structure clearly.
- Eloquent can load related data, constrain queries, and simplify joins.

Choosing the right relationship type is key to clean schema design and efficient querying.

</details>

<details>
<summary>34. What are polymorphic relationships and when would you use them?</summary>

#### Laravel

Polymorphic relationships allow one model to relate to multiple model types using one pair of columns (usually `*_type` and `*_id`).

1. **How it works**

- Child table stores parent type + parent ID.
- One child model can point to different parent models.

2. **Common examples**

- `Comment` on `Post`, `Video`, `Product`.
- `Image` attached to `User`, `Team`, `Article`.
- `Activity` targeting multiple entity types.

3. **Laravel relation methods**

- `morphTo` on child.
- `morphMany` / `morphOne` on parent.
- `morphToMany` / `morphedByMany` for polymorphic many-to-many.

4. **When to use**

- When behavior is shared across heterogeneous parent entities.
- When you want one reusable child table instead of many parallel tables.

5. **Tradeoff**

- More flexible schema, but can increase query complexity and require careful indexing.

Use polymorphic relations when they reduce duplication and match the domain model naturally.

</details>

<details>
<summary>35. What is eager loading?</summary>

#### Laravel

Eager loading means loading related models in advance as part of the main query flow, rather than loading each relation later per item.

1. **How to do it**

```php
$posts = Post::with(['author', 'comments'])->latest()->get();
```

2. **Why it matters**

- Reduces total query count.
- Prevents N+1 query issues.
- Improves response time and DB efficiency.

3. **Useful variants**

- Nested eager loading: `with('comments.user')`.
- Constrained eager loading with closures.
- Default eager loads via model `$with` when always needed.

Eager loading is a core optimization practice for Eloquent-based applications.

</details>

<details>
<summary>36. What is the N+1 query problem and how do you solve it?</summary>

#### Laravel

N+1 happens when you run 1 query for a list, then an additional query per item for related data.

1. **Typical scenario**

- Query 100 posts.
- Access `$post->author` in loop.
- Results in 101 queries (1 + 100).

2. **Why it is bad**

- Large query count.
- Higher latency and DB load.
- Poor scalability under traffic.

3. **How to solve in Laravel**

- Use eager loading with `with()`.

```php
$posts = Post::with('author')->get();
```

- Use `load()` / `loadMissing()` when you already have model collections.
- Use query profiling tools (Telescope/Debugbar/logging) to detect hotspots.

4. **Best practice**

- Anticipate needed relations at query time.
- Review loops over models for hidden lazy loads.

Solving N+1 is one of the highest-impact Eloquent performance improvements.

</details>

<details>
<summary>37. What is lazy eager loading?</summary>

#### Laravel

Lazy eager loading loads relationships after models are already retrieved, but still in bulk rather than per-model.

1. **When it is used**

- You fetched models first.
- Later decide which relations are needed.

2. **Methods**

- `load()` loads specified relations.
- `loadMissing()` loads only relations not already loaded.

```php
$posts = Post::latest()->take(50)->get();
$posts->load('author', 'comments');
```

3. **Why it helps**

- Avoids N+1 while keeping flexible control flow.
- Useful in conditional logic or layered services.

4. **Difference from eager loading**

- Eager loading: `with()` before query execution.
- Lazy eager loading: `load()` after query execution.

Lazy eager loading is a practical middle ground between flexibility and performance.

</details>

<details>
<summary>38. What are global scopes and local scopes?</summary>

#### Laravel

Scopes are reusable query constraints in Eloquent.

1. **Global scopes**

- Applied automatically to all queries for a model.
- Good for cross-cutting constraints (e.g., tenant isolation, soft delete behavior, active-only records).

2. **Local scopes**

- Explicitly called in queries when needed.
- Define focused reusable filters.

```php
public function scopePublished(Builder $query): Builder
{
    return $query->whereNotNull('published_at');
}

$posts = Post::published()->get();
```

3. **When to choose**

- Global scope: default business rule that should apply almost everywhere.
- Local scope: optional filter for specific use cases.

4. **Caution**

- Overusing global scopes can hide data unexpectedly; document them clearly.

Scopes improve consistency and reduce repeated query conditions.

</details>

<details>
<summary>39. What are query scopes?</summary>

#### Laravel

Query scopes are model methods that encapsulate reusable query constraints for cleaner and composable querying.

1. **Local query scope pattern**

- Method name starts with `scope`.
- Called without the prefix.

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

2. **Benefits**

- Reusable filters.
- More readable query chains.
- Centralized constraint logic.

3. **Practical use**

- Status filters (`active`, `published`, `archived`).
- Date windows (`recent`, `betweenDates`).
- Business constraints (`visibleTo`, `forTenant`).

Query scopes are a key tool for keeping Eloquent queries expressive and maintainable.

</details>

<details>
<summary>40. What are accessors and mutators?</summary>

#### Laravel

Accessors and mutators define how model attributes are transformed when reading and writing.

1. **Accessor**

- Transforms a value when it is retrieved from the model.

2. **Mutator**

- Transforms a value before it is stored on the model.

3. **Modern style (`Attribute`)**

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

4. **Typical use cases**

- Normalize input (trim/case formatting).
- Present computed/formatted values.
- Handle encryption/decryption transformations.

5. **Difference from casts**

- Casts handle common type conversion.
- Accessors/mutators handle custom domain-specific transformations.

They help keep attribute transformation logic centralized and consistent.

</details>

<details>
<summary>41. What are casts in Eloquent?</summary>

#### Laravel

Casts define how Eloquent converts model attributes between raw database values and PHP types.

1. **What casts do**

- Convert values on read/write automatically.
- Keep attribute handling consistent and type-safe.

2. **Common cast types**

- `integer`, `float`, `decimal:2`, `boolean`
- `datetime`, `immutable_datetime`
- `array`, `json`, `object`, `collection`
- `encrypted`, `hashed`

3. **Example**

```php
protected function casts(): array
{
    return [
        'is_active' => 'boolean',
        'price' => 'decimal:2',
        'meta' => 'array',
        'published_at' => 'datetime',
    ];
}
```

4. **Why it matters**

- Reduces manual parsing/formatting code.
- Prevents subtle type bugs.
- Improves readability of domain code.

Casts are a foundational feature for clean model attribute management.

</details>

<details>
<summary>42. What are Attribute objects in modern Laravel?</summary>

#### Laravel

`Attribute` objects are the modern way to define accessors and mutators in one place for a model field.

1. **Core idea**

- A method returns `Attribute::make(get: ..., set: ...)`.
- Encapsulates read/write transformations clearly.

2. **Example**

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

3. **Benefits**

- Cleaner than legacy `getXxxAttribute` / `setXxxAttribute` methods.
- Groups getter/setter behavior in one method.
- Easier to read, test, and maintain.

4. **When to use**

- Custom formatting, normalization, encryption logic, or value-object mapping on specific attributes.

Attribute objects are the preferred modern accessor/mutator pattern in current Laravel versions.

</details>

<details>
<summary>43. What are Eloquent Collections?</summary>

#### Laravel

Eloquent Collections are specialized collection objects returned by Eloquent queries, extending Laravel’s base `Collection` with model-aware behavior.

1. **What they are**

- Returned by methods like `get()` and relationship loads.
- Contain model instances, not plain arrays.

2. **Extra capabilities**

- Inherits rich collection API (`map`, `filter`, `groupBy`, `pluck`, etc.).
- Adds Eloquent-specific helpers like `load()`, `loadMissing()`, `modelKeys()`, `fresh()`.

3. **Example**

```php
$users = User::where('is_active', true)->get(); // Eloquent Collection
$emails = $users->pluck('email');
```

4. **Why useful**

- Expressive post-query transformations.
- Convenient bulk operations on model sets.

Eloquent Collections combine ORM awareness with functional-style data operations.

</details>

<details>
<summary>44. What is the difference between arrays and collections?</summary>

#### Laravel

Arrays are native PHP data structures, while Collections are object wrappers with a fluent API for transformations.

1. **Arrays**

- Fast native structure.
- Access via language syntax.
- Fewer high-level transformation helpers by default.

2. **Collections**

- `Illuminate\Support\Collection` object.
- Chainable methods: `map`, `filter`, `reduce`, `sortBy`, `groupBy`, etc.
- More expressive and readable for complex data pipelines.

3. **Example**

```php
$names = collect($users)
    ->filter(fn ($u) => $u->is_active)
    ->pluck('name')
    ->values();
```

4. **When to use which**

- Use arrays for simple, low-level operations.
- Use collections for readability and composable transformations.

Collections trade small overhead for much better ergonomics in application code.

</details>

<details>
<summary>45. What are Lazy Collections?</summary>

#### Laravel

Lazy Collections process items as a stream (generator-based) instead of loading all items into memory at once.

1. **Core property**

- Memory-efficient iteration over very large datasets.

2. **How they work**

- Items are generated and processed one by one.
- Transformation chain executes lazily during iteration.

3. **Typical sources**

- `lazy()` queries.
- `cursor()` from Eloquent/query builder.
- Custom generators wrapped in `LazyCollection`.

4. **When to use**

- Data migration scripts.
- Large exports/imports.
- Background jobs over millions of rows.

5. **Tradeoff**

- Some collection operations requiring full materialization are less suitable.

Lazy Collections are ideal when memory safety matters more than random-access convenience.

</details>

<details>
<summary>46. What is the purpose of the cursor() method?</summary>

#### Laravel

`cursor()` returns a lazy iterable of results, letting you loop through records one at a time with low memory usage.

1. **Why use it**

- Avoid loading full result set into RAM.
- Process large tables efficiently.

2. **Example**

```php
foreach (User::where('is_active', true)->cursor() as $user) {
    // process user
}
```

3. **Characteristics**

- Generator-based iteration.
- Good for read/process pipelines.
- Works well with queues and long-running jobs.

4. **When not ideal**

- If you need random access to all results at once.
- If you need heavy eager-loaded graph materialization for all records.

`cursor()` is a key tool for scalable record-by-record processing.

</details>

<details>
<summary>47. What is chunking and when should you use chunk() or lazy()?</summary>

#### Laravel

Chunking means processing query results in small batches instead of loading everything at once.

1. **`chunk()`**

- Fetches records in fixed-size batches and executes callback per chunk.

```php
User::query()->chunk(1000, function ($users) {
    foreach ($users as $user) {
        // process
    }
});
```

2. **`lazy()`**

- Internally chunked, but exposed as a single lazy stream.
- More composable for pipeline-style code.

```php
User::query()->lazy(1000)->each(function (User $user) {
    // process
});
```

3. **When to choose**

- Use `chunk()` for explicit per-batch operations.
- Use `lazy()` for fluent streaming transformations.

4. **Important note**

- When updating rows during iteration, prefer ID-based variants (`chunkById`, `lazyById`) to avoid skipping/duplicating rows.

Chunking is essential for large dataset processing with controlled memory usage.

</details>

<details>
<summary>48. Explain query builder in Laravel.</summary>

#### Laravel

Laravel Query Builder is a fluent SQL query construction API that works above PDO and below Eloquent models.

1. **What it is**

- Database-agnostic query interface via `DB::table(...)`.
- Supports select, joins, where clauses, grouping, ordering, pagination, inserts/updates/deletes.

2. **Example**

```php
$users = DB::table('users')
    ->select('id', 'name', 'email')
    ->where('is_active', true)
    ->orderByDesc('created_at')
    ->limit(20)
    ->get();
```

3. **Why use it**

- More control over SQL than high-level ORM patterns.
- Great for reporting queries and complex joins.
- Still supports binding and SQL injection-safe parameter handling.

4. **Eloquent vs builder**

- Eloquent: model-centric, rich domain features.
- Query Builder: table/query-centric, lower-level and often leaner.

Query Builder is the core fluent layer for precise SQL work in Laravel.

</details>

<details>
<summary>49. How do you output raw SQL queries in Laravel?</summary>

#### Laravel

You can inspect SQL and bindings in several ways depending on debugging depth.

1. **`toSql()` + `getBindings()`**

```php
$query = User::where('email', 'like', '%@example.com%');

$sql = $query->toSql();
$bindings = $query->getBindings();
```

2. **`toRawSql()` (modern Laravel)**

- Returns SQL with bindings interpolated for easier reading.

```php
$sql = User::where('id', 5)->toRawSql();
```

3. **Query listener**

```php
DB::listen(function ($query) {
    logger()->debug($query->sql, $query->bindings);
});
```

4. **Tooling**

- Laravel Telescope / Debugbar can show executed queries and timings.

Use these methods in development/debugging, not as permanent production output.

</details>

<details>
<summary>50. What aggregate methods are available in query builder?</summary>

#### Laravel

Laravel Query Builder provides standard SQL aggregate helpers.

1. **Main aggregate methods**

- `count()`
- `sum($column)`
- `avg($column)` / `average($column)`
- `min($column)`
- `max($column)`

2. **Examples**

```php
$totalUsers = DB::table('users')->count();
$totalRevenue = DB::table('orders')->sum('amount');
$avgOrder = DB::table('orders')->avg('amount');
$firstDate = DB::table('orders')->min('created_at');
$latestDate = DB::table('orders')->max('created_at');
```

3. **With grouped queries**

- Combine `selectRaw(...)` + `groupBy(...)` for per-group aggregates.

4. **Why useful**

- Efficient server-side calculations.
- Avoid transferring unnecessary rows into application memory.

Aggregates are essential for dashboards, analytics, and business metrics endpoints.

</details>
