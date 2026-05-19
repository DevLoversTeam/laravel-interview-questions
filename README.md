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
<summary>2. Що таке Composer autoloading і як працює PSR-4?</summary>

#### PHP

Composer autoloading — це механізм автоматичного завантаження класів без ручних `require/include`, а PSR-4 — стандарт мапінгу namespace до файлової структури.

1. **Роль Composer autoload**

- Генерує автозавантажувач на основі конфігурації пакетів/застосунку.
- Підключається один раз і підвантажує класи за потреби.

2. **Принцип PSR-4**

- Namespace-префікс мапиться на базову директорію.
- Сегменти namespace відповідають піддиректоріям.
- Ім’я класу відповідає імені файла.

3. **Приклад**

- `App\\` -> `app/`
- `App\\Services\\BillingService` -> `app/Services/BillingService.php`

4. **Чому це важливо**

- Передбачувана структура коду.
- Менше ручного bootstrap-боїлерплейту.
- Краща сумісність із екосистемою пакетів.

Composer + PSR-4 — фундамент сучасної організації PHP/Laravel-кодової бази.

</details>

<details>
<summary>3. Що таке spread/splat оператор у PHP?</summary>

#### PHP

Оператор `...` у PHP використовується для розпакування аргументів/масивів і для variadic-параметрів.

1. **Argument unpacking**

```php
$args = [2, 3];
$result = sum(...$args);
```

2. **Array unpacking**

```php
$a = [1, 2];
$b = [...$a, 3, 4];
```

3. **Variadic capture**

```php
function logAll(string ...$messages): void {}
```

`...` робить функціональний і композиційний код коротшим і читабельнішим.

</details>

<details>
<summary>4. Що таке enums у PHP 8.1+?</summary>

#### PHP

Enums — це нативні типи для моделювання обмеженої множини станів/значень.

1. **Види**

- Unit enums (без скалярного значення).
- Backed enums (із `string` або `int` значенням).

2. **Приклад**

```php
enum OrderStatus: string
{
    case Draft = 'draft';
    case Paid = 'paid';
    case Shipped = 'shipped';
}
```

3. **Навіщо**

- Сильніші контракти.
- Менше “магічних рядків”.
- Краща type safety і static analysis.

Enums — рекомендований підхід для finite-state моделей у сучасному PHP.

</details>

<details>
<summary>5. Що таке readonly properties у PHP?</summary>

#### PHP

`readonly` властивість можна присвоїти лише один раз (зазвичай у конструкторі).

1. **Поведінка**

- Після ініціалізації змінювати значення заборонено.

2. **Приклад**

```php
final class UserDto
{
    public function __construct(
        public readonly int $id,
        public readonly string $email,
    ) {}
}
```

3. **Переваги**

- Менше випадкових мутацій.
- Простіше підтримувати immutable-об’єкти.

Readonly properties підвищують передбачуваність об’єктного стану.

</details>

<details>
<summary>6. Що таке readonly classes у PHP 8.2+?</summary>

#### PHP

`readonly class` робить усі instance-властивості класу readonly за замовчуванням.

1. **Що це дає**

- Політика незмінності на рівні всього класу.
- Менше boilerplate, ніж ставити `readonly` на кожне поле окремо.

2. **Приклад**

```php
readonly class Money
{
    public function __construct(
        public int $amount,
        public string $currency,
    ) {}
}
```

Readonly classes добре підходять для value objects і DTO з immutable-семантикою.

</details>

<details>
<summary>7. Що таке PHP generators і коли їх варто використовувати?</summary>

#### PHP

Generators — це функції з `yield`, які повертають значення ліниво, по одному, без створення великого масиву в пам’яті.

1. **Що вирішують**

- Значно зменшують споживання пам’яті при обробці великих наборів даних.

2. **Коли використовувати**

- Потокова обробка файлів.
- Ітерація великих вибірок із БД.
- Пайплайни, де не потрібна повна матеріалізація всіх даних.

3. **Приклад**

```php
function numbers(int $max): Generator
{
    for ($i = 1; $i <= $max; $i++) {
        yield $i;
    }
}
```

Generators доречні там, де важлива memory-efficiency і послідовна обробка даних.

</details>

<details>
<summary>8. Що таке Laravel Sail?</summary>

#### Laravel

Laravel Sail — це офіційне легковагове Docker-оточення для локальної розробки Laravel.

1. **Що дає Sail**

- Готові контейнери для PHP, БД, Redis та супутніх сервісів.
- Узгоджене локальне середовище для всієї команди.

2. **Чому його використовують**

- Швидкий онбординг нових розробників.
- Менше “працює тільки в мене” проблем.
- Не треба вручну збирати локальний стек.

3. **Практична користь**

- Команди запуску, тестування й сервісних операцій виконуються через єдиний Docker-based workflow.

Sail — практичний дефолт для контейнеризованої локальної розробки на Laravel.

</details>

<details>
<summary>9. Що таке Form Requests?</summary>

#### Laravel

Form Requests — це окремі request-класи, які інкапсулюють валідацію та авторизацію для конкретного HTTP-запиту.

1. **Що містять**

- `authorize()` для перевірки права на дію.
- `rules()` для правил валідації.

2. **Як використовуються**

- Type-hint у controller action; Laravel автоматично виконує перевірки до бізнес-логіки.

```php
public function store(StoreOrderRequest $request): JsonResponse
{
    $data = $request->validated();
    // ...
}
```

3. **Переваги**

- Тонші контролери.
- Централізована й повторно використовувана валідація.
- Простіше тестування request-рівня.

Form Requests — канонічний Laravel-підхід до валідації вхідних даних на межі API/web.

</details>

<details>
<summary>10. Як створювати REST API у Laravel?</summary>

#### Laravel

Створення REST API у Laravel базується на ресурсних маршрутах, валідації, авторизації та стабільному JSON-контракті.

1. Використовуйте `routes/api.php` і `Route::apiResource(...)`.
2. Тримайте контролери тонкими, бізнес-логіку виносьте в сервіси/actions.
3. Валідуйте вхідні дані через Form Requests.
4. Формуйте відповіді через API Resources.
5. Захищайте API через Sanctum/Passport, middleware, policies і rate limiting.

Добрий REST API в Laravel — це насамперед узгодженість контрактів і передбачувана поведінка.

</details>

<details>
<summary>11. Як працює concurrency у чергах?</summary>

#### Laravel

Concurrency у чергах досягається запуском кількох workers паралельно, щоб обробляти багато jobs одночасно.

1. **Модель**

- Кожен worker обробляє jobs незалежно.
- Більше workers = вищий паралельний throughput.

2. **Керування**

- Кількість worker-процесів.
- Розділення за пріоритетними чергами.
- Налаштування timeout/retry/memory.

3. **Вимоги до коректності**

- Jobs мають бути ідемпотентними.
- Для спільних ресурсів потрібні блокування/атомарні операції.

Concurrency підвищує пропускну здатність, але вимагає правильної моделі консистентності.

</details>

<details>
<summary>12. Що таке ідемпотентність у queued jobs?</summary>

#### Laravel

Ідемпотентність означає: повторний запуск тієї самої job не змінює фінальний результат порівняно з одноразовим виконанням.

1. **Чому це критично**

- Jobs можуть ретраїтися.
- Можливі дублікати dispatch.

2. **Як реалізувати**

- Унікальні бізнес-ключі/idempotency keys.
- Перевірка стану перед побічною дією.
- DB-обмеження або атомарні операції.

3. **Приклад**

- “Надіслати інвойс лише один раз на invoice ID”.

Ідемпотентність — ключ до надійних retry-safe асинхронних процесів.

</details>

<details>
<summary>13. Як працює кешування в Laravel?</summary>

#### Laravel

Laravel cache зберігає попередньо обчислені дані у швидкому сховищі, щоб зменшити повторні дорогі обчислення.

1. **Патерн**

- Читаємо з кешу.
- За відсутності — обчислюємо і зберігаємо з TTL.

2. **API**

- `get`, `put`, `remember`, `rememberForever`, `forget`.

3. **Приклад**

```php
$users = Cache::remember('users.active', 300, fn () => User::where('is_active', true)->get());
```

Кеш знижує latency й навантаження на БД.

</details>

<details>
<summary>14. Які cache drivers доступні?</summary>

#### Laravel

Поширені cache drivers у Laravel:

- `array`
- `file`
- `database`
- `redis`
- `memcached`
- `dynamodb` (за конфігурації)
- `null`

Для high-load сценаріїв зазвичай обирають Redis або Memcached.

</details>

<details>
<summary>15. Які cache-стратегії варто використовувати у high-load Laravel-застосунку?</summary>

#### Laravel

1. Cache-aside (`remember`) для дорогих запитів.
2. Захист від cache stampede через locks/jitter.
3. Точкове invalidation (за можливості tags).
4. Кешування компактних payload замість важких об’єктів.
5. Постійний моніторинг hit rate/latency.

У high-load найважливіші не лише швидкі кеші, а й правильна invalidation-стратегія.

</details>

<details>
<summary>16. Що таке cache tags?</summary>

#### Laravel

Cache tags дозволяють групувати ключі й очищати їх разом.

1. **Навіщо**

- Точкове очищення пов’язаних кешів без глобального flush.

2. **Приклад**

```php
Cache::tags(['users', 'team:42'])->put('users.team.42.list', $data, 600);
Cache::tags(['users', 'team:42'])->flush();
```

Працює не на всіх драйверах (типово Redis/Memcached).

</details>

<details>
<summary>17. Як очищати та прогрівати кеш?</summary>

#### Laravel

1. **Очищення**

```bash
php artisan cache:clear
php artisan config:clear
php artisan route:clear
php artisan view:clear
```

2. **Побудова кешів**

```bash
php artisan config:cache
php artisan route:cache
php artisan view:cache
```

3. **Warm-up**

- Після деплою наперед заповнюйте “гарячі” ключі для зменшення cold-start.

</details>

<details>
<summary>18. Що таке Laravel Octane?</summary>

#### Laravel

Laravel Octane запускає Laravel на long-lived workers (Swoole або RoadRunner) замість повного bootstrap на кожен запит.

Це дає вищий throughput і нижчу latency для відповідних навантажень.

</details>

<details>
<summary>19. Як Laravel Octane покращує продуктивність?</summary>

#### Laravel

1. Менше перезапусків framework bootstrap.
2. Більше запитів на один worker-процес.
3. Краща ефективність під сталим навантаженням.

Важливо писати Octane-safe код (без витоків mutable state між запитами).

</details>

<details>
<summary>20. Що таке Swoole і RoadRunner?</summary>

#### Laravel

Swoole і RoadRunner — high-performance application servers для Octane.

- **Swoole**: PHP-розширення з async/coroutines.
- **RoadRunner**: Go-based сервер із persistent PHP workers.

Обидва зменшують overhead класичного request-per-process підходу.

</details>

<details>
<summary>21. Які проблеми можуть виникати через state persistence в Octane?</summary>

#### Laravel

Оскільки workers довгоживучі, помилки керування станом можуть “протікати” між запитами.

1. Stale singleton/static state.
2. Випадкове збереження request/user контексту.
3. Memory growth і нестабільність worker-ів.

Потрібні stateless-підходи, скидання контексту й моніторинг пам’яті.

</details>

<details>
<summary>22. Як оптимізувати Laravel-застосунок для production?</summary>

#### Laravel

1. Увімкнути framework caches (`config`, `route`, `view`).
2. Налаштувати OPcache.
3. Виносити важкі задачі в queues.
4. Оптимізувати БД (N+1, індекси, `EXPLAIN`).
5. Використовувати Redis/Memcached кеш.
6. Налаштувати моніторинг і алерти.
7. Використовувати безпечний zero-downtime deployment flow.

Production-оптимізація — безперервний цикл “виміряти → покращити → перевірити”.

</details>

<details>
<summary>23. Що таке task scheduling у Laravel?</summary>

#### Laravel

Task scheduling у Laravel — це кодо-орієнтований шар керування регулярними задачами (cron orchestration).

1. **Базова ідея**

- Розклад визначається в коді застосунку.
- Системний cron запускає Laravel scheduler щохвилини.

2. **Типові сценарії**

- Періодичні синхронізації даних.
- Очистка службових даних.
- Генерація звітів.
- Розсилки за розкладом.

3. **Переваги**

- Централізовані, версійовані правила запуску.
- Менше ручного адміністрування великої кількості cron-записів на сервері.
- Підтримка overlap-захисту, environment-умов і гнучкої частоти.

4. **Операційний принцип**

- Налаштовується один cron-запис для `schedule:run`.
- Laravel сам визначає, які задачі мають запуститися в поточну хвилину.

Task scheduling робить регулярну автоматизацію в Laravel передбачуваною й підтримуваною.

</details>

<details>
<summary>24. Що таке Laravel Broadcasting?</summary>

#### Laravel

Laravel Broadcasting — це realtime-шар Laravel для доставки server-side подій клієнтам через WebSockets (або сумісні драйвери).

1. **Що він робить**

- Транслює вибрані події Laravel у канали.
- Дозволяє клієнтам підписуватися й реагувати миттєво.

2. **Типові сценарії**

- Живі сповіщення.
- Чати та індикатори присутності.
- Realtime-дашборди й оновлення статусів.

3. **Ключові поняття**

- Канали: `public`, `private`, `presence`.
- Авторизація для private/presence каналів.
- Event-класи з broadcasting-поведінкою.

4. **Загальна схема**

- Backend dispatch-ить broadcast event.
- Broadcast driver відправляє подію у websocket-інфраструктуру.
- Frontend (зазвичай Laravel Echo) слухає подію та оновлює UI.

Broadcasting дозволяє будувати реактивний UX без надмірного polling.

</details>

<details>
<summary>25. Що таке job batching?</summary>

#### Laravel

Job batching об’єднує багато jobs в один керований пакет із загальним життєвим циклом.

1. **Що це дає**

- Dispatch багатьох jobs як одного логічного процесу.
- Відстеження прогресу, завершення та помилок.
- Callback-и на етапах `then`, `catch`, `finally`.

2. **Типовий сценарій**

- Імпорт великого файлу, розбитий на багато jobs по чанках.

3. **Де корисно**

- Масові імпорт/експорт процеси.
- Переіндексація.
- Fan-out завдання, де важливий загальний статус.

4. **Практична користь**

- Краще спостереження за multi-job workflow.
- Простіше керування в адмінці (моніторинг/скасування).

Batching доречний, коли багато паралельних jobs належать одному бізнес-процесу.

</details>

<details>
<summary>26. Як працюють signed URLs у Laravel?</summary>

#### Laravel

Signed URL містить криптографічний підпис, що підтверджує: посилання сформоване вашим застосунком і не було змінене.

1. **Що захищається**

- Цілісність path і query parameters.
- За потреби — строк дії (тимчасові посилання).

2. **Як згенерувати**

```php
$url = URL::signedRoute('unsubscribe', ['user' => $user->id]);
$temporary = URL::temporarySignedRoute('download', now()->addMinutes(30), ['file' => $fileId]);
```

3. **Як перевірити**

- Використайте middleware `signed` на маршруті або відповідну перевірку в запиті.

```php
Route::get('/unsubscribe/{user}', UnsubscribeController::class)
    ->name('unsubscribe')
    ->middleware('signed');
```

4. **Типові сценарії**

- Unsubscribe links.
- Email verification дії.
- Тимчасові download/action посилання.

Signed URLs дають простий спосіб безпечно відкривати публічні дії без обов’язкової сесійної автентифікації.

</details>

<details>
<summary>27. Як Laravel захищає від XSS-атак?</summary>

#### Laravel

Laravel запобігає XSS переважно через безпечний рендеринг і escaping за замовчуванням.

1. **Blade екранує вивід автоматично**

- `{{ $value }}` HTML-escape-иться за замовчуванням.
- Це не дозволяє недовіреному HTML/JS виконатися в браузері.

2. **Обережно з raw output**

- `{!! $value !!}` рендерить без escaping.
- Використовуйте лише для довіреного або попередньо санітайзеного контенту.

3. **Додаткові захисні шари**

- Валідація й нормалізація вводу.
- CSP та інші security headers (через middleware/server config).

4. **API/frontend-практика**

- JSON-відповіді зазвичай безпечніші за вставку сирого HTML.
- На client-side також потрібно екранувати недовірені дані.

5. **Практичне правило**

- Escape by default, sanitize when needed, minimize raw rendering paths.

Laravel дає сильні дефолти, але фінальна безпека залежить від дисципліни виводу в прикладному коді.

</details>

<details>
<summary>28. Як Laravel захищає від SQL Injection?</summary>

#### Laravel

Laravel знижує ризик SQL Injection завдяки parameter binding і безпечним query-абстракціям за замовчуванням.

1. **Prepared statements і bindings**

- Query Builder та Eloquent використовують bind-параметри замість конкатенації SQL-рядків.

2. **Безпечні приклади**

```php
User::where('email', $email)->first();
DB::table('orders')->where('status', $status)->get();
```

3. **Де лишається ризик**

- Ручна конкатенація в raw SQL із недовіреним вводом.

```php
// небезпечно, якщо $input недовірений
DB::select("SELECT * FROM users WHERE email = '$input'");
```

4. **Безпечний raw SQL**

- Використовуйте placeholders і bindings:

```php
DB::select('SELECT * FROM users WHERE email = ?', [$input]);
```

5. **Best practices**

- Віддавайте перевагу Eloquent/Query Builder.
- Валідуйте вхідні дані.
- Мінімізуйте ручне складання SQL із зовнішніх параметрів.

Laravel безпечний за замовчуванням, але некоректне використання raw SQL може повернути injection-ризики.

</details>

<details>
<summary>29. Коли обирати Sanctum замість Passport?</summary>

#### Laravel

Sanctum доцільно обирати тоді, коли потрібна проста first-party автентифікація без повного OAuth2-стека.

1. **Коли Sanctum підходить найкраще**

- SPA + Laravel backend із session/cookie auth.
- Mobile або внутрішні клієнти з personal access tokens.
- Невеликі/середні API, де не потрібна OAuth2 delegation.

2. **Чому саме Sanctum**

- Швидше впровадження.
- Менша операційна складність.
- Менше рухомих частин у керуванні токенами.

3. **Коли його недостатньо**

- Потрібна делегована авторизація для сторонніх застосунків.
- Потрібні повні OAuth2 grant-flow і стандартизований auth-server рівень.

4. **Практичне правило**

- За замовчуванням для first-party продуктів — Sanctum.
- Переходьте на Passport, коли OAuth2-вимоги чітко сформульовані.

Sanctum — прагматичний дефолт для більшості Laravel API у продуктовій розробці.

</details>

<details>
<summary>30. Порівняйте Laravel Sanctum і Laravel Passport.</summary>

#### Laravel

Sanctum і Passport обидва надають API-автентифікацію, але орієнтовані на різну складність задач.

1. **Sanctum**

- Легковагова token-auth + SPA session-auth.
- Personal access tokens і прості abilities.
- Швидший старт і менше OAuth2-складності.

2. **Passport**

- Повноцінний OAuth2 server.
- Підтримує authorization code, client credentials, refresh tokens, scopes та інші OAuth2-механізми.
- Краще підходить для third-party delegated authorization.

3. **Компроміс**

- Sanctum: простіше впровадити і підтримувати для first-party застосунків.
- Passport: потужніше, але важче в налаштуванні та операційному супроводі.

4. **Типовий вибір**

- Sanctum: SPA/mobile + власний backend.
- Passport: платформи з зовнішніми OAuth-клієнтами та складними auth-сценаріями.

Обирайте за реальними протокольними вимогами, а не за “універсальністю” пакета.

</details>

<details>
<summary>31. Що таке multi-authentication і як його реалізувати?</summary>

#### Laravel

Multi-authentication — це підтримка кількох типів користувачів/guard-контекстів в одному застосунку (наприклад, `web`, `admin`, `api`).

1. **Типові сценарії**

- Окремі портали для адміністраторів і клієнтів.
- Різні рівні доступу для внутрішніх і зовнішніх користувачів.
- Різні auth-стратегії для різних каналів доступу.

2. **Як реалізувати**

- Налаштувати кілька guards/providers у auth-конфігурації.
- Використовувати middleware з конкретним guard: `auth:admin`, `auth:web`, `auth:sanctum`.
- За потреби мати окремі login-flow/controllers/routes для кожного guard.

3. **Приклад**

```php
Route::middleware('auth:admin')->group(function () {
    Route::get('/admin/dashboard', AdminDashboardController::class);
});
```

4. **Best practices**

- Ізолюйте route-групи для кожного guard.
- Тримайте authorization-правила явними для кожного user-type.

Multi-auth дає чітке розділення ідентичностей і прав доступу в різних доменах одного застосунку.

</details>

<details>
<summary>32. Як працює автентифікація в Laravel?</summary>

#### Laravel

Автентифікація в Laravel перевіряє особу користувача й зберігає її між запитами через guards і providers.

1. **Ключові складові**

- **Guards** визначають, як користувач автентифікується (session, token тощо).
- **Providers** визначають, як отримуються користувачі (зазвичай Eloquent-модель).

2. **Session-based flow (web)**

- Користувач надсилає credentials.
- Laravel валідує їх через provider.
- У разі успіху ID користувача зберігається в сесії.
- Наступні запити резолвлять користувача із session/cookie.

3. **Token-based flow (API)**

- Клієнт надсилає токен (наприклад, Sanctum/Passport bearer token).
- Guard валідує токен і резолвить користувача.

4. **Корисні helper-и**

- `Auth::attempt()`, `Auth::user()`, `auth()->check()`.
- Middleware `auth` для захисту маршрутів.

Laravel-автентифікація є guard-орієнтованою та однаково добре працює і для web, і для API.

</details>

<details>
<summary>33. У чому різниця між API Resources і Transformers?</summary>

#### Laravel

Обидва підходи формують вихідні дані, але API Resources — це нативний стандарт Laravel, а Transformers — ширший архітектурний патерн або зовнішній шар мапінгу.

1. **API Resources (вбудовано в Laravel)**

- Офіційний механізм Laravel (`JsonResource`).
- Тісна інтеграція з фреймворком і просте використання.
- Найкращий дефолт для більшості Laravel API.

2. **Transformers (загальний патерн / пакети)**

- Архітектурний підхід для мапінгу domain-даних у response DTO.
- Може бути реалізований кастомними класами або пакетами (наприклад, Fractal-подібні підходи).
- Корисний, коли потрібен framework-agnostic або дуже кастомний transformation pipeline.

3. **Практична різниця**

- Resource = офіційний Laravel-підхід.
- Transformer = ширший патерн, який може як використовувати Laravel-примітиви, так і бути незалежним від них.

4. **Що обирати**

- У Laravel-first застосунках: за замовчуванням API Resources.
- Кастомний transformer-шар: коли межі домену/API вимагають додаткового відокремлення.

Обидва підходи розв’язують проблему представлення даних; вибір залежить від складності архітектури та вимог до переносимості.

</details>

<details>
<summary>34. Що таке soft deletes?</summary>

#### Laravel

Soft deletes позначають запис як видалений, але фізично не видаляють його з таблиці.

1. **Як це працює**

- Використовується колонка `deleted_at`.
- Під час видалення встановлюється `deleted_at`, а рядок лишається в БД.
- Дефолтні запити не повертають soft-deleted записи.

2. **Увімкнення в моделі**

```php
use Illuminate\Database\Eloquent\SoftDeletes;

class Post extends Model
{
    use SoftDeletes;
}
```

3. **Ключові helper-методи**

- `withTrashed()` — включити видалені записи.
- `onlyTrashed()` — тільки видалені.
- `restore()` — відновити запис.
- `forceDelete()` — видалити назавжди.

4. **Чому це корисно**

- Можливість відновлення даних.
- Краща “аудитність” і безпечніший робочий процес при випадкових видаленнях.

Soft deletes — практичний компроміс між семантикою видалення та відновлюваністю даних.

</details>

<details>
<summary>35. Що таке database seeding?</summary>

#### Laravel

Database seeding — це процес заповнення бази даних наперед визначеними або згенерованими даними.

1. **Призначення**

- Підготувати застосунок до роботи з необхідними стартовими даними.
- Дати реалістичні набори даних для development/testing.

2. **Як запускається**

- Класи сідів виконуються через Artisan.

```bash
php artisan db:seed
php artisan db:seed --class=UserSeeder
```

3. **Типовий процес**

- `DatabaseSeeder` оркеструє запуск інших сідів.
- Factories використовуються для масового створення синтетичних записів.

4. **Best practices**

- Критичні довідкові дані робіть детермінованими.
- У production уникайте руйнівної логіки сідів, якщо це не заплановано явно.
- Версіонуйте сіди разом із кодовою базою.

Seeding забезпечує відтворюваність середовищ і готовність системи до розробки чи тестування.

</details>

<details>
<summary>36. Як генерувати й відкочувати міграції?</summary>

#### Laravel

Laravel надає Artisan-команди для створення міграцій і керування їх виконанням.

1. **Генерація міграції**

```bash
php artisan make:migration create_orders_table
php artisan make:migration add_status_to_orders_table --table=orders
```

2. **Запуск міграцій**

```bash
php artisan migrate
```

3. **Відкат останнього batch**

```bash
php artisan migrate:rollback
```

4. **Відкат кількох кроків**

```bash
php artisan migrate:rollback --step=3
```

5. **Інші корисні команди**

- `php artisan migrate:reset` (відкатити все)
- `php artisan migrate:refresh` (reset + migrate)
- `php artisan migrate:fresh` (видалити всі таблиці + migrate)

Команди rollback/refresh потрібно застосовувати обережно, особливо в production-середовищі.

</details>

<details>
<summary>37. Що таке транзакції бази даних і як їх використовувати?</summary>

#### Laravel

Транзакція бази даних об’єднує кілька операцій в одну атомарну дію: або виконуються всі, або всі відкочуються.

1. **Навіщо потрібні транзакції**

- Зберігають цілісність даних при пов’язаних записах.
- Запобігають частковим змінам, якщо виникла помилка.

2. **Використання в Laravel**

```php
DB::transaction(function () use ($orderData) {
    $order = Order::create($orderData);
    Inventory::reserveForOrder($order);
    Payment::captureForOrder($order);
});
```

3. **Ручне керування (за потреби)**

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

4. **Best practices**

- Тримайте транзакцію короткою й швидкою.
- Уникайте довгих зовнішніх HTTP-викликів усередині транзакції.
- За потреби комбінуйте з row locking для конкурентно-чутливих сценаріїв.

Транзакції критично важливі для надійних фінансових, складських і багатокрокових бізнес-процесів.

</details>

<details>
<summary>38. Як вивести raw SQL-запити в Laravel?</summary>

#### Laravel

У Laravel є кілька способів переглянути SQL і bindings залежно від глибини дебагу.

1. **`toSql()` + `getBindings()`**

```php
$query = User::where('email', 'like', '%@example.com%');

$sql = $query->toSql();
$bindings = $query->getBindings();
```

2. **`toRawSql()` (сучасний Laravel)**

- Повертає SQL із підставленими bindings для зручнішого читання.

```php
$sql = User::where('id', 5)->toRawSql();
```

3. **Слухач запитів**

```php
DB::listen(function ($query) {
    logger()->debug($query->sql, $query->bindings);
});
```

4. **Інструменти**

- Laravel Telescope / Debugbar можуть показувати виконані запити та їхній час.

Ці підходи варто використовувати в development/debugging, а не як постійну production-вивідну логіку.

</details>

<details>
<summary>39. Що таке chunking і коли використовувати chunk() або lazy()?</summary>

#### Laravel

Chunking — це обробка результатів запиту невеликими пакетами, а не завантаження всього набору в пам’ять одразу.

1. **`chunk()`**

- Отримує записи фіксованими порціями й виконує callback для кожного chunk.

```php
User::query()->chunk(1000, function ($users) {
    foreach ($users as $user) {
        // process
    }
});
```

2. **`lazy()`**

- Внутрішньо теж працює через порції, але назовні дає єдиний lazy-потік.
- Зручніший для pipeline-style коду.

```php
User::query()->lazy(1000)->each(function (User $user) {
    // process
});
```

3. **Коли що обирати**

- `chunk()` — коли потрібна явна обробка “пакет за пакетом”.
- `lazy()` — коли потрібен гнучкий потоковий fluent-процес.

4. **Важлива примітка**

- Якщо ви оновлюєте записи під час ітерації, віддавайте перевагу ID-орієнтованим варіантам (`chunkById`, `lazyById`), щоб уникнути пропусків/дублів.

Chunking — базова практика для обробки великих наборів даних із контрольованим споживанням пам’яті.

</details>

<details>
<summary>40. Яке призначення методу cursor()?</summary>

#### Laravel

`cursor()` повертає lazy-ітератор результатів, що дозволяє проходити записи по одному з мінімальним використанням пам’яті.

1. **Навіщо використовувати**

- Щоб не завантажувати весь результат запиту в RAM.
- Щоб ефективно обробляти великі таблиці.

2. **Приклад**

```php
foreach (User::where('is_active', true)->cursor() as $user) {
    // process user
}
```

3. **Характеристики**

- Ітерація на базі генератора.
- Добре підходить для read/process-пайплайнів.
- Ефективний у queue/long-running job сценаріях.

4. **Коли це не ідеально**

- Якщо потрібен випадковий доступ до всіх результатів одразу.
- Якщо потрібна важка eager-завантажена графова структура для всього набору.

`cursor()` — ключовий інструмент масштабованої обробки записів “рядок за рядком”.

</details>

<details>
<summary>41. Що таке Lazy Collections?</summary>

#### Laravel

Lazy Collections обробляють елементи як потік (на базі генераторів), а не завантажують усі дані в пам’ять одразу.

1. **Ключова властивість**

- Пам’яткоефективна ітерація великих наборів даних.

2. **Як це працює**

- Елементи генеруються та обробляються по одному.
- Ланцюжок трансформацій виконується ліниво, під час ітерації.

3. **Типові джерела**

- `lazy()` у запитах.
- `cursor()` в Eloquent/query builder.
- Кастомні генератори, обгорнуті в `LazyCollection`.

4. **Коли використовувати**

- Скрипти міграції даних.
- Великі експорт/імпорт процеси.
- Фонові задачі з мільйонами рядків.

5. **Компроміс**

- Частина операцій колекцій, що вимагає повної матеріалізації, менш зручна для lazy-підходу.

Lazy Collections ідеальні там, де безпека пам’яті важливіша за random access.

</details>

<details>
<summary>42. У чому різниця між масивами й колекціями?</summary>

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
<summary>43. Як згенерувати events і listeners?</summary>

#### Laravel

Laravel надає Artisan-генератори та стандартний flow реєстрації для events/listeners.

1. **Згенерувати event**

```bash
php artisan make:event OrderPaid
```

2. **Згенерувати listener**

```bash
php artisan make:listener SendOrderReceipt --event=OrderPaid
```

3. **Зареєструвати зв’язок**

- Зв’яжіть event і listener в event service provider або використовуйте discovery-конфігурацію фреймворку.

4. **Dispatch події**

```php
event(new OrderPaid($order));
```

5. **Черга для listener за потреби**

- Реалізуйте `ShouldQueue` у listener, щоб обробка йшла асинхронно.

Генерація + явна реєстрація роблять event-workflow прозорим і підтримуваним.

</details>

<details>
<summary>44. Що таке events і listeners у Laravel?</summary>

#### Laravel

Events і listeners реалізують publish-subscribe підхід для внутрішньої взаємодії модулів у Laravel-застосунку.

1. **Event**

- Представляє факт того, що щось сталося в домені/застосунку.
- Приклади: `OrderPaid`, `UserRegistered`, `InvoiceOverdue`.

2. **Listener**

- Клас-обробник, який реагує на event і виконує побічну дію.
- Приклади: надіслати email, оновити CRM, поставити downstream-job.

3. **Чому цей підхід корисний**

- Розв’язує core-flow і побічні дії.
- Підвищує модульність і підтримуваність.
- Дозволяє додавати кілька реакцій на одну подію без зміни producer-коду.

4. **Dispatch і обробка**

- Подія dispatch-иться із сервісу/контролера.
- Фреймворк доставляє її зареєстрованим listeners.

Events описують факти, listeners реалізують реакції.

</details>

<details>
<summary>45. Що таке queued listeners?</summary>

#### Laravel

Queued listeners — це event-listeners, які виконуються асинхронно через систему черг, а не одразу під час dispatch події.

1. **Чим відрізняються від звичайних listeners**

- Звичайний listener виконується негайно.
- Queued listener ставиться в чергу й обробляється worker-ом.

2. **Як увімкнути**

- Listener має реалізувати `ShouldQueue`.

3. **Навіщо це потрібно**

- Не блокувати request-cycle важкими побічними діями.
- Винести у фон email, зовнішні API-виклики, аналітику тощо.

4. **Best practices**

- Робіть listener-логіку ідемпотентною.
- Налаштовуйте retries/timeouts відповідно до ризиків.
- Обробляйте помилки зовнішніх залежностей явно.

Queued listeners — ключовий елемент масштабованої event-обробки без деградації UX.

</details>

<details>
<summary>46. Що таке job batching?</summary>

#### Laravel

Job batching об’єднує багато jobs в один відстежуваний пакет із спільним життєвим циклом і callback-обробкою.

1. **Що дає batching**

- Можливість dispatch-ити багато jobs як один логічний блок.
- Відстеження прогресу, завершення та помилок.
- Callback-и на етапах `then`, `catch`, `finally`.

2. **Приклад сценарію**

- Імпорт великого файлу, розбитий на багато chunk-processing jobs в одному batch.

3. **Типові use case**

- Імпорт/експорт даних.
- Масові reindex-операції.
- Fan-out навантаження, де важливий загальний статус виконання.

4. **Операційні переваги**

- Краща спостережуваність і керованість multi-job workflow.
- Простіший контроль (моніторинг/скасування) через адмінські інструменти.

Batching корисний, коли багато паралельних jobs належать до одного бізнес-процесу.

</details>

<details>
<summary>47. Як обробляти failed jobs?</summary>

#### Laravel

Laravel надає вбудовані механізми для фіксації, аналізу, повторного запуску та очищення failed jobs.

1. **Фіксація помилок**

- Налаштуйте сховище для failed jobs (зазвичай таблиця `failed_jobs`).
- Винятки під час виконання переводять job у failed після вичерпання retry-ліміту.

2. **Retry-поведінка**

- Контролюється через властивості/опції job (`tries`, backoff-стратегії).

3. **Корисні команди**

```bash
php artisan queue:failed
php artisan queue:retry all
php artisan queue:forget <id>
php artisan queue:flush
```

4. **Job-рівнева обробка**

- Реалізуйте метод `failed(Throwable $e)` для cleanup/alert/compensation логіки.

5. **Best practices**

- Робіть jobs ідемпотентними.
- Додавайте структуроване логування й алерти.
- Розділяйте transient і permanent failure-сценарії.

Надійна обробка failed jobs критична для стабільної асинхронної архітектури.

</details>

<details>
<summary>48. У чому різниця між queue drivers: sync, database, Redis і SQS?</summary>

#### Laravel

Ці драйвери відрізняються моделлю виконання, продуктивністю, надійністю та операційними вимогами.

1. **`sync`**

- Виконує job негайно в межах поточного запиту.
- Не потребує фонового worker.
- Добре для local dev/простих сценаріїв, але не для важкої асинхронної production-нагрузки.

2. **`database`**

- Зберігає jobs у таблиці реляційної БД.
- Простий у старті й надійний, але зазвичай повільніший на високому throughput.

3. **`redis`**

- In-memory backend із високою швидкістю.
- Підходить для високого throughput і низької latency.
- Часто використовується разом із Horizon для моніторингу.

4. **`sqs`**

- Повністю керований queue-сервіс AWS.
- Висока масштабованість і надійність.
- Підходить для distributed/cloud-native архітектур; має хмарні затримки/вартість.

5. **Практичний вибір**

- Малий/простий проєкт: `database`.
- Високонавантажений стек із Redis: `redis`.
- AWS-native розподілені системи: `sqs`.
- Локальне або примусово синхронне виконання: `sync`.

Вибір драйвера має відповідати профілю навантаження та інфраструктурній стратегії.

</details>

<details>
<summary>49. Які queue drivers доступні в Laravel?</summary>

#### Laravel

Laravel підтримує кілька backend-ів черг через конфігуровані drivers.

1. **Поширені вбудовані drivers**

- `sync`
- `database`
- `redis`
- `sqs` (Amazon SQS)
- `null`

2. **Загальні характеристики**

- `sync`: виконує job одразу в поточному request-потоці.
- `database`: зберігає jobs у таблицях БД.
- `redis`: швидкий in-memory backend.
- `sqs`: керований хмарний queue-сервіс.
- `null`: ігнорує jobs (корисно для окремих local/testing сценаріїв).

3. **Конфігурація**

- Налаштовується в `config/queue.php` та через environment variables.

Driver обирають за вимогами до надійності, throughput, інфраструктури та операційної моделі.

</details>

<details>
<summary>50. Що таке jobs і queue workers?</summary>

#### Laravel

Jobs і workers — це базові producer-consumer компоненти асинхронної обробки в Laravel.

1. **Jobs**

- Інкапсульовані класи задач (зазвичай у `app/Jobs`).
- Представляють окрему одиницю роботи для негайного або відкладеного виконання.
- Для асинхронного виконання зазвичай реалізують `ShouldQueue`.

2. **Queue workers**

- Довгоживучі процеси, які виконують jobs із черги.
- Запускаються через Artisan (`php artisan queue:work`).
- Підтримують параметри retries, timeout, sleep, queue selection.

3. **Потік виконання**

- Код dispatch-ить job (`dispatch(...)`).
- Payload job потрапляє в обраний queue backend.
- Worker забирає job і виконує `handle()`.

4. **Операційна примітка**

- У production workers зазвичай керуються process manager-ом (Supervisor/systemd).

Jobs визначають роботу, а workers безперервно виконують її у фоні.

</details>

<details>
<summary>51. Поясніть систему черг у Laravel.</summary>

#### Laravel

Система черг Laravel виносить довгі або важкі задачі з HTTP request-cycle в асинхронну фонову обробку.

1. **Навіщо використовуються черги**

- Швидша відповідь користувачу.
- Краща масштабованість під навантаженням.
- Надійне виконання із retry-механізмами та контролем помилок.

2. **Як це працює**

- Застосунок dispatch-ить job у queue backend.
- Queue worker читає job із черги й виконує її.
- Невдалі jobs можна повторити або зберігати у failed storage.

3. **Типові задачі в черзі**

- Email-розсилки, сповіщення, генерація звітів.
- Інтеграції з зовнішніми API та webhooks.
- Обробка зображень/відео, важкі імпорт/експорт операції.

4. **Ключові інструменти екосистеми**

- Worker-команда `queue:work`.
- Відстеження через `failed_jobs`.
- Horizon (для Redis-черг) для моніторингу та керування.

Черги — критичний елемент для responsive і надійних Laravel-застосунків.

</details>

<details>
<summary>52. Що таке encrypted cookies і signed cookies?</summary>

#### Laravel

Encrypted cookies і signed cookies обидва захищають цілісність cookie, але шифрування додатково захищає конфіденційність вмісту.

1. **Encrypted cookies**

- Значення cookie шифрується й підписується.
- Клієнт не може прочитати або коректно змінити оригінальне значення.
- Laravel middleware може автоматично шифрувати/дешифрувати такі cookie.

2. **Signed cookies (орієнтація на цілісність)**

- Значення може залишатися читабельним, але перевіряється підписом.
- Дозволяє виявляти підміну, але не приховує зміст.

3. **Дефолтна поведінка Laravel**

- У типовому web-стеку Laravel зазвичай використовуються саме encrypted cookies.

4. **Коли що використовувати**

- Encrypted cookies — для чутливих або stateful значень.
- Signed-only підхід — коли читабельність прийнятна, але потрібна перевірка цілісності.

5. **Security note**

- Завжди встановлюйте `Secure`, `HttpOnly` та коректний `SameSite`.

На практиці encrypted cookies найчастіше є безпечнішим дефолтним вибором для Laravel web-застосунків.

</details>

<details>
<summary>53. Як працюють signed URLs у Laravel?</summary>

#### Laravel

Signed URL містить криптографічний підпис, який підтверджує, що посилання згенероване вашим застосунком і не було змінене.

1. **Що саме захищає**

- Цілісність path і query parameters.
- Опційно — строк дії для time-limited посилань.

2. **Генерація signed URL**

```php
$url = URL::signedRoute('unsubscribe', ['user' => $user->id]);
$temporary = URL::temporarySignedRoute('download', now()->addMinutes(30), ['file' => $fileId]);
```

3. **Перевірка підпису**

- Використовуйте middleware `signed` на маршруті або перевірку через helper запиту.

```php
Route::get('/unsubscribe/{user}', UnsubscribeController::class)
    ->name('unsubscribe')
    ->middleware('signed');
```

4. **Типові сценарії**

- Unsubscribe-посилання.
- Email verification дії.
- Тимчасові download/action посилання.

Signed URL — простий спосіб захищати публічні дії без обов’язкової повної автентифікованої сесії.

</details>

<details>
<summary>54. Яких security best practices має дотримуватися кожен Laravel-застосунок?</summary>

#### Laravel

Кожен Laravel-застосунок має поєднувати дефолтні механізми фреймворку зі строгою операційною дисципліною.

1. **Auth і контроль доступу**

- Захищайте приватні маршрути автентифікацією.
- Використовуйте gates/policies для перевірки прав.
- Дотримуйтеся принципу найменших привілеїв.

2. **Безпека вводу/виводу**

- Валідуйте всі вхідні дані.
- Екрануйте вивід за замовчуванням (Blade `{{ }}`).
- Уникайте конкатенації raw SQL; використовуйте bindings.

3. **Безпека сесій і cookies**

- Увімкніть `HttpOnly`, `Secure` та коректний `SameSite`.
- Регенеруйте сесію на login/logout.

4. **Секрети й конфігурація**

- Захищайте `.env`, ротуйте секрети, розділяйте середовища.
- Ніколи не комітьте credentials у git.

5. **Транспорт і заголовки**

- Примусово використовуйте HTTPS.
- Додавайте security headers (CSP, HSTS, X-Frame-Options тощо).

6. **Гігієна залежностей і платформи**

- Регулярно оновлюйте Laravel/PHP/пакети.
- Моніторте вразливості й швидко встановлюйте патчі.

7. **Захист від зловживань**

- Налаштовуйте rate limiting для auth і чутливих ендпоінтів.
- Логуйте та моніторте підозрілу активність.

8. **Захист даних**

- Паролі лише хешуйте, чутливі зворотні дані шифруйте.
- Робіть резервні копії та перевіряйте процедури відновлення.

Безпека — це не одна фіча, а багатошарова безперервна практика в коді та операціях.

</details>

<details>
<summary>55. Що таке Gates і Policies?</summary>

#### Laravel

Gates і Policies — це механізми авторизації в Laravel.

1. **Gates**

- Closure-орієнтовані правила авторизації.
- Підходять для простих ability-перевірок, не прив’язаних жорстко до моделі.

2. **Policies**

- Класовий підхід до авторизації, організований навколо моделі/ресурсу.
- Методи на кшталт `view`, `create`, `update`, `delete` тощо.

3. **Коли що використовувати**

- **Gates** — для простих глобальних перевірок.
- **Policies** — для model-centric авторизації та масштабованих систем.

4. **Приклади використання**

- `Gate::allows('export-reports')`
- `$this->authorize('update', $post)`

Gates дають легкі перевірки, Policies — структуровану авторизацію для великих застосунків.

</details>

<details>
<summary>56. Як працюють Blade-директиви @can і @cannot?</summary>

#### Laravel

`@can` і `@cannot` — це Blade-директиви, які умовно рендерять HTML залежно від результату авторизації.

1. **`@can`**

- Показує контент, якщо користувач має право на вказану дію.

```blade
@can('update', $post)
    <a href="{{ route('posts.edit', $post) }}">Edit</a>
@endcan
```

2. **`@cannot`**

- Показує контент, якщо користувач не має права.

```blade
@cannot('delete', $post)
    <span>You cannot delete this post.</span>
@endcannot
```

3. **Як вони обчислюються**

- Усередині викликають логіку gate/policy.
- Працюють у контексті поточного автентифікованого користувача.

4. **Чому це корисно**

- UI узгоджується з backend-правилами доступу.
- Користувач не бачить дій, які йому недоступні.

Ці директиви спрощують permission-aware рендеринг у Blade.

</details>

<details>
<summary>57. Що таке multi-authentication і як його реалізувати?</summary>

#### Laravel

Multi-authentication — це підтримка кількох user-type/guard-контекстів в одному застосунку (наприклад, `web`, `admin`, `api`).

1. **Типові сценарії**

- Окремі портали для адміністраторів і клієнтів.
- Доступ для співробітників і зовнішніх партнерів.
- Різні auth-стратегії для різних каналів.

2. **Як реалізувати**

- Налаштувати кілька guards/providers у auth-конфігурації.
- Використовувати middleware з конкретним guard: `auth:admin`, `auth:web`, `auth:sanctum`.
- За потреби розділити login-flow/controllers/routes для кожного guard.

3. **Приклад захисту маршруту**

```php
Route::middleware('auth:admin')->group(function () {
    Route::get('/admin/dashboard', AdminDashboardController::class);
});
```

4. **Best practices**

- Ізолюйте route-групи й session-flow для кожного guard.
- Явно фіксуйте authorization-правила для кожного типу користувача.

Multi-auth дає чітке розділення ідентичностей і прав доступу між доменами застосунку.

</details>

<details>
<summary>58. Порівняйте Laravel Sanctum і Laravel Passport.</summary>

#### Laravel

Sanctum і Passport обидва вирішують API-автентифікацію, але для різного рівня складності.

1. **Sanctum**

- Легковагова token-auth + SPA session-auth.
- Personal access tokens і прості abilities.
- Швидкий старт без OAuth2-складності.

2. **Passport**

- Повноцінний OAuth2 server.
- Підтримує authorization code, client credentials, refresh tokens, scopes (та інші потоки).
- Краще підходить для third-party delegated authorization.

3. **Компроміс складності**

- Sanctum: простіше й швидше для first-party застосунків.
- Passport: потужніше, але важче в налаштуванні та супроводі.

4. **Типовий вибір**

- Sanctum: SPA/mobile + власний backend.
- Passport: platform/ecosystem API з зовнішніми OAuth-клієнтами.

Обирайте за вимогами протоколу автентифікації, а не лише за популярністю пакета.

</details>

<details>
<summary>59. Коли обирати Sanctum замість Passport?</summary>

#### Laravel

Sanctum варто обирати, коли потрібна проста first-party автентифікація без повного OAuth2-стеку.

1. **Добрі сценарії для Sanctum**

- SPA + Laravel backend із session/cookie auth.
- Mobile або внутрішні клієнти з personal access tokens.
- Невеликі/середні API, де OAuth2 delegation не потрібен.

2. **Чому саме Sanctum**

- Швидша реалізація.
- Нижча операційна складність.
- Менше рухомих частин у керуванні токенами.

3. **Коли цього недостатньо**

- Коли стороннім застосункам потрібна делегована авторизація користувача.
- Коли потрібні повні OAuth2 grant-флоу та можливості auth-server рівня стандарту.

4. **Практичне правило**

- За замовчуванням — Sanctum для first-party продуктів.
- Переходьте на Passport, коли OAuth2-вимоги явно присутні.

Sanctum — прагматичний дефолт для більшості Laravel API-продуктів.

</details>

<details>
<summary>60. Як Laravel захищає від SQL Injection?</summary>

#### Laravel

Laravel знижує ризик SQL Injection завдяки parameter binding і безпечним query-абстракціям “за замовчуванням”.

1. **Prepared statements / bindings**

- Query Builder і Eloquent використовують bind-параметри замість конкатенації SQL-рядків.

2. **Безпечні приклади**

```php
User::where('email', $email)->first();
DB::table('orders')->where('status', $status)->get();
```

3. **Де ризик лишається**

- Небезпечна ручна конкатенація raw SQL.

```php
// risk, якщо $input недовірений
DB::select("SELECT * FROM users WHERE email = '$input'");
```

4. **Безпечний raw SQL**

- Використовуйте placeholders і bindings:

```php
DB::select('SELECT * FROM users WHERE email = ?', [$input]);
```

5. **Best practices**

- Віддавайте перевагу Eloquent/Query Builder.
- Валідуйте ввід і не будуйте SQL із недовірених значень вручну.

Laravel безпечний “із коробки”, але неправильне використання raw SQL може повернути injection-ризики.

</details>

<details>
<summary>61. Як Laravel захищає від CSRF-атак?</summary>

#### Laravel

Laravel захищає від CSRF, вимагаючи валідний CSRF-токен для state-changing web-запитів.

1. **Як це працює**

- Генерується session-bound токен і зберігається на сервері.
- Форма містить токен (`@csrf`).
- Middleware перевіряє токен на POST/PUT/PATCH/DELETE запитах.

2. **Використання в Blade**

```blade
<form method="POST" action="/profile">
    @csrf
    <!-- fields -->
</form>
```

3. **AJAX/SPA**

- Токен можна передавати в заголовку (наприклад, `X-CSRF-TOKEN`) для same-site session-flow.

4. **Чому це ефективно**

- Зловмисник не може згенерувати коректний session-bound токен із іншого сайту.

5. **Важлива примітка**

- CSRF головно стосується cookie/session browser-запитів, а не типових stateless bearer-token API.

CSRF middleware — базовий рівень web-безпеки в Laravel.

</details>

<details>
<summary>62. Як Laravel захищає від XSS-атак?</summary>

#### Laravel

Laravel запобігає XSS передусім через escaping output і безпечні шаблонні дефолти.

1. **Blade за замовчуванням екранує**

- `{{ $value }}` автоматично HTML-escape-иться.
- Це не дає недовіреному HTML/JS виконатися.

2. **Обережно з unescaped output**

- `{!! $value !!}` рендерить raw HTML, тому має використовуватися лише для довіреного/санітайзеного контенту.

3. **Додатковий захист**

- Валідація та нормалізація вводу зменшують ризик потрапляння шкідливих payload.
- CSP/security headers (через middleware/server config) додають defense-in-depth.

4. **Frontend/API аспекти**

- Повернення JSON зазвичай безпечніше, ніж рендер raw HTML-фрагментів.
- Client-side рендер теж має екранувати недовірений контент.

5. **Практичне правило**

- Escape by default, sanitize коли HTML справді потрібен, і мінімізуйте raw-render шляхи.

Laravel дає сильні дефолти, але безпечний output-handling у прикладному коді лишається критичним.

</details>

<details>
<summary>63. Як працює шифрування в Laravel?</summary>

#### Laravel

Laravel надає симетричне шифрування через facade `Crypt` із використанням ключа застосунку.

1. **Як це працює**

- Використовується app key із environment/config.
- Дані шифруються з перевіркою цілісності для виявлення підміни.
- Розшифрування можливе лише тим самим ключем.

2. **Типове використання**

```php
$encrypted = Crypt::encryptString('secret-value');
$plain = Crypt::decryptString($encrypted);
```

3. **Де застосовується**

- Чутливі значення, що зберігаються в БД/конфігурованих payload.
- Внутрішні механізми фреймворку (наприклад, encrypted cookies, якщо увімкнено).

4. **Best practices**

- Тримайте `APP_KEY` секретним і стабільним для кожного середовища.
- Ротуйте ключі обережно, з продуманою міграційною стратегією.
- Не шифруйте те, що має бути хешованим (наприклад, паролі).

Шифрування Laravel дає простий і безпечний захист “at rest” для чутливих, але зворотно-дешифровуваних даних.

</details>

<details>
<summary>64. У чому різниця між автентифікацією та авторизацією?</summary>

#### Laravel

Автентифікація й авторизація пов’язані, але це різні рівні безпеки.

1. **Автентифікація (Authentication)**

- Відповідає на запитання: “Хто ви?”
- Перевіряє особу (login/session/token).

2. **Авторизація (Authorization)**

- Відповідає на запитання: “Що вам дозволено робити?”
- Перевіряє права/ability на конкретну дію або ресурс.

3. **Відображення в Laravel**

- Автентифікація: guards, providers, `auth` middleware.
- Авторизація: gates, policies, `can` middleware, Blade-директиви `@can`.

4. **Приклад**

- Користувач може бути автентифікований (увійшов у систему), але не мати права видалити чужий пост.

Автентифікація встановлює ідентичність, авторизація застосовує правила доступу.

</details>

<details>
<summary>65. Як працює автентифікація в Laravel?</summary>

#### Laravel

Автентифікація в Laravel перевіряє особу користувача й зберігає цю ідентичність між запитами через guards і providers.

1. **Ключові складові**

- **Guards** визначають, як користувач автентифікується в запиті (session, token тощо).
- **Providers** визначають, як отримуються користувачі (зазвичай Eloquent-модель).

2. **Session-based flow (web)**

- Користувач надсилає credentials.
- Laravel валідує їх через provider.
- У разі успіху ID користувача зберігається в сесії.
- У наступних запитах поточний користувач резолвиться із session/cookie.

3. **Token-based flow (API)**

- Клієнт надсилає токен (наприклад, Sanctum/Passport bearer token).
- Guard валідує токен і резолвить автентифікованого користувача.

4. **Фреймворкові helper-и**

- `Auth::attempt()`, `Auth::user()`, `auth()->check()`.
- Middleware `auth` захищає маршрути.

5. **Практична рекомендація**

- Використовуйте вбудовані auth-скелети/пакети для типових сценаріїв.
- Тримайте auth-логіку централізовано, уникайте власної crypto/session-реалізації без потреби.

Автентифікація в Laravel guard-орієнтована й узгоджена для web та API точок входу.

</details>

<details>
<summary>66. У чому різниця між API Resources і Transformers?</summary>

#### Laravel

Обидва підходи формують вихідні дані, але API Resources — це нативний стандарт Laravel, а Transformers — ширший архітектурний патерн або зовнішній шар мапінгу.

1. **API Resources (вбудовано в Laravel)**

- Офіційний механізм Laravel (`JsonResource`).
- Тісна інтеграція з фреймворком і просте використання.
- Найкращий дефолт для більшості Laravel API.

2. **Transformers (загальний патерн / пакети)**

- Архітектурний підхід для мапінгу domain-даних у response DTO.
- Може бути реалізований кастомними класами або пакетами (наприклад, Fractal-подібні підходи).
- Корисний, коли потрібен framework-agnostic або дуже кастомний transformation pipeline.

3. **Практична різниця**

- Resource = офіційний Laravel-підхід.
- Transformer = ширший патерн, який може як використовувати Laravel-примітиви, так і бути незалежним від них.

4. **Що обирати**

- У Laravel-first застосунках: за замовчуванням API Resources.
- Кастомний transformer-шар: коли межі домену/API вимагають додаткового відокремлення.

Обидва підходи розв’язують проблему представлення даних; вибір залежить від складності архітектури та вимог до переносимості.

</details>

<details>
<summary>67. Що таке API Resources у Laravel?</summary>

#### Laravel

API Resources — це шар трансформації, який перетворює моделі/колекції на узгоджену JSON-структуру відповіді.

1. **Що вони роблять**

- Контролюють форму вихідних даних.
- Приховують внутрішні поля.
- Передбачувано форматують і компонують пов’язані дані.

2. **Приклад**

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

3. **Використання**

```php
return new UserResource($user);
return UserResource::collection($users);
```

4. **Чому це важливо**

- Стабільні API-контракти.
- Розділення persistence-моделі та transport-формату.
- Простіше версіонування API й контроль політики відповіді.

API Resources — нативний first-class підхід Laravel для стандартизації JSON API-відповідей.

</details>

<details>
<summary>68. Як оптимізувати Eloquent-запити для продуктивності?</summary>

#### Laravel

Оптимізація Eloquent переважно зводиться до зменшення кількості запитів, обсягу даних і зайвої model-обробки.

1. **Уникайте N+1**

- Використовуйте `with()` / `load()` для relationships.

2. **Вибирайте лише потрібні колонки**

```php
User::query()->select('id', 'name')->get();
```

3. **Робіть агрегації/перевірки існування на рівні SQL**

- `count`, `sum`, `exists`, `withCount` замість завантаження повних колекцій.

4. **Ефективно обробляйте великі набори**

- Використовуйте `chunkById`, `lazyById`, `cursor` для memory-safe ітерації.

5. **Індексна стратегія**

- Додавайте релевантні індекси для частих фільтрів/сортувань/join.

6. **Кешуйте там, де доречно**

- Кешуйте стабільні або дорогі результати запитів.

7. **Вимірюйте та профілюйте**

- Використовуйте Telescope/Debugbar/query logs і `EXPLAIN` плани БД.

8. **Для складних звітних маршрутів використовуйте query builder/raw SQL**

- Не кожен важкий запит зручно моделювати лише високорівневим ORM-підходом.

Оптимізація має бути measurement-driven: спершу міряйте, потім покращуйте найкритичніші місця.

</details>

<details>
<summary>69. Що таке soft deletes?</summary>

#### Laravel

Soft deletes позначають запис як видалений, але фізично не видаляють його з таблиці.

1. **Як це працює**

- Використовується колонка `deleted_at`.
- Під час видалення встановлюється `deleted_at`, а рядок лишається в БД.
- Дефолтні запити не повертають soft-deleted записи.

2. **Увімкнення в моделі**

```php
use Illuminate\Database\Eloquent\SoftDeletes;

class Post extends Model
{
    use SoftDeletes;
}
```

3. **Ключові helper-методи**

- `withTrashed()` — включити видалені записи.
- `onlyTrashed()` — тільки видалені.
- `restore()` — відновити запис.
- `forceDelete()` — видалити назавжди.

4. **Чому це корисно**

- Можливість відновлення даних.
- Краща “аудитність” і безпечніший робочий процес при випадкових видаленнях.

Soft deletes — практичний компроміс між семантикою видалення та відновлюваністю даних.

</details>

<details>
<summary>70. Що таке database seeding?</summary>

#### Laravel

Database seeding — це процес заповнення бази даних наперед визначеними або згенерованими даними.

1. **Призначення**

- Підготувати застосунок до роботи з необхідними стартовими даними.
- Дати реалістичні набори даних для development/testing.

2. **Як запускається**

- Класи сідів виконуються через Artisan.

```bash
php artisan db:seed
php artisan db:seed --class=UserSeeder
```

3. **Типовий процес**

- `DatabaseSeeder` оркеструє запуск інших сідів.
- Factories використовуються для масового створення синтетичних записів.

4. **Best practices**

- Критичні довідкові дані робіть детермінованими.
- У production уникайте руйнівної логіки сідів, якщо це не заплановано явно.
- Версіонуйте сіди разом із кодовою базою.

Seeding забезпечує відтворюваність середовищ і готовність системи до розробки чи тестування.

</details>

<details>
<summary>71. Як працюють factories у сучасному Laravel?</summary>

#### Laravel

У сучасному Laravel factories є class-based і model-centric, зазвичай розміщуються в `database/factories`.

1. **Factory на основі definition**

- Метод `definition()` повертає дефолтні fake-атрибути.

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

- Іменовані варіанти для конкретних сценаріїв.

```php
public function admin(): static
{
    return $this->state(fn () => ['is_admin' => true]);
}
```

3. **Використання**

```php
User::factory()->admin()->count(3)->create();
User::factory()->make(); // не зберігає в БД
```

4. **Робота зі зв’язками**

- Factories підтримують створення relations через `has()`, `for()` та callbacks.

Factories роблять генерацію тестових/службових даних виразною, композиційною та контрольованою.

</details>

<details>
<summary>72. Що таке seeders і factories?</summary>

#### Laravel

Seeders і factories допомагають швидко генерувати та заповнювати дані для розробки, тестів і початкового стану системи.

1. **Seeders**

- Класи, які наповнюють БД визначеними наборами даних.
- Підходять для базових довідкових даних (ролі, права, налаштування).

2. **Factories**

- “Шаблони” для генерації model-екземплярів із fake або кастомними даними.
- Зручні для тестів і demo/dev-даних.

3. **Як працюють разом**

- Seeder викликає factories для швидкого створення великої кількості записів.

```php
User::factory()->count(50)->create();
```

4. **Типові сценарії**

- Bootstrap локального середовища.
- Підготовка даних для автотестів.
- Наповнення staging/demo середовищ.

Seeders визначають, *що* вставляти, а factories визначають, *як* генерувати дані моделей.

</details>

<details>
<summary>73. Як генерувати й відкочувати міграції?</summary>

#### Laravel

Laravel надає Artisan-команди для створення міграцій і керування їх виконанням.

1. **Генерація міграції**

```bash
php artisan make:migration create_orders_table
php artisan make:migration add_status_to_orders_table --table=orders
```

2. **Запуск міграцій**

```bash
php artisan migrate
```

3. **Відкат останнього batch**

```bash
php artisan migrate:rollback
```

4. **Відкат кількох кроків**

```bash
php artisan migrate:rollback --step=3
```

5. **Інші корисні команди**

- `php artisan migrate:reset` (відкатити все)
- `php artisan migrate:refresh` (reset + migrate)
- `php artisan migrate:fresh` (видалити всі таблиці + migrate)

Команди rollback/refresh потрібно застосовувати обережно, особливо в production-середовищі.

</details>

<details>
<summary>74. Що таке міграції і чому вони важливі?</summary>

#### Laravel

Міграції — це version-controlled PHP-файли, які описують зміни схеми бази даних у часі.

1. **Що роблять міграції**

- Створюють/змінюють/видаляють таблиці, колонки, індекси, constraints.
- Роблять зміни схеми відтворюваними в усіх середовищах.

2. **Чому це важливо**

- Командна робота над схемою через code review.
- Детерміновані deploy-и й rollback-и.
- Підхід “інфраструктура як код” для еволюції БД.

3. **Типова структура міграції**

- `up()` застосовує зміни.
- `down()` відкочує зміни.

4. **Операційна цінність**

- Простіший онбординг і CI-налаштування.
- Менше “works on my machine” розбіжностей схеми БД.

Міграції — основа підтримуваного життєвого циклу схеми в Laravel.

</details>

<details>
<summary>75. Що таке транзакції бази даних і як їх використовувати?</summary>

#### Laravel

Транзакція бази даних об’єднує кілька операцій в одну атомарну дію: або виконуються всі, або всі відкочуються.

1. **Навіщо потрібні транзакції**

- Зберігають цілісність даних при пов’язаних записах.
- Запобігають частковим змінам, якщо виникла помилка.

2. **Використання в Laravel**

```php
DB::transaction(function () use ($orderData) {
    $order = Order::create($orderData);
    Inventory::reserveForOrder($order);
    Payment::captureForOrder($order);
});
```

3. **Ручне керування (за потреби)**

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

4. **Best practices**

- Тримайте транзакцію короткою й швидкою.
- Уникайте довгих зовнішніх HTTP-викликів усередині транзакції.
- За потреби комбінуйте з row locking для конкурентно-чутливих сценаріїв.

Транзакції критично важливі для надійних фінансових, складських і багатокрокових бізнес-процесів.

</details>

<details>
<summary>76. Які aggregate-методи доступні в query builder?</summary>

#### Laravel

Laravel Query Builder надає стандартні SQL-агрегації у вигляді helper-методів.

1. **Основні aggregate-методи**

- `count()`
- `sum($column)`
- `avg($column)` / `average($column)`
- `min($column)`
- `max($column)`

2. **Приклади**

```php
$totalUsers = DB::table('users')->count();
$totalRevenue = DB::table('orders')->sum('amount');
$avgOrder = DB::table('orders')->avg('amount');
$firstDate = DB::table('orders')->min('created_at');
$latestDate = DB::table('orders')->max('created_at');
```

3. **Разом із групуванням**

- Комбінуйте `selectRaw(...)` + `groupBy(...)` для агрегацій по групах.

4. **Чому це корисно**

- Ефективні обчислення на стороні БД.
- Не потрібно переносити зайві рядки в пам’ять застосунку.

Агрегації — базовий інструмент для дашбордів, аналітики та бізнес-метрик API.

</details>

<details>
<summary>77. Як вивести raw SQL-запити в Laravel?</summary>

#### Laravel

У Laravel є кілька способів переглянути SQL і bindings залежно від глибини дебагу.

1. **`toSql()` + `getBindings()`**

```php
$query = User::where('email', 'like', '%@example.com%');

$sql = $query->toSql();
$bindings = $query->getBindings();
```

2. **`toRawSql()` (сучасний Laravel)**

- Повертає SQL із підставленими bindings для зручнішого читання.

```php
$sql = User::where('id', 5)->toRawSql();
```

3. **Слухач запитів**

```php
DB::listen(function ($query) {
    logger()->debug($query->sql, $query->bindings);
});
```

4. **Інструменти**

- Laravel Telescope / Debugbar можуть показувати виконані запити та їхній час.

Ці підходи варто використовувати в development/debugging, а не як постійну production-вивідну логіку.

</details>

<details>
<summary>78. Поясніть query builder у Laravel.</summary>

#### Laravel

Laravel Query Builder — це fluent API для побудови SQL-запитів, який працює поверх PDO і нижче рівня Eloquent-моделей.

1. **Що це таке**

- БД-агностичний інтерфейс запитів через `DB::table(...)`.
- Підтримує select, joins, where-умови, group, order, pagination, insert/update/delete.

2. **Приклад**

```php
$users = DB::table('users')
    ->select('id', 'name', 'email')
    ->where('is_active', true)
    ->orderByDesc('created_at')
    ->limit(20)
    ->get();
```

3. **Чому його використовують**

- Дає більше контролю над SQL, ніж високорівневий ORM-підхід.
- Добре підходить для звітних запитів і складних join-конструкцій.
- Зберігає безпечну роботу з параметрами через bindings.

4. **Eloquent vs Query Builder**

- Eloquent: model-centric, багаті domain-можливості.
- Query Builder: table/query-centric, нижчий рівень і часто “легший”.

Query Builder — базовий fluent-шар для точного SQL-контролю в Laravel.

</details>

<details>
<summary>79. Що таке chunking і коли використовувати chunk() або lazy()?</summary>

#### Laravel

Chunking — це обробка результатів запиту невеликими пакетами, а не завантаження всього набору в пам’ять одразу.

1. **`chunk()`**

- Отримує записи фіксованими порціями й виконує callback для кожного chunk.

```php
User::query()->chunk(1000, function ($users) {
    foreach ($users as $user) {
        // process
    }
});
```

2. **`lazy()`**

- Внутрішньо теж працює через порції, але назовні дає єдиний lazy-потік.
- Зручніший для pipeline-style коду.

```php
User::query()->lazy(1000)->each(function (User $user) {
    // process
});
```

3. **Коли що обирати**

- `chunk()` — коли потрібна явна обробка “пакет за пакетом”.
- `lazy()` — коли потрібен гнучкий потоковий fluent-процес.

4. **Важлива примітка**

- Якщо ви оновлюєте записи під час ітерації, віддавайте перевагу ID-орієнтованим варіантам (`chunkById`, `lazyById`), щоб уникнути пропусків/дублів.

Chunking — базова практика для обробки великих наборів даних із контрольованим споживанням пам’яті.

</details>

<details>
<summary>80. Яке призначення методу cursor()?</summary>

#### Laravel

`cursor()` повертає lazy-ітератор результатів, що дозволяє проходити записи по одному з мінімальним використанням пам’яті.

1. **Навіщо використовувати**

- Щоб не завантажувати весь результат запиту в RAM.
- Щоб ефективно обробляти великі таблиці.

2. **Приклад**

```php
foreach (User::where('is_active', true)->cursor() as $user) {
    // process user
}
```

3. **Характеристики**

- Ітерація на базі генератора.
- Добре підходить для read/process-пайплайнів.
- Ефективний у queue/long-running job сценаріях.

4. **Коли це не ідеально**

- Якщо потрібен випадковий доступ до всіх результатів одразу.
- Якщо потрібна важка eager-завантажена графова структура для всього набору.

`cursor()` — ключовий інструмент масштабованої обробки записів “рядок за рядком”.

</details>

<details>
<summary>81. Що таке Lazy Collections?</summary>

#### Laravel

Lazy Collections обробляють елементи як потік (на базі генераторів), а не завантажують усі дані в пам’ять одразу.

1. **Ключова властивість**

- Пам’яткоефективна ітерація великих наборів даних.

2. **Як це працює**

- Елементи генеруються та обробляються по одному.
- Ланцюжок трансформацій виконується ліниво, під час ітерації.

3. **Типові джерела**

- `lazy()` у запитах.
- `cursor()` в Eloquent/query builder.
- Кастомні генератори, обгорнуті в `LazyCollection`.

4. **Коли використовувати**

- Скрипти міграції даних.
- Великі експорт/імпорт процеси.
- Фонові задачі з мільйонами рядків.

5. **Компроміс**

- Частина операцій колекцій, що вимагає повної матеріалізації, менш зручна для lazy-підходу.

Lazy Collections ідеальні там, де безпека пам’яті важливіша за random access.

</details>

<details>
<summary>82. У чому різниця між масивами й колекціями?</summary>

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
<summary>83. Що таке Eloquent Collections?</summary>

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
<summary>84. Які головні переваги Laravel порівняно з іншими PHP-фреймворками?</summary>

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
<summary>85. Як Laravel дотримується архітектури MVC?</summary>

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
<summary>86. Опишіть життєвий цикл запиту в застосунку Laravel.</summary>

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
<summary>87. Що таке сервісний контейнер Laravel?</summary>

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
<summary>88. Поясніть різницю між binding, singleton binding і resolving у сервісному контейнері.</summary>

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
<summary>89. Що таке contextual binding і коли його варто використовувати?</summary>

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
<summary>90. Що таке Service Providers і яка їхня мета?</summary>

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
<summary>91. У чому різниця між registering і booting у service provider?</summary>

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
<summary>92. Що таке Laravel Contracts?</summary>

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
<summary>93. У чому різниця між Contract і Facade?</summary>

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
<summary>94. Поясніть різницю між Facades і helper-функціями в Laravel.</summary>

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
<summary>95. Як працює Dependency Injection у Laravel?</summary>

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
<summary>96. Як Laravel використовує IoC (Inversion of Control)?</summary>

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
<summary>97. Що таке middleware у Laravel?</summary>

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
<summary>98. Як зареєструвати та призначити middleware?</summary>

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
<summary>99. Як middleware працює з параметрами?</summary>

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
<summary>100. Що таке route groups, prefixes і middleware groups?</summary>

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
<summary>101. Що таке route model binding?</summary>

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
<summary>102. Поясніть implicit vs explicit route model binding.</summary>

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
<summary>103. Що таке rate limiting у Laravel і як він працює?</summary>

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
<summary>104. Що таке invokable controllers?</summary>

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
<summary>105. Що таке Single Action Controllers?</summary>

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
<summary>106. У чому різниця між Resource Controllers і API Resource Controllers?</summary>

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
<summary>107. Як створювати кастомні Artisan-команди?</summary>

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
<summary>108. Що таке macros і коли вони корисні?</summary>

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
<summary>109. Що таке Actions в архітектурі Laravel і коли їх використовувати?</summary>

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
<summary>110. Поясніть Repository Pattern і його переваги.</summary>

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
<summary>111. Що таке Traits у PHP і як вони використовуються в Laravel?</summary>

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
<summary>112. У чому різниця між Laravel і Lumen, і чи актуальний Lumen у 2026 році?</summary>

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
<summary>113. Що таке Eloquent ORM?</summary>

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
<summary>114. Що таке Eloquent Models?</summary>

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
<summary>115. Поясніть one-to-one, one-to-many, many-to-many і polymorphic relationships.</summary>

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
<summary>116. Що таке polymorphic relationships і коли їх використовувати?</summary>

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
<summary>117. Що таке eager loading?</summary>

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
<summary>118. Що таке проблема N+1 і як її вирішити?</summary>

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
<summary>119. Що таке lazy eager loading?</summary>

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
<summary>120. Що таке global scopes і local scopes?</summary>

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
<summary>121. Що таке query scopes?</summary>

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
<summary>122. Що таке accessors і mutators?</summary>

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
<summary>123. Що таке casts в Eloquent?</summary>

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
<summary>124. Що таке Attribute objects у сучасному Laravel?</summary>

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

<details>
<summary>125. Як реалізувати WebSockets у Laravel?</summary>

#### Laravel

У Laravel WebSockets зазвичай реалізують через зв’язку Broadcasting + Reverb (або сумісну websocket-інфраструктуру) + Echo на фронтенді.

1. **Налаштування backend**

- Сконфігурувати broadcasting driver і websocket server.
- Описати broadcastable events та авторизацію каналів.

2. **Налаштування frontend**

- Ініціалізувати Laravel Echo з websocket-конектором.
- Підписатися на канали й слухати події.

3. **Безпека каналів**

- Для захищених потоків використовувати private/presence канали.

4. **Операційні аспекти**

- Масштабувати websocket-інстанси під навантаження.
- Моніторити кількість з’єднань, частоту повідомлень і reconnect-поведінку.

5. **Типові сценарії**

- Realtime-сповіщення, чат, колаборація, live-дашборди.

У сучасному Laravel зв’язка Reverb + Echo є стандартним first-party шляхом для WebSocket-функціоналу.

</details>

<details>
<summary>126. У чому різниця між feature tests і unit tests?</summary>

#### Laravel

Feature-тести й unit-тести відрізняються насамперед рівнем охоплення та глибиною інтеграції.

1. **Unit tests**

- Перевіряють невеликий ізольований фрагмент логіки (клас/метод).
- Зазвичай мають мінімум framework-контексту.
- Залежності часто мокаються.

2. **Feature tests**

- Перевіряють поведінку системи через фреймворкові межі.
- Часто охоплюють маршрути, middleware, валідацію, БД, auth і структуру відповіді.

3. **Коли що застосовувати**

- Unit tests: складна чиста бізнес-логіка.
- Feature tests: ключові user/API-флоу та інтеграційна впевненість.

4. **Практичний баланс**

- Комбінуйте обидва підходи: unit для швидких точкових перевірок, feature для end-to-end поведінки.

Unit-тест відповідає на питання “чи правильно працює цей компонент?”, feature-тест — “чи правильно працює сценарій у системі?”.

</details>
