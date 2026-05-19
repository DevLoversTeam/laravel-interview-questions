**Read in other languages: [English 🇺🇸](README.en.md),
[Polska 🇵🇱](README.pl.md), [German 🇩🇪](README.de.md), [French 🇫🇷](README.fr.md),
[Spanish 🇪🇸](README.es.md), [Українська 🇺🇦](README.md).**

<h1>
  Laravel <img src="./assets/laravel.svg" width="40" height="40" alt="Laravel logo"/>
</h1>

<h2>Найпопулярніші запитання та відповіді на співбесіді з Laravel</h2>

<details>
<summary>1. Що таке Laravel і чому його використовують?</summary>

#### Laravel

Laravel — це сучасний PHP-фреймворк для веброзробки, орієнтований на продуктивність розробника, чисту архітектуру та підтримуваний код.

1. **Що таке Laravel**

- Відкритий фреймворк, побудований на компонентах Symfony.
- Достатньо opinionated, щоб давати сильні стандартні рішення, але водночас гнучкий для кастомної архітектури.

2. **Чому його використовують**

- Прискорює розробку завдяки вбудованим механізмам маршрутизації, валідації, автентифікації, черг, пошти, подій і кешування.
- Сприяє чистому коду через сервісний контейнер, middleware, Eloquent ORM та інструменти тестування.
- Надає офіційні інструменти (`Artisan`, міграції, планувальник, Horizon, Telescope) для production-ready застосунків.

3. **Типові сценарії використання**

- REST API та бекенд-сервіси.
- Серверно-рендерені вебзастосунки.
- Адмінпанелі, SaaS-продукти та маркетплейси.
- Фонова обробка задач і інтеграції зі сторонніми сервісами.

Коротко: Laravel використовують, щоб швидше будувати безпечні, масштабовані й підтримувані PHP-застосунки з меншим обсягом шаблонного коду.

</details>

<details>
<summary>19. Що таке route model binding?</summary>

#### Laravel

Route model binding автоматично перетворює параметри маршруту на екземпляри Eloquent-моделей.

1. **Що це робить**

- Конвертує сегмент маршруту на кшталт `{user}` в об’єкт `User`.
- Якщо запис не знайдено, Laravel автоматично повертає `404`.

2. **Приклад**

```php
Route::get('/users/{user}', [UserController::class, 'show']);

public function show(User $user): View
{
    return view('users.show', compact('user'));
}
```

3. **Переваги**

- Прибирає повторюваний `findOrFail()` boilerplate.
- Підвищує читабельність і type safety.
- Дає централізований контроль над поведінкою пошуку.

4. **Розширене використання**

- Кастомні route keys (наприклад, slug).
- Scoped/nested binding для батьківсько-дочірніх зв’язків.

Route model binding — одна з найкорисніших конвенцій Laravel для стислого й безпечного коду контролерів.

</details>

<details>
<summary>18. Що таке route groups, prefixes і middleware groups?</summary>

#### Laravel

Групування маршрутів допомагає структурувати роутинґ і застосовувати спільні налаштування один раз.

1. **Route groups**

- Об’єднують маршрути під спільними атрибутами (`middleware`, `prefix`, `name`, `namespace` тощо).

2. **Prefixes**

- Додають URI-префікс до всіх маршрутів у групі.

```php
Route::prefix('api/v1')->group(function () {
    Route::get('/users', [UserController::class, 'index']);
});
```

3. **Name prefixes**

- Додають спільний префікс до імен маршрутів.

```php
Route::name('admin.')->group(function () {
    Route::get('/dashboard', [AdminController::class, 'dashboard'])->name('dashboard');
});
// Ім’я маршруту: admin.dashboard
```

4. **Middleware groups**

- Іменований набір middleware (наприклад, `web`, `api`), який можна застосувати одним викликом.
- Зменшує повторення й стандартизує поведінку для секцій маршрутів.

5. **Чому це важливо**

- Чистіші route-файли.
- Узгоджені правила безпеки та обробки запитів.
- Простіша підтримка зі зростанням застосунку.

</details>

<details>
<summary>17. Як middleware працює з параметрами?</summary>

#### Laravel

Laravel middleware може приймати параметри з route-оголошення, що дозволяє конфігурувати поведінку без дублювання middleware-класів.

1. **Використання в маршруті**

```php
Route::get('/admin', AdminController::class)
    ->middleware('role:admin');
```

2. **Сигнатура middleware**

```php
public function handle(Request $request, Closure $next, string $role): Response
{
    if (! $request->user() || ! $request->user()->hasRole($role)) {
        abort(403);
    }

    return $next($request);
}
```

3. **Кілька параметрів**

- Передаються через кому: `middleware('throttle:60,1')`.
- Middleware отримує їх як додаткові аргументи після `$next`.

4. **Коли це корисно**

- Перевірки ролей/прав доступу.
- Варіанти rate limiting.
- Feature- або tenant-обмеження залежно від route-контексту.

Параметризовані middleware підвищують повторне використання й роблять намір на рівні маршрутів явним.

</details>

<details>
<summary>16. Як зареєструвати та призначити middleware?</summary>

#### Laravel

У сучасному Laravel middleware зазвичай конфігуруються в bootstrap-конфігурації застосунку й призначаються через alias, group або напряму через клас.

1. **Реєстрація alias/group**

- Визначте aliases і склад груп у конфігурації middleware на етапі bootstrap.
- Типові aliases: `auth`, `verified`, `throttle` тощо.

2. **Global middleware**

- Додаються до global-стека й виконуються для кожного запиту.

3. **Призначення маршрутам**

- Для окремого маршруту:

```php
Route::get('/profile', ProfileController::class)
    ->middleware('auth');
```

- Для групи маршрутів:

```php
Route::middleware(['auth', 'verified'])->group(function () {
    Route::get('/dashboard', DashboardController::class);
});
```

4. **Призначення через ім’я класу**

- За потреби middleware можна навішувати напряму через class name, а не alias.

Практичний підхід: використовуйте aliases для читабельності та єдиного стилю в кодовій базі.

</details>

<details>
<summary>15. Що таке middleware у Laravel?</summary>

#### Laravel

Middleware — це класи, які перевіряють, фільтрують або трансформують HTTP-запити/відповіді під час проходження через request pipeline.

1. **Призначення**

- Виконувати наскрізну логіку до/після контролерної логіки.

2. **Типові use case**

- Перевірка автентифікації/авторизації.
- Rate limiting.
- CSRF-захист.
- Логування запитів і security headers.
- Локалізація та встановлення tenant/context.

3. **Модель виконання**

- Запит заходить у стек middleware.
- Кожен middleware або пропускає далі (`$next($request)`), або зупиняє потік (повертає response/redirect/error).
- Відповідь також може модифікуватися на зворотному шляху.

4. **Типи**

- Global middleware (для всіх запитів).
- Route middleware (для конкретних маршрутів/груп).

Middleware дає змогу тримати контролери сфокусованими, виносячи повторювану HTTP-логіку в окремі pipeline-шари.

</details>

<details>
<summary>14. Як Laravel використовує IoC (Inversion of Control)?</summary>

#### Laravel

Laravel застосовує IoC, передаючи створення об’єктів і зв’язування залежностей сервісному контейнеру, замість жорсткого створення залежностей усередині класів.

1. **Традиційний підхід (без IoC)**

- Клас сам інстанціює залежності (`new StripeGateway()`), що створює сильну зв’язаність.

2. **IoC у Laravel**

- Класи оголошують потрібні абстракції (інтерфейси/типи).
- Контейнер надає конкретні реалізації.

3. **Де це проявляється**

- Контролери, middleware, jobs, events/listeners, commands, policies, кастомні сервіси.
- Внутрішні частини фреймворку також працюють за цим принципом.

4. **Переваги**

- Замінність реалізацій (наприклад, Stripe vs PayPal).
- Краще unit-тестування й модульна архітектура.
- Централізоване налаштування object graph у providers.

IoC у Laravel — архітектурна основа для DI, contracts і тестованості.

</details>

<details>
<summary>13. Як працює Dependency Injection у Laravel?</summary>

#### Laravel

Dependency Injection (DI) у Laravel працює через сервісний контейнер, який автоматично резолвить залежності класів.

1. **Ін’єкція через конструктор**

- Ви type-hint-ите залежності в конструкторі.
- Laravel резолвить і підставляє їх під час створення класу.

```php
final class OrderController
{
    public function __construct(private OrderService $service) {}
}
```

2. **Ін’єкція в метод**

- Працює в controller actions, handlers job-ів, listeners, commands тощо.
- Параметри з type-hint можуть резолвитися автоматично.

```php
public function store(StoreOrderRequest $request, OrderService $service): JsonResponse
{
    // ...
}
```

3. **Ін’єкція інтерфейсів**

- Якщо інжектите інтерфейс, прив’яжіть його до concrete-класу в provider.

```php
$this->app->bind(PaymentGateway::class, StripeGateway::class);
```

4. **Чому DI важливий**

- Низька зв’язаність.
- Просте тестування з mocks/fakes.
- Явні залежності й краща підтримуваність.

У Laravel DI — це базовий спосіб чисто з’єднувати сервіси застосунку.

</details>

<details>
<summary>12. Поясніть різницю між Facades і helper-функціями в Laravel.</summary>

#### Laravel

І Facades, і helpers дають короткий синтаксис, але відрізняються структурою, прозорістю та підходом до тестування.

1. **Facades**

- Класовий статичний проксі (`Cache::`, `DB::`, `Bus::`).
- Прив’язані до сервісів контейнера.
- Підтримують facade mocking/faking API.
- Краще IDE-discoverability через методи класу.

2. **Helper-функції**

- Глобальні функції на кшталт `app()`, `route()`, `now()`, `config()`, `request()`, `response()`.
- Дуже короткі й зручні в шаблонах/контролерах.
- У використанні не прив’язані до імені класу.

3. **Ключові відмінності**

- Facade: явна поверхня сервісу через клас.
- Helper: легковаговий глобальний шорткат.

4. **Тестування та архітектура**

- У core business-коді constructor DI зазвичай чистіший, ніж обидва підходи.
- Для framework glue-коду обидва варіанти прийнятні; facades зазвичай явніші, helpers — лаконічніші.

5. **Практична рекомендація**

- В domain-сервісах надавайте перевагу DI + contracts.
- У контролерах, jobs, views і фреймворк-інтеграціях використовуйте facades/helpers прагматично.

</details>

<details>
<summary>11. У чому різниця між Contract і Facade?</summary>

#### Laravel

Contracts і Facades пов’язані з сервісами Laravel, але вирішують різні задачі.

1. **Contract**

- PHP-інтерфейс (зазвичай у `Illuminate\Contracts\...`).
- Описує поведінку/можливість без деталей реалізації.
- Використовується для dependency inversion і чистої архітектури.

2. **Facade**

- “Статичний” проксі до сервісу, який резолвиться з контейнера.
- Дає короткий синтаксис для викликів фреймворк-сервісів.
- Приклад: `Cache::get('key')`, `Log::info('...')`.

3. **Ключова відмінність**

- Contract = абстракційна межа (залежність на рівні дизайну).
- Facade = зручний шар доступу (викличний API-стиль).

4. **Вплив на тестування**

- Contracts легко мокати через DI.
- Facades також можна мокати (`Facade::shouldReceive()`), але це все ще “статично-подібний” стиль.

5. **Коли що обирати**

- Віддавайте перевагу Contracts у domain/application сервісах.
- Використовуйте Facades у контролерах, невеликому glue-коді або фреймворк-орієнтованих ділянках, де важлива стислість.

Коротко: Contract визначає, *що* робить сервіс, а Facade — *наскільки зручно* ви його викликаєте.

</details>

<details>
<summary>10. Що таке Laravel Contracts?</summary>

#### Laravel

Laravel Contracts — це визначені фреймворком PHP-інтерфейси, які описують можливості core-сервісів незалежно від їхніх реалізацій.

1. **Що це таке**

- Інтерфейси в просторі імен `Illuminate\Contracts\...`.
- Приклади: `Cache\Repository`, `Queue\Queue`, `Auth\Guard`, `Mail\Mailer`.

2. **Навіщо вони існують**

- Розв’язують ваш код від конкретних класів фреймворку.
- Дають чистий dependency inversion і спрощують тестування.
- Дозволяють змінювати реалізації з мінімальними змінами коду.

3. **Як використовуються**

- Type-hint контракт у конструкторі/методі.
- Дозвольте контейнеру зарезолвити поточну реалізацію.

```php
use Illuminate\Contracts\Cache\Repository as Cache;

final class UserService
{
    public function __construct(private Cache $cache) {}
}
```

4. **Практична користь**

- Більш підтримувана архітектура й чіткіші межі між шарами.
- Кращі mocks/fakes у тестах.
- Простіша заміна інфраструктурних деталей.

Contracts — один із ключових будівельних блоків для написання Laravel-сумісного, але implementation-agnostic коду.

</details>

<details>
<summary>9. У чому різниця між registering і booting у service provider?</summary>

#### Laravel

У Service Provider методи `register()` і `boot()` виконуються на різних етапах і мають різні обов’язки.

1. **`register()`**

- Використовується лише для реєстрації прив’язок у контейнері.
- Має бути без побічних ефектів і не повинен залежати від того, що сервіси інших провайдерів уже boot-нулися.

```php
public function register(): void
{
    $this->app->singleton(PaymentGateway::class, StripeGateway::class);
}
```

2. **`boot()`**

- Виконується після того, як усі провайдери зареєстровані.
- Використовується для дій, яким потрібні вже доступні сервіси: routes, view composers, observers, event wiring, macros.

```php
public function boot(): void
{
    Schema::defaultStringLength(191);
}
```

3. **Практична відмінність**

- `register()` = оголошення залежностей.
- `boot()` = виконання логіки інтеграції з фреймворком.

Коректне розділення цих етапів запобігає помилкам порядку ініціалізації та робить старт застосунку передбачуваним.

</details>

<details>
<summary>8. Що таке Service Providers і яка їхня мета?</summary>

#### Laravel

Service Providers — це центральний механізм bootstrap у Laravel для реєстрації та конфігурації сервісів застосунку.

1. **Основне призначення**

- Реєструвати прив’язки в контейнері.
- Конфігурувати сервіси пакета/застосунку під час старту.

2. **Що зазвичай розміщують у них**

- Прив’язки інтерфейсів до реалізацій.
- Реєстрацію singleton для інфраструктурних сервісів.
- Реєстрацію event/listener (або у спеціалізованому провайдері).
- Bootstrap пакета й wiring конфігурації.

3. **Типові приклади**

- `AppServiceProvider`
- `RouteServiceProvider`
- Провайдери пакетів

4. **Чому це важливо**

- Формує передбачуваний стартовий шар застосунку.
- Виносить bootstrap-логіку з контролерів/моделей.
- Підвищує модульність і підтримуваність у великих проєктах.

Service Providers — фактично composition root застосунку на Laravel.

</details>

<details>
<summary>7. Що таке contextual binding і коли його варто використовувати?</summary>

#### Laravel

Contextual binding дозволяє надавати різні реалізації одного інтерфейсу залежно від того, який саме клас зараз резолвиться.

1. **Яку проблему вирішує**

- Кілька споживачів потребують той самий контракт, але з різною конкретною поведінкою.

2. **Приклад сценарію**

- `PhotoController` має використовувати `S3Filesystem`.
- `ReportController` має використовувати `LocalFilesystem`.
- Обидва залежать від `FilesystemInterface`.

3. **Container API**

```php
$this->app->when(PhotoController::class)
    ->needs(FilesystemInterface::class)
    ->give(S3Filesystem::class);

$this->app->when(ReportController::class)
    ->needs(FilesystemInterface::class)
    ->give(LocalFilesystem::class);
```

4. **Коли використовувати**

- Multi-tenant або multi-region інтеграції.
- Різні адаптери для різних use case.
- Коли інтерфейсна архітектура потрібна, але глобальної прив’язки недостатньо.

Contextual binding корисний тоді, коли однієї глобальної прив’язки мало, і поведінка має відрізнятися залежно від контексту споживача.

</details>

<details>
<summary>6. Поясніть різницю між binding, singleton binding і resolving у сервісному контейнері.</summary>

#### Laravel

Ці терміни описують різні операції в життєвому циклі контейнера Laravel.

1. **Binding (`bind`)**

- Реєструє, як контейнер має створювати тип.
- Створює **новий екземпляр при кожному резолві** (transient lifecycle).

```php
$this->app->bind(PaymentGateway::class, StripeGateway::class);
```

2. **Singleton binding (`singleton`)**

- Реєструє тип як **спільний екземпляр**.
- Під час першого резолву створює об’єкт, під час наступних повертає той самий.

```php
$this->app->singleton(CacheClient::class, fn () => new CacheClient());
```

3. **Resolving (`make` / auto-injection)**

- Сам факт запиту до контейнера, щоб отримати екземпляр.
- Може бути явним (`app()->make(...)`) або неявним через constructor injection.

```php
$gateway = app()->make(PaymentGateway::class);
```

4. **Практичне правило**

- Використовуйте `bind` для stateless/легких сервісів.
- Використовуйте `singleton` для спільних/важких/інфраструктурних клієнтів.
- Віддавайте перевагу автоматичному resolving через dependency injection у класах, якими керує фреймворк.

</details>

<details>
<summary>5. Що таке сервісний контейнер Laravel?</summary>

#### Laravel

Сервісний контейнер Laravel — це IoC-контейнер (Inversion of Control), який відповідає за створення об’єктів і керування залежностями.

1. **Ключова роль**

- Централізоване місце, де класи/інтерфейси прив’язуються до конкретних реалізацій.
- Автоматично резолвить залежності конструктора через reflection.

2. **Чому це важливо**

- Зменшує ручне “зшивання” об’єктів.
- Дає dependency inversion (залежність від інтерфейсів, а не конкретних класів).
- Підвищує тестованість завдяки простій заміні реалізацій (наприклад, fakes/mocks).

3. **Де використовується**

- Контролери, middleware, jobs, listeners, commands і service-класи.
- Внутрішні механізми фреймворку та кастомна архітектура застосунку.

4. **Поширені API**

- `bind()` для transient-прив’язок.
- `singleton()` для єдиного спільного екземпляра.
- `make()` / `app()` для резолву сервісів.

5. **Практичний ефект**

- Чистіші конструктори, менша зв’язаність, кращий модульний дизайн.

У Laravel сервісний контейнер є однією з базових основ масштабованої архітектури застосунку.

</details>

<details>
<summary>4. Опишіть життєвий цикл запиту в застосунку Laravel.</summary>

#### Laravel

Життєвий цикл запиту в Laravel описує, як вхідний HTTP-запит перетворюється на HTTP-відповідь.

1. **Точка входу**

- Вебсервер спрямовує запити в `public/index.php`.
- Завантажуються Composer autoloader і bootstrap Laravel-застосунку.

2. **Запуск HTTP kernel**

- Ініціалізується сервісний контейнер.
- Готуються global і route middleware-ланцюжки.

3. **Service providers**

- Провайдери реєструються та boot-яться.
- Стають доступними core-сервіси й прив’язки застосунку.

4. **Фаза маршрутизації**

- Router знаходить маршрут за методом + URI.
- Виконується middleware pipeline маршруту.

5. **Виконання контролера/обробника**

- Викликається action контролера, closure або invokable-клас.
- Залежності автоматично резолвляться з контейнера.
- Виконуються валідація, авторизація, бізнес-логіка та доступ до даних.

6. **Формування відповіді**

- Обробник повертає `Response`, `JsonResponse`, view, redirect або серіалізовані дані.
- Laravel нормалізує результат у HTTP response object.

7. **Фаза завершення**

- Відповідь надсилається клієнту.
- Виконуються terminable middleware і post-response хуки.

Цей цикл дає Laravel передбачувану модель виконання та чіткі точки розширення.

</details>

<details>
<summary>3. Як Laravel дотримується архітектури MVC?</summary>

#### Laravel

Laravel дотримується MVC (Model-View-Controller), розділяючи доменну/дану логіку, обробку запиту та презентаційний шар.

1. **Model (M)**

- Зазвичай це Eloquent-моделі в `app/Models`.
- Представляють доменні сутності та записи бази даних.
- Містять зв’язки, scope-и, casts і доменну поведінку.

2. **View (V)**

- Blade-шаблони в `resources/views`.
- Відповідають лише за відображення.
- Отримують підготовлені дані з контролерів або view-моделей.

3. **Controller (C)**

- Класи в `app/Http/Controllers`.
- Обробляють HTTP-запити, координують валідацію/сервіси й повертають відповіді.
- Мають залишатися “тонкими”: оркестрація, а не важка бізнес-логіка.

4. **Потік запиту в термінах MVC**

- Route зіставляє URL з action контролера.
- Контролер використовує моделі/сервіси для виконання use case.
- Контролер повертає view (HTML) або JSON-відповідь (API).

Laravel також підтримує service-класи, actions, repositories і доменні шари поверх MVC для більших застосунків.

</details>

<details>
<summary>2. Які головні переваги Laravel порівняно з іншими PHP-фреймворками?</summary>

#### Laravel

Головні переваги Laravel пов’язані з сильним developer experience, багатою вбудованою функціональністю та великим екосистемним оточенням.

1. **Зручність для розробника**

- Послідовний і виразний дизайн API в компонентах фреймворку.
- Якісна документація та простий онбординг.
- Швидке створення каркасу застосунку й CLI-процеси через `Artisan`.

2. **“Batteries included”**

- Першокласна підтримка маршрутизації, валідації, автентифікації, черг, подій, сповіщень, кешування та планування задач.
- ORM (Eloquent) і міграції схеми доступні “з коробки”.

3. **Архітектура та підтримуваність**

- Сервісний контейнер і dependency injection глибоко інтегровані.
- Middleware і service providers явно оформлюють наскрізні аспекти.
- Сильна підтримка тестування через інтеграцію PHPUnit/Pest.

4. **Сила екосистеми**

- Офіційні інструменти: Forge, Vapor, Horizon, Telescope, Octane, Sanctum, Passport, Cashier.
- Зрілі community-пакети та довготривала стабільність екосистеми.

5. **Операційна продуктивність**

- Зручні CI/CD і deployment-процеси.
- Якісна підтримка черг, кешування, Redis та моніторингу.

Laravel часто обирають тоді, коли команді потрібно швидко постачати бізнес-функціонал без втрати якості коду та довгострокової підтримуваності.

</details>
