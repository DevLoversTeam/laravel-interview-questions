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
<summary>44. У чому різниця між масивами й колекціями?</summary>

#### Laravel

Масиви — це нативна структура даних PHP, а колекції — об’єктні обгортки з fluent API для трансформацій.

1. **Масиви**

- Швидка нативна структура.
- Доступ через синтаксис мови.
- Менше високорівневих інструментів трансформації “з коробки”.

2. **Колекції**

- Об’єкти `Illuminate\Support\Collection`.
- Chainable-методи: `map`, `filter`, `reduce`, `sortBy`, `groupBy` тощо.
- Виразніші й читабельніші для складних пайплайнів обробки даних.

3. **Приклад**

```php
$names = collect($users)
    ->filter(fn ($u) => $u->is_active)
    ->pluck('name')
    ->values();
```

4. **Коли що використовувати**

- Масиви — для простих, низькорівневих операцій.
- Колекції — для читабельності та композиційних трансформацій.

Колекції дають невеликий оверхед, але значно кращу ергономіку в прикладному коді.

</details>

<details>
<summary>43. Що таке Eloquent Collections?</summary>

#### Laravel

Eloquent Collections — це спеціалізовані колекції, які повертаються Eloquent-запитами й розширюють базову `Collection` можливостями, орієнтованими на моделі.

1. **Що це таке**

- Повертаються методами на кшталт `get()` та під час завантаження relationships.
- Містять екземпляри моделей, а не звичайні масиви.

2. **Додаткові можливості**

- Наслідують багатий API колекцій (`map`, `filter`, `groupBy`, `pluck` тощо).
- Додають Eloquent-специфічні helper-и: `load()`, `loadMissing()`, `modelKeys()`, `fresh()`.

3. **Приклад**

```php
$users = User::where('is_active', true)->get(); // Eloquent Collection
$emails = $users->pluck('email');
```

4. **Чому це корисно**

- Виразні post-query трансформації.
- Зручні пакетні операції над наборами моделей.

Eloquent Collections поєднують ORM-обізнаність із функціональним стилем обробки даних.

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
<summary>20. Поясніть implicit vs explicit route model binding.</summary>

#### Laravel

Обидва підходи резолвлять параметри маршруту в моделі, але відрізняються стилем конфігурації.

1. **Implicit binding**

- Laravel сам виводить прив’язку з імені параметра + type-hint.
- Мінімум налаштувань.

```php
Route::get('/posts/{post}', fn (Post $post) => $post);
```

2. **Explicit binding**

- Ви вручну визначаєте, як параметр мапиться на модель.
- Корисно для кастомної логіки або нестандартного резолву.

```php
Route::bind('post', function (string $value) {
    return Post::where('slug', $value)->firstOrFail();
});
```

3. **Коли що обирати**

- За замовчуванням використовуйте implicit binding (чисто й конвенційно).
- Explicit binding застосовуйте для особливих правил пошуку, трансформацій або edge case.

4. **Пов’язане налаштування**

- У багатьох випадках достатньо перевизначити `getRouteKeyName()` у моделі (наприклад, для slug), без повного explicit binding.

Implicit = автоматична прив’язка за конвенцією. Explicit = ручний контроль логіки прив’язки.

</details>

<details>
<summary>21. Що таке rate limiting у Laravel і як він працює?</summary>

#### Laravel

Rate limiting обмежує кількість запитів, які клієнт може виконати за певний проміжок часу, щоб захистити API від зловживань і перевантаження.

1. **Що він робить**

- Обмежує частоту запитів за ключем (ID користувача, IP, токен або кастомний ідентифікатор).
- Повертає `429 Too Many Requests`, якщо ліміт перевищено.

2. **Як Laravel це реалізує**

- Використовує іменовані лімітери, визначені через `RateLimiter::for(...)`.
- Застосовує лімітер через middleware (зазвичай `throttle`).
- Зберігає лічильники в cache-backend (Redis/Memcached/database cache залежно від конфігурації).

3. **Базовий приклад**

```php
RateLimiter::for('api', function (Request $request) {
    return Limit::perMinute(60)->by($request->user()?->id ?: $request->ip());
});
```

4. **Де застосовувати**

- Публічні API-ендпоінти.
- Login, OTP, reset password та інші чутливі ендпоінти.
- Дорогі операції (пошук, експорт, генерація звітів).

5. **Чому це важливо**

- Підвищує надійність і справедливість доступу.
- Зменшує ризики brute-force атак і наслідки пікового трафіку.

</details>

<details>
<summary>22. Що таке invokable controllers?</summary>

#### Laravel

Invokable controllers — це контролери з одним методом `__invoke()`, які призначені для виконання однієї конкретної дії.

1. **Структура**

```php
final class PublishPostController
{
    public function __invoke(Post $post): JsonResponse
    {
        // ...
    }
}
```

2. **Маршрутизація**

```php
Route::post('/posts/{post}/publish', PublishPostController::class);
```

3. **Переваги**

- Дуже сфокусована відповідальність.
- Чистіше зіставлення route-to-action.
- Добре поєднується з action-орієнтованою архітектурою.

4. **Коли корисно**

- Ендпоінти з чіткою єдиною метою.
- CQRS/action-based стиль.
- Великі кодові бази, де менші класи покращують навігацію.

Invokable controllers — практичний спосіб тримати HTTP-шар явним і модульним.

</details>

<details>
<summary>23. Що таке Single Action Controllers?</summary>

#### Laravel

Single Action Controllers — це той самий підхід, що й invokable controllers: один клас контролера обробляє одну дію через метод `__invoke()`.

1. **Ключова ідея**

- Один клас = один use case.
- Без набору методів `index/store/update` в одному контролері.

2. **Чому команди це використовують**

- Краще розділення відповідальностей.
- Простішe тестування кожного ендпоінта.
- Менше merge-конфліктів у великих командах.

3. **Приклади use case**

- `ApproveInvoiceController`
- `SendWelcomeEmailController`
- `GenerateReportController`

4. **Компроміс**

- Більше файлів/класів.
- Але зазвичай краща довгострокова підтримуваність для середніх і великих проєктів.

Single Action Controllers — це передусім архітектурний стиль, який ставить акцент на ясність і масштабованість.

</details>

<details>
<summary>24. У чому різниця між Resource Controllers і API Resource Controllers?</summary>

#### Laravel

Різниця переважно в наборі згенерованих action-ів і в цільовому форматі відповіді.

1. **Resource Controller (`Route::resource`)**

- Генерує повний web CRUD-набір маршрутів:
  `index`, `create`, `store`, `show`, `edit`, `update`, `destroy`.
- Містить маршрути `create` і `edit`, зазвичай для HTML-форм/сторінок.

2. **API Resource Controller (`Route::apiResource`)**

- Генерує API-орієнтований CRUD-набір:
  `index`, `store`, `show`, `update`, `destroy`.
- Не містить `create` і `edit` (UI-сторінки форм для API зазвичай не потрібні).

3. **Типове використання**

- `resource`: server-rendered вебзастосунки.
- `apiResource`: JSON API, mobile backend, SPA backend.

4. **Пов’язаний концепт**

- API-відповіді часто формуються через `JsonResource` для узгодженого контракту даних.

</details>

<details>
<summary>25. Як створювати кастомні Artisan-команди?</summary>

#### Laravel

Кастомні Artisan-команди — це CLI-класи для автоматизації, обслуговування, імпортів і операційних процесів.

1. **Згенеруйте клас команди**

```bash
php artisan make:command SyncInvoicesCommand
```

2. **Визначте signature і description**

```php
protected $signature = 'billing:sync {--dry-run}';
protected $description = 'Sync invoices from billing provider';
```

3. **Реалізуйте логіку в `handle()`**

```php
public function handle(): int
{
    // command logic
    return self::SUCCESS;
}
```

4. **Використовуйте DI у команді**

- Інжектіть сервіси через конструктор або через резолв у методі.

5. **Запускайте команду**

```bash
php artisan billing:sync --dry-run
```

6. **Опціонально: планування**

- Зареєструйте команду в scheduler, щоб запускати її автоматично.

Кастомні команди ідеально підходять для повторюваних backend-операцій та DevOps-автоматизації.

</details>

<details>
<summary>26. Що таке macros і коли вони корисні?</summary>

#### Laravel

Macros дозволяють додавати власні методи до класів фреймворку під час виконання (до macroable-класів) без зміни вихідного коду Laravel.

1. **Поширені macroable-цілі**

- `Collection`, `Str`, `ResponseFactory`, `Route` тощо.

2. **Приклад**

```php
use Illuminate\Support\Collection;

Collection::macro('toKeyValue', function (string $key, string $value) {
    return $this->mapWithKeys(fn ($item) => [$item[$key] => $item[$value]]);
});
```

3. **Коли корисно**

- Повторювана утилітарна логіка по всій кодовій базі.
- Domain-specific helper-методи для колекцій/рядків.
- Більш виразний API для типових трансформацій.

4. **Best practices**

- Реєструйте macros у service provider.
- Обирайте чіткі назви, щоб уникати колізій.
- Не зловживайте: для складної поведінки краще окремі класи.

Macros найкраще підходять для невеликих, часто вживаних розширень фреймворку.

</details>

<details>
<summary>27. Що таке Actions в архітектурі Laravel і коли їх використовувати?</summary>

#### Laravel

Actions — це сфокусовані класи, які інкапсулюють один бізнесовий use case (одну прикладну операцію).

1. **Що таке Action**

- Клас на кшталт `CreateOrderAction`, `PublishPostAction`, `RefundPaymentAction`.
- Зазвичай має один метод (`handle()` або `execute()`).

2. **Навіщо використовувати Actions**

- Забирають бізнес-логіку з контролерів/моделей.
- Повторно використовуються з HTTP-контролерів, jobs, console-команд і listeners.
- Легше unit-тестуються завдяки чітким вхідним/вихідним контрактам.

3. **Типова структура**

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

4. **Коли використовувати**

- Нетипові або нетривіальні use case з оркестрацією правил.
- Логіка, що використовується з кількох точок входу.
- Команди, які застосовують service/action або CQRS-подібну архітектуру.

Actions покращують модульність і роблять бізнесові workflows явними.

</details>

<details>
<summary>28. Поясніть Repository Pattern і його переваги.</summary>

#### Laravel

Repository Pattern абстрагує доступ до даних через інтерфейси, щоб бізнес-логіка не була жорстко прив’язана до ORM/деталей запитів.

1. **Базова ідея**

- Визначаєте контракт (наприклад, `OrderRepository`).
- Надаєте реалізацію (наприклад, `EloquentOrderRepository`).
- Інжектите репозиторій у сервіси/actions.

2. **Переваги**

- Чітке розділення між domain/application логікою та persistence-шаром.
- Простішe тестування через fake/in-memory репозиторії.
- Централізація складної query-логіки та caching-стратегій.
- Легша заміна джерела даних у майбутньому.

3. **Компроміси**

- Додатковий шар абстракції й більше boilerplate-коду.
- Не завжди виправданий для дуже простих CRUD-застосунків.

4. **Прагматична рекомендація**

- Використовуйте репозиторії там, де доступ до даних складний або спільний для багатьох модулів.
- Уникайте over-engineering у простих секціях системи.

Repository Pattern цінний тоді, коли реально зменшує зв’язаність і складність, а не просто додає indirection.

</details>

<details>
<summary>29. Що таке Traits у PHP і як вони використовуються в Laravel?</summary>

#### Laravel

Traits — це мовний механізм PHP для горизонтального повторного використання коду між класами без спадкування.

1. **Що дають traits**

- Повторно використовувані методи/властивості через `use`.
- Спільну поведінку для класів, які не мають спільної ієрархії.

2. **Приклади використання в Laravel**

- Фреймворкові traits, такі як `SoftDeletes`, `HasFactory`, `Notifiable`, `AuthorizesRequests`, `DispatchesJobs`, `ValidatesRequests`.

3. **Приклад у моделі**

```php
use Illuminate\Database\Eloquent\SoftDeletes;

class Post extends Model
{
    use SoftDeletes;
}
```

4. **Best practices**

- Тримайте traits невеликими й цілісними.
- Використовуйте їх для повторного використання поведінки, а не для маскування “роздутого” класу.
- Для складної domain-логіки віддавайте перевагу композиції/сервісам.

Traits — практичний механізм реюзу, який широко застосовується в Laravel internals і прикладному коді.

</details>

<details>
<summary>30. У чому різниця між Laravel і Lumen, і чи актуальний Lumen у 2026 році?</summary>

#### Laravel

Laravel і Lumen мають спільне походження, але орієнтовані на різні архітектурні компроміси.

1. **Головні відмінності**

- **Laravel**: повнофункціональний фреймворк (багата екосистема, first-party пакети, широкі конвенції, велика інтеграційність).
- **Lumen**: micro-framework варіант із фокусом на мінімалізм і простіші API-сценарії.

2. **Архітектура та екосистема**

- Laravel має ширшу сумісність із first-party пакетами й повніший набір інструментів для розробки.
- Lumen навмисно “тонший” і не прагне повної сумісності з усією surface-областю пакетів Laravel.

3. **Контекст продуктивності**

- Історично Lumen обирали для легковагових API.
- У сучасних версіях Laravel продуктивність суттєво покращилась, тому практичний розрив для багатьох навантажень зменшився.

4. **Чи актуальний Lumen у 2026 році?**

- **Для нових проєктів:** зазвичай **не рекомендований** як базовий вибір в екосистемі Laravel.
- **Для існуючих систем:** залишається актуальним, якщо вже стабільно працює в продакшені.
- **Типовий вибір у 2026:** Laravel (з правильною оптимізацією) для більшості нових API та web backend-ів.

5. **Практичне правило вибору**

- Нові продукти стартуйте на Laravel.
- Lumen залишайте переважно для підтримки legacy-сервісів із чіткими операційними причинами.

</details>

<details>
<summary>31. Що таке Eloquent ORM?</summary>

#### Laravel

Eloquent ORM — це реалізація Active Record у Laravel для роботи з базою даних через PHP-об’єкти, а не через сирий SQL.

1. **Що він надає**

- Відображення model-to-table.
- Інтеграцію з query builder.
- Керування зв’язками між моделями.
- Attribute casting, accessors/mutators, scopes, events.

2. **Чому команди його використовують**

- Швидша розробка завдяки виразному синтаксису.
- Чистіший domain-код для типових CRUD-сценаріїв.
- Вбудовані конвенції, що зменшують boilerplate.

3. **Приклад**

```php
$users = User::query()
    ->where('is_active', true)
    ->latest()
    ->take(10)
    ->get();
```

4. **Важливе зауваження**

- Eloquent чудово підходить для більшості прикладних задач.
- Для вузькоспеціальних/звітних запитів query builder або raw SQL інколи кращі.

Eloquent — базовий data-access шар у більшості Laravel-застосунків.

</details>

<details>
<summary>32. Що таке Eloquent Models?</summary>

#### Laravel

Eloquent Models — це PHP-класи, які представляють таблиці бази даних та інкапсулюють поведінку даних.

1. **Базова роль**

- Кожна модель зазвичай мапиться на одну таблицю.
- Екземпляри моделі представляють окремі рядки таблиці.

2. **Що зазвичай містять моделі**

- Fillable/guarded атрибути.
- Casts і роботу з датами.
- Relationships.
- Scopes і domain-specific методи.

3. **Базовий приклад**

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

4. **Чому це важливо**

- Централізують persistence-логіку та поведінку сутності.
- Підвищують читабельність і узгодженість операцій із даними.

Eloquent-моделі — ключові будівельні блоки database-driven застосунків на Laravel.

</details>

<details>
<summary>33. Поясніть one-to-one, one-to-many, many-to-many і polymorphic relationships.</summary>

#### Laravel

Eloquent-зв’язки визначають, як моделі пов’язані між собою в структурі даних.

1. **One-to-one (`hasOne` / `belongsTo`)**

- Один запис пов’язаний рівно з одним записом.
- Приклад: `User` має один `Profile`.

2. **One-to-many (`hasMany` / `belongsTo`)**

- Один батьківський запис має багато дочірніх.
- Приклад: `Post` має багато `Comment`.

3. **Many-to-many (`belongsToMany`)**

- Обидві сторони можуть мати багато пов’язаних записів.
- Потребує pivot-таблиці.
- Приклад: `User` належить багатьом `Role`.

4. **Polymorphic**

- Модель може належати більш ніж одному типу батьківської моделі через спільний інтерфейс.
- Приклад: `Comment` може належати `Post` або `Video`.

5. **Чому це важливо**

- Зв’язки чітко відображають структуру домену.
- Eloquent може завантажувати пов’язані дані, обмежувати запити й спрощувати join-операції.

Правильний вибір типу зв’язку — ключ до чистого дизайну схеми та ефективних запитів.

</details>

<details>
<summary>34. Що таке polymorphic relationships і коли їх використовувати?</summary>

#### Laravel

Polymorphic relationships дозволяють одній моделі бути пов’язаною з кількома типами моделей через одну пару колонок (зазвичай `*_type` і `*_id`).

1. **Як це працює**

- Дочірня таблиця зберігає тип батьківської моделі + її ID.
- Одна дочірня модель може посилатися на різні батьківські моделі.

2. **Типові приклади**

- `Comment` для `Post`, `Video`, `Product`.
- `Image` для `User`, `Team`, `Article`.
- `Activity` для кількох типів сутностей.

3. **Методи зв’язків у Laravel**

- `morphTo` на дочірній моделі.
- `morphMany` / `morphOne` на батьківській моделі.
- `morphToMany` / `morphedByMany` для polymorphic many-to-many.

4. **Коли використовувати**

- Коли поведінка спільна для різнорідних батьківських сутностей.
- Коли потрібна одна універсальна дочірня таблиця замість кількох паралельних.

5. **Компроміс**

- Більш гнучка схема, але інколи складніші запити й вищі вимоги до індексації.

Використовуйте polymorphic-зв’язки там, де вони справді зменшують дублювання і природно відповідають доменній моделі.

</details>

<details>
<summary>35. Що таке eager loading?</summary>

#### Laravel

Eager loading означає, що пов’язані моделі завантажуються наперед у межах основного запиту, а не підтягуються пізніше для кожного елемента окремо.

1. **Як це робиться**

```php
$posts = Post::with(['author', 'comments'])->latest()->get();
```

2. **Чому це важливо**

- Зменшує загальну кількість SQL-запитів.
- Запобігає проблемі N+1.
- Покращує час відповіді й ефективність роботи БД.

3. **Корисні варіанти**

- Nested eager loading: `with('comments.user')`.
- Constrained eager loading через closures.
- Default eager loading через `$with` у моделі, якщо зв’язок потрібен майже завжди.

Eager loading — одна з базових практик оптимізації продуктивності в Eloquent.

</details>

<details>
<summary>36. Що таке проблема N+1 і як її вирішити?</summary>

#### Laravel

Проблема N+1 виникає, коли виконується 1 запит на список записів, а потім ще по одному запиту на кожен елемент для пов’язаних даних.

1. **Типовий сценарій**

- Ви отримали 100 постів.
- У циклі звертаєтесь до `$post->author`.
- У підсумку маєте 101 запит (1 + 100).

2. **Чому це погано**

- Різко зростає кількість запитів.
- Підвищується latency і навантаження на БД.
- Погіршується масштабованість під трафіком.

3. **Як вирішити в Laravel**

- Використовувати eager loading через `with()`.

```php
$posts = Post::with('author')->get();
```

- Використовувати `load()` / `loadMissing()`, якщо колекція моделей уже отримана.
- Застосовувати профайлінг (Telescope/Debugbar/логи) для виявлення “гарячих” місць.

4. **Best practice**

- Плануйте потрібні зв’язки на етапі побудови запиту.
- Перевіряйте цикли по моделях на приховані lazy-load виклики.

Усунення N+1 — одна з найефективніших оптимізацій продуктивності в Eloquent.

</details>

<details>
<summary>37. Що таке lazy eager loading?</summary>

#### Laravel

Lazy eager loading завантажує зв’язки після того, як моделі вже отримані, але все одно пакетно, а не по одній моделі.

1. **Коли використовується**

- Ви спочатку отримали моделі.
- Пізніше вирішили, які саме зв’язки потрібно підтягнути.

2. **Методи**

- `load()` завантажує вказані зв’язки.
- `loadMissing()` завантажує лише ті, що ще не завантажені.

```php
$posts = Post::latest()->take(50)->get();
$posts->load('author', 'comments');
```

3. **Чому це корисно**

- Уникає N+1, зберігаючи гнучкий контроль потоку.
- Підходить для умовної логіки або шарованих сервісів.

4. **Різниця з eager loading**

- Eager loading: `with()` до виконання SQL-запиту.
- Lazy eager loading: `load()` після виконання SQL-запиту.

Lazy eager loading — практичний компроміс між гнучкістю та продуктивністю.

</details>

<details>
<summary>38. Що таке global scopes і local scopes?</summary>

#### Laravel

Scopes — це повторно використовувані обмеження запитів в Eloquent.

1. **Global scopes**

- Автоматично застосовуються до всіх запитів моделі.
- Підходять для наскрізних правил (наприклад, tenant isolation, soft delete поведінка, active-only записи).

2. **Local scopes**

- Викликаються явно в запитах, коли потрібно.
- Дають сфокусовані повторно використовувані фільтри.

```php
public function scopePublished(Builder $query): Builder
{
    return $query->whereNotNull('published_at');
}

$posts = Post::published()->get();
```

3. **Коли що обирати**

- Global scope: дефолтне бізнес-правило, яке має діяти майже всюди.
- Local scope: опційний фільтр для конкретних use case.

4. **Застереження**

- Надмірне використання global scopes може “ховати” дані неочікувано; документуйте їх явно.

Scopes покращують узгодженість і прибирають дублювання умов у запитах.

</details>

<details>
<summary>39. Що таке query scopes?</summary>

#### Laravel

Query scopes — це методи моделі, які інкапсулюють повторно використовувані обмеження запиту для чистішого та композиційного query-коду.

1. **Патерн local query scope**

- Ім’я методу починається з `scope`.
- У виклику префікс не використовується.

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

2. **Переваги**

- Повторне використання фільтрів.
- Краща читабельність query-chain.
- Централізація логіки умов.

3. **Практичне застосування**

- Фільтри статусів (`active`, `published`, `archived`).
- Діапазони дат (`recent`, `betweenDates`).
- Бізнес-обмеження (`visibleTo`, `forTenant`).

Query scopes — ключовий інструмент для виразних і підтримуваних Eloquent-запитів.

</details>

<details>
<summary>40. Що таке accessors і mutators?</summary>

#### Laravel

Accessors і mutators визначають, як атрибути моделі трансформуються при читанні та записі.

1. **Accessor**

- Трансформує значення, коли воно зчитується з моделі.

2. **Mutator**

- Трансформує значення перед записом у модель.

3. **Сучасний стиль (`Attribute`)**

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

4. **Типові use case**

- Нормалізація вводу (trim/форматування регістру).
- Представлення обчислених/відформатованих значень.
- Трансформації на кшталт шифрування/дешифрування.

5. **Різниця з casts**

- Casts покривають типові перетворення типів.
- Accessors/mutators покривають кастомні, domain-specific трансформації.

Вони допомагають централізувати логіку перетворення атрибутів і робити її послідовною.

</details>

<details>
<summary>41. Що таке casts в Eloquent?</summary>

#### Laravel

Casts визначають, як Eloquent автоматично перетворює атрибути моделі між “сирими” значеннями БД і PHP-типами.

1. **Що роблять casts**

- Конвертують значення під час читання/запису.
- Роблять роботу з атрибутами послідовною й типобезпечною.

2. **Поширені типи casts**

- `integer`, `float`, `decimal:2`, `boolean`
- `datetime`, `immutable_datetime`
- `array`, `json`, `object`, `collection`
- `encrypted`, `hashed`

3. **Приклад**

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

4. **Чому це важливо**

- Менше ручного коду для парсингу/форматування.
- Менше неочевидних помилок типів.
- Краща читабельність domain-коду.

Casts — фундаментальна можливість для чистого керування атрибутами моделей.

</details>

<details>
<summary>42. Що таке Attribute objects у сучасному Laravel?</summary>

#### Laravel

`Attribute` objects — це сучасний спосіб визначати accessors і mutators в одному місці для конкретного поля моделі.

1. **Базова ідея**

- Метод повертає `Attribute::make(get: ..., set: ...)`.
- Чітко інкапсулює read/write-трансформації.

2. **Приклад**

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

3. **Переваги**

- Чистіше, ніж legacy-методи `getXxxAttribute` / `setXxxAttribute`.
- Getter і setter-логіка згрупована в одному методі.
- Простіше читати, тестувати та підтримувати.

4. **Коли використовувати**

- Кастомне форматування, нормалізація, шифрування або мапінг на value object для конкретних атрибутів.

Attribute objects — рекомендований сучасний патерн для accessors/mutators у поточних версіях Laravel.

</details>
