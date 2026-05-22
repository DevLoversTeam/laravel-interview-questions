**Read in other languages: [English 🇺🇸](README.en.md),
[Polska 🇵🇱](README.pl.md), [German 🇩🇪](README.de.md), [French 🇫🇷](README.fr.md),
[Spanish 🇪🇸](README.es.md), [Українська 🇺🇦](README.md).**

<h1>
  Laravel <img src="./assets/laravel.svg" width="40" height="40" alt="Laravel logo"/>
</h1>

<h2>Najpopularniejsze pytania i odpowiedzi na rozmowach Laravel</h2>

<details>
<summary>1. Czym jest Laravel i dlaczego się go używa?</summary>

#### Laravel

Laravel to nowoczesny framework webowy PHP, skupiony na produktywności dewelopera, czystej architekturze i łatwym utrzymaniu kodu.

1. **Czym jest Laravel**

- Open-source’owy framework zbudowany na komponentach Symfony.
- Wystarczająco opiniotwórczy, by dawać mocne domyślne wzorce, a jednocześnie elastyczny dla własnej architektury.

2. **Dlaczego się go używa**

- Przyspiesza development dzięki wbudowanym mechanizmom: routing, walidacja, autoryzacja, kolejki, mail, eventy i cache.
- Wspiera czysty kod poprzez service container, middleware, Eloquent ORM i narzędzia testowe.
- Dostarcza first-party narzędzia (`Artisan`, migracje, scheduler, Horizon, Telescope) do aplikacji gotowych na produkcję.

3. **Typowe zastosowania**

- REST API i usługi backendowe.
- Serwerowo renderowane aplikacje webowe.
- Panele administracyjne, produkty SaaS i platformy marketplace.
- Przetwarzanie zadań w tle oraz integracje z usługami zewnętrznymi.

Krótko: Laravel służy do szybszego budowania bezpiecznych, skalowalnych i utrzymywalnych aplikacji PHP, przy mniejszej ilości boilerplate’u.

</details>


<details>
<summary>2. Jakie są główne zalety Laravel w porównaniu z innymi frameworkami PHP?</summary>

#### Laravel

Główne zalety Laravel wynikają z bardzo dobrego developer experience, bogatych funkcji wbudowanych oraz dużego ekosystemu.

1. **Developer experience**

- Spójny i ekspresyjny design API we wszystkich komponentach frameworka.
- Bardzo dobra dokumentacja i łatwy onboarding.
- Szybkie scaffoldowanie i workflow CLI przez `Artisan`.

2. **„Baterie w zestawie”**

- First-class wsparcie dla routingu, walidacji, auth, kolejek, eventów, notyfikacji, cache i schedulera.
- ORM (Eloquent) oraz migracje schematu dostępne domyślnie.

3. **Architektura i utrzymywalność**

- Service container i dependency injection są głęboko zintegrowane.
- Middleware i service providery jasno wydzielają concerns przekrojowe.
- Mocne wsparcie testów dzięki integracji z PHPUnit/Pest.

4. **Siła ekosystemu**

- Oficjalne narzędzia: Forge, Vapor, Horizon, Telescope, Octane, Sanctum, Passport, Cashier.
- Dojrzałe paczki społeczności oraz długoterminowa stabilność ekosystemu.

5. **Produktywność operacyjna**

- Płynne workflow CI/CD i deploymentów.
- Bardzo dobre wsparcie dla kolejek, cache, Redis i monitoringu.

Laravel jest często wybierany, gdy zespoły chcą szybko dostarczać funkcje biznesowe bez utraty jakości kodu i długoterminowej utrzymywalności.

</details>

<details>
<summary>3. Jak Laravel realizuje architekturę MVC?</summary>

#### Laravel

Laravel realizuje MVC (Model-View-Controller), rozdzielając logikę domeny/danych, obsługę żądań oraz warstwę prezentacji.

1. **Model (M)**

- Zwykle modele Eloquent w `app/Models`.
- Reprezentują encje domenowe i rekordy bazy danych.
- Zawierają relacje, scope’y, casty i zachowania na poziomie domeny.

2. **View (V)**

- Szablony Blade w `resources/views`.
- Odpowiadają wyłącznie za prezentację.
- Otrzymują przygotowane dane z kontrolerów/view modeli.

3. **Controller (C)**

- Klasy w `app/Http/Controllers`.
- Obsługują żądania HTTP, koordynują walidację/serwisy i zwracają odpowiedzi.
- Powinny pozostać „cienkie”: orkiestracja, a nie ciężka logika biznesowa.

4. **Przepływ żądania w ujęciu MVC**

- Route mapuje URL do akcji kontrolera.
- Kontroler używa modeli/serwisów do realizacji use case’u.
- Kontroler zwraca widok (HTML) lub odpowiedź JSON (API).

Laravel wspiera też service classes, actions, repozytoria i warstwy domenowe ponad MVC w większych aplikacjach.

</details>

<details>
<summary>4. Opisz cykl życia żądania w aplikacji Laravel.</summary>

#### Laravel

Cykl życia żądania w Laravel opisuje, jak przychodzące żądanie HTTP jest przekształcane w odpowiedź.

1. **Punkt wejścia**

- Serwer WWW kieruje ruch do `public/index.php`.
- Ładowany jest autoloader Composera i bootstrap aplikacji Laravel.

2. **Start kernela HTTP**

- Inicjalizowany jest service container.
- Przygotowywane są globalne i routowe stosy middleware.

3. **Service providery**

- Providery są rejestrowane i bootowane.
- Główne serwisy i bindowania aplikacji stają się dostępne.

4. **Faza routingu**

- Router dopasowuje metodę żądania + URI do trasy.
- Wykonywany jest pipeline middleware przypisany do trasy.

5. **Wykonanie kontrolera/handlera**

- Uruchamiana jest akcja kontrolera, closure albo klasa invokable.
- Zależności są automatycznie rozwiązywane z containera.
- Zachodzą: walidacja, autoryzacja, logika biznesowa i dostęp do danych.

6. **Tworzenie odpowiedzi**

- Handler zwraca `Response`, `JsonResponse`, widok, redirect albo serializowalne dane.
- Laravel normalizuje wynik do obiektu odpowiedzi HTTP.

7. **Faza zakończenia**

- Odpowiedź jest wysyłana do klienta.
- Uruchamiane są terminable middleware i hooki po wysłaniu odpowiedzi.

Ten cykl daje Laravelowi przewidywalny model wykonania i jasne punkty rozszerzeń.

</details>

<details>
<summary>5. Czym jest service container w Laravel?</summary>

#### Laravel

Service container w Laravel to kontener IoC (Inversion of Control), odpowiedzialny za tworzenie obiektów i zarządzanie zależnościami.

1. **Główna rola**

- Centralne miejsce, gdzie klasy/interfejsy są wiązane z konkretnymi implementacjami.
- Automatycznie rozwiązuje zależności konstruktora przez refleksję.

2. **Dlaczego to ważne**

- Ogranicza ręczne „spinanie” obiektów.
- Umożliwia dependency inversion (zależność od interfejsów, nie od klas konkretnych).
- Poprawia testowalność przez podmianę implementacji (np. fake/mock).

3. **Gdzie jest używany**

- Kontrolery, middleware, joby, listenery, komendy i klasy serwisowe.
- Wewnętrzne mechanizmy frameworka i własna architektura aplikacji.

4. **Typowe API**

- `bind()` dla wiązań transient.
- `singleton()` dla jednej współdzielonej instancji.
- `make()` / `app()` do rozwiązywania serwisów.

5. **Efekt praktyczny**

- Czystsze konstruktory, mniejsze sprzężenie, lepszy modularny design.

W Laravel service container jest jednym z kluczowych fundamentów skalowalnej architektury aplikacji.

</details>

<details>
<summary>6. Wyjaśnij różnicę między bindingiem, singleton bindingiem i resolvingiem w service containerze.</summary>

#### Laravel

Te pojęcia opisują różne operacje w cyklu życia containera w Laravel.

1. **Binding (`bind`)**

- Rejestruje sposób budowania typu przez container.
- Tworzy **nową instancję przy każdym resolve** (cykl życia transient).

```php
$this->app->bind(PaymentGateway::class, StripeGateway::class);
```

2. **Singleton binding (`singleton`)**

- Rejestruje typ jako **współdzieloną instancję**.
- Pierwszy resolve ją tworzy, kolejne zwracają ten sam obiekt.

```php
$this->app->singleton(CacheClient::class, fn () => new CacheClient());
```

3. **Resolving (`make` / auto-injection)**

- Czynność proszenia containera o dostarczenie instancji.
- Może zachodzić jawnie (`app()->make(...)`) albo niejawnie przez injection w konstruktorze.

```php
$gateway = app()->make(PaymentGateway::class);
```

4. **Praktyczna zasada**

- `bind` dla serwisów stateless/lekkich.
- `singleton` dla współdzielonych/cięższych/stanowych klientów infrastrukturalnych.
- W klasach zarządzanych przez framework preferuj automatyczny resolving przez dependency injection.

</details>

<details>
<summary>7. Czym jest contextual binding i kiedy go używać?</summary>

#### Laravel

Contextual binding pozwala dostarczać różne implementacje tego samego interfejsu w zależności od tego, która klasa jest aktualnie rozwiązywana.

1. **Jaki problem rozwiązuje**

- Wielu konsumentów potrzebuje tego samego kontraktu, ale innego zachowania implementacji.

2. **Przykładowy scenariusz**

- `PhotoController` powinien używać `S3Filesystem`.
- `ReportController` powinien używać `LocalFilesystem`.
- Oba zależą od `FilesystemInterface`.

3. **API containera**

```php
$this->app->when(PhotoController::class)
    ->needs(FilesystemInterface::class)
    ->give(S3Filesystem::class);

$this->app->when(ReportController::class)
    ->needs(FilesystemInterface::class)
    ->give(LocalFilesystem::class);
```

4. **Kiedy używać**

- Integracje multi-tenant lub multi-region.
- Różne adaptery dla różnych use case’ów.
- Utrzymanie projektowania opartego na interfejsach bez globalnych konfliktów bindingów.

Contextual binding jest przydatny, gdy jeden globalny binding to za mało i zachowanie musi zależeć od kontekstu konsumenta.

</details>

<details>
<summary>8. Czym są Service Providery i jaki jest ich cel?</summary>

#### Laravel

Service Providery to centralny mechanizm bootstrapu w Laravel do rejestrowania i konfigurowania serwisów aplikacji.

1. **Główny cel**

- Rejestrowanie bindingów w containerze.
- Konfigurowanie serwisów pakietu/aplikacji podczas startu.

2. **Co zwykle się tam umieszcza**

- Bindings interfejs -> implementacja.
- Rejestracje singletonów dla serwisów infrastrukturalnych.
- Rejestrację eventów/listenerów (lub w osobnym providerze).
- Bootstrap pakietów i spięcie konfiguracji.

3. **Domyślne przykłady**

- `AppServiceProvider`
- `RouteServiceProvider`
- Providery pakietów

4. **Dlaczego to ważne**

- Tworzy przewidywalną warstwę startową.
- Trzyma logikę bootstrapu poza kontrolerami/modelami.
- Poprawia modularność i utrzymywalność w większych aplikacjach.

Service Providery są w praktyce composition rootem aplikacji Laravel.

</details>

<details>
<summary>9. Jaka jest różnica między `registering` a `booting` w service providerze?</summary>

#### Laravel

W Service Providerze metody `register()` i `boot()` uruchamiają się na różnych etapach i mają różne odpowiedzialności.

1. **`register()`**

- Służy wyłącznie do bindowania rzeczy w containerze.
- Powinna być wolna od efektów ubocznych i nie powinna zależeć od serwisów z innych providerów, które jeszcze nie zostały zbootowane.

```php
public function register(): void
{
    $this->app->singleton(PaymentGateway::class, StripeGateway::class);
}
```

2. **`boot()`**

- Uruchamia się po zarejestrowaniu wszystkich providerów.
- Używana do działań wymagających już dostępnych serwisów: routes, view composery, obserwery, spięcie eventów, macros.

```php
public function boot(): void
{
    Schema::defaultStringLength(191);
}
```

3. **Praktyczne rozróżnienie**

- `register()` = deklarowanie zależności.
- `boot()` = wykonywanie logiki integracyjnej frameworka.

Poprawne rozdzielenie tych ról zapobiega błędom kolejności bootowania i utrzymuje przewidywalne zachowanie startu aplikacji.

</details>

<details>
<summary>10. Czym są Laravel Contracts?</summary>

#### Laravel

Laravel Contracts to zdefiniowane przez framework interfejsy PHP, które opisują kluczowe możliwości serwisów niezależnie od ich implementacji.

1. **Czym są**

- Interfejsy w przestrzeni `Illuminate\Contracts\...`.
- Przykłady: `Cache\Repository`, `Queue\Queue`, `Auth\Guard`, `Mail\Mailer`.

2. **Dlaczego istnieją**

- Oddzielają Twój kod od konkretnych klas frameworka.
- Umożliwiają czyste dependency inversion i łatwiejsze testowanie.
- Pozwalają podmieniać implementacje przy minimalnych zmianach kodu.

3. **Jak się ich używa**

- Type-hint kontraktu w konstruktorze/metodzie.
- Pozwól containerowi rozwiązać aktualną implementację.

```php
use Illuminate\Contracts\Cache\Repository as Cache;

final class UserService
{
    public function __construct(private Cache $cache) {}
}
```

4. **Korzyść praktyczna**

- Bardziej utrzymywalna architektura i wyraźniejsze granice.
- Lepsze mocki/fake’i w testach.
- Łatwiejsza migracja szczegółów infrastrukturalnych.

Contracts to kluczowy element pisania kodu Laravel, który jest przyjazny frameworkowi, ale niezależny od konkretnych implementacji.

</details>

<details>
<summary>11. Jaka jest różnica między Contract a Facade?</summary>

#### Laravel

Contracts i Facades są powiązane z serwisami Laravel, ale rozwiązują różne problemy.

1. **Contract**

- Interfejs PHP (zwykle w `Illuminate\Contracts\...`).
- Definiuje zachowanie/możliwości bez szczegółów implementacji.
- Służy do dependency inversion i czystej architektury.

2. **Facade**

- Statycznie wyglądający proxy do serwisu rozwiązywanego z containera.
- Zapewnia zwięzłą składnię wywołań usług frameworka.
- Przykład: `Cache::get('key')`, `Log::info('...')`.

3. **Kluczowa różnica**

- Contract = granica abstrakcji (zależność na etapie projektowania).
- Facade = warstwa wygodnego dostępu (API stylu wywołań).

4. **Wpływ na testowanie**

- Contracts łatwo mockować przez DI.
- Facades też da się mockować (`Facade::shouldReceive()`), ale nadal to styl „quasi-statyczny”.

5. **Kiedy co preferować**

- Preferuj Contracts w serwisach domenowych/aplikacyjnych.
- Używaj Facades w kontrolerach, małym glue code lub obszarach silnie frameworkowych, gdzie zwięzłość pomaga.

Krótko: Contract definiuje *co* robi serwis, a Facade daje *jak wygodnie* go wywołać.

</details>

<details>
<summary>12. Wyjaśnij różnicę między Facades a funkcjami helper w Laravel.</summary>

#### Laravel

Zarówno Facades, jak i helpery dają zwięzłą składnię, ale różnią się strukturą, wykrywalnością i semantyką testowania.

1. **Facades**

- Statycznie wyglądający proxy oparty o klasę (`Cache::`, `DB::`, `Bus::`).
- Mapowane do serwisów containera.
- Wspierają API do mockowania/fake’owania facade.
- Lepsza wykrywalność w IDE dzięki metodom klas.

2. **Funkcje helper**

- Funkcje globalne, np. `app()`, `route()`, `now()`, `config()`, `request()`, `response()`.
- Bardzo krótkie i wygodne w szablonach/kontrolerach.
- W użyciu nie są powiązane z nazwą klasy.

3. **Kluczowe różnice**

- Facade: jawna powierzchnia serwisu przez klasę.
- Helper: lekki globalny skrót.

4. **Testowanie i architektura**

- W kluczowym kodzie biznesowym DI przez konstruktor jest zwykle czystsze niż oba style.
- W frameworkowym glue code oba podejścia są akceptowalne; facades bywają bardziej jawne, helpery bardziej zwięzłe.

5. **Praktyczna wskazówka**

- W serwisach domenowych preferuj DI + contracts.
- Facades/helperów używaj pragmatycznie w kontrolerach, jobach, widokach i kodzie integracyjnym z frameworkiem.

</details>

<details>
<summary>13. Jak działa Dependency Injection w Laravel?</summary>

#### Laravel

Dependency Injection (DI) w Laravel jest napędzane przez service container, który automatycznie rozwiązuje zależności klas.

1. **Wstrzykiwanie przez konstruktor**

- Deklarujesz zależności przez type-hint w konstruktorze.
- Laravel rozwiązuje je i wstrzykuje podczas tworzenia klasy.

```php
final class OrderController
{
    public function __construct(private OrderService $service) {}
}
```

2. **Wstrzykiwanie do metod**

- Działa w akcjach kontrolerów, handlerach jobów, listenerach, komendach itd.
- Parametry z type-hintem mogą być auto-resolved.

```php
public function store(StoreOrderRequest $request, OrderService $service): JsonResponse
{
    // ...
}
```

3. **Wstrzykiwanie interfejsu**

- Jeśli wstrzykujesz interfejs, zbindować go trzeba do konkretnej klasy w providerze.

```php
$this->app->bind(PaymentGateway::class, StripeGateway::class);
```

4. **Dlaczego DI jest ważne**

- Niskie sprzężenie.
- Łatwe testowanie przez mocki/fake’i.
- Jawne zależności i lepsza utrzymywalność.

W Laravel DI to domyślny sposób czystego „okablowania” serwisów aplikacji.

</details>

<details>
<summary>14. Jak Laravel wykorzystuje IoC (Inversion of Control)?</summary>

#### Laravel

Laravel stosuje IoC, delegując tworzenie obiektów i spinanie zależności do service containera, zamiast hardkodować zależności wewnątrz klas.

1. **Podejście tradycyjne (bez IoC)**

- Klasa sama tworzy swoje zależności (`new StripeGateway()`), co powoduje silne sprzężenie.

2. **Z IoC w Laravel**

- Klasy deklarują wymagane abstrakcje (interfejsy/typy).
- Container dostarcza konkretne implementacje.

3. **Gdzie widać IoC**

- Kontrolery, middleware, joby, eventy/listenery, komendy, policies, własne serwisy.
- Wewnętrzne mechanizmy frameworka także opierają się na tym samym mechanizmie.

4. **Korzyści**

- Możliwość podmiany implementacji (np. Stripe vs PayPal).
- Lepsze testy jednostkowe i modularna architektura.
- Scentralizowana konfiguracja grafu obiektów w providerach.

IoC w Laravel to architektony fundament DI, contracts i testowalności.

</details>

<details>
<summary>15. Czym są middleware w Laravel?</summary>

#### Laravel

Middleware to klasy, które sprawdzają, filtrują lub transformują żądania/odpowiedzi HTTP, gdy przechodzą przez pipeline żądania.

1. **Cel**

- Wykonywanie concerns przekrojowych przed/po logice kontrolera.

2. **Typowe zastosowania**

- Sprawdzenia uwierzytelnienia/autoryzacji.
- Rate limiting.
- Ochrona CSRF.
- Logowanie żądań i nagłówki bezpieczeństwa.
- Lokalizacja oraz konfiguracja tenant/context.

3. **Model wykonania**

- Żądanie wchodzi do stosu middleware.
- Każde middleware decyduje, czy kontynuować (`$next($request)`), czy przerwać (zwrócić response/redirect/error).
- Odpowiedź może być też modyfikowana w drodze powrotnej.

4. **Typy**

- Global middleware (dla wszystkich żądań).
- Route middleware (przypisane do konkretnych tras/grup).

Middleware utrzymują kontrolery skupione na logice, przenosząc powtarzalne concerns HTTP do dedykowanych warstw pipeline’u.

</details>

<details>
<summary>16. Jak rejestrować i przypisywać middleware?</summary>

#### Laravel

W nowoczesnym Laravel middleware zwykle konfiguruje się w bootstrap/application configuration i przypisuje przez alias, grupę albo bezpośrednio klasą.

1. **Rejestrowanie aliasów/grup middleware**

- Zdefiniuj aliasy i skład grup w konfiguracji middleware podczas bootstrapu aplikacji.
- Typowe aliasy to m.in. `auth`, `verified`, `throttle`.

2. **Global middleware**

- Dodawane do globalnego stosu, więc działają dla każdego żądania.

3. **Przypisywanie do tras**

- Dla pojedynczej trasy:

```php
Route::get('/profile', ProfileController::class)
    ->middleware('auth');
```

- Dla grupy tras:

```php
Route::middleware(['auth', 'verified'])->group(function () {
    Route::get('/dashboard', DashboardController::class);
});
```

4. **Przez nazwę klasy**

- W razie potrzeby middleware można podpiąć bezpośrednio klasą, zamiast aliasu.

Praktyczne podejście: używaj aliasów dla czytelności i spójności w całej codebase.

</details>

<details>
<summary>17. Jak middleware działa z parametrami?</summary>

#### Laravel

Middleware w Laravel może przyjmować parametry z definicji tras, co pozwala konfigurować zachowanie bez duplikowania klas middleware.

1. **Użycie w trasie**

```php
Route::get('/admin', AdminController::class)
    ->middleware('role:admin');
```

2. **Sygnatura middleware**

```php
public function handle(Request $request, Closure $next, string $role): Response
{
    if (! $request->user() || ! $request->user()->hasRole($role)) {
        abort(403);
    }

    return $next($request);
}
```

3. **Wiele parametrów**

- Przekazywane jako wartości rozdzielone przecinkami: `middleware('throttle:60,1')`.
- Middleware otrzymuje je jako dodatkowe argumenty po `$next`.

4. **Kiedy to przydatne**

- Sprawdzanie ról/uprawnień.
- Warianty rate limitingu.
- Ograniczenia feature/tenant zależnie od kontekstu trasy.

Middleware parametryzowane poprawia reużywalność i utrzymuje jawny zamiar na poziomie tras.

</details>

<details>
<summary>18. Czym są route groups, prefixy i middleware groups?</summary>

#### Laravel

Grupowanie tras pomaga porządkować routing i stosować współdzieloną konfigurację tylko raz.

1. **Route groups**

- Łączą trasy pod wspólnymi atrybutami (`middleware`, `prefix`, `name`, `namespace` itd.).

2. **Prefixy**

- Dodają prefiks URI do wszystkich tras w grupie.

```php
Route::prefix('api/v1')->group(function () {
    Route::get('/users', [UserController::class, 'index']);
});
```

3. **Prefixy nazw**

- Dodają wspólny prefiks nazw tras.

```php
Route::name('admin.')->group(function () {
    Route::get('/dashboard', [AdminController::class, 'dashboard'])->name('dashboard');
});
// Nazwa trasy: admin.dashboard
```

4. **Middleware groups**

- Nazwany zestaw middleware (np. `web`, `api`), który można zastosować razem.
- Ogranicza powtórzenia i standaryzuje zachowanie w sekcjach tras.

5. **Dlaczego to ważne**

- Czystsze pliki routingu.
- Spójne zasady bezpieczeństwa i obsługi żądań.
- Łatwiejsze utrzymanie wraz ze wzrostem aplikacji.

</details>

<details>
<summary>19. Czym jest route model binding?</summary>

#### Laravel

Route model binding automatycznie rozwiązuje parametry trasy do instancji modeli Eloquent.

1. **Co robi**

- Zamienia segment trasy jak `{user}` na obiekt modelu `User`.
- Jeśli model nie zostanie znaleziony, Laravel automatycznie zwraca `404`.

2. **Przykład**

```php
Route::get('/users/{user}', [UserController::class, 'show']);

public function show(User $user): View
{
    return view('users.show', compact('user'));
}
```

3. **Korzyści**

- Usuwa powtarzalny boilerplate z `findOrFail()`.
- Poprawia czytelność i type safety.
- Daje scentralizowaną kontrolę nad zachowaniem wyszukiwania.

4. **Zaawansowane użycie**

- Własne klucze tras (np. slug).
- Scoped/nested bindings dla relacji parent-child.

Route model binding to jedna z najbardziej użytecznych konwencji Laravel do zwięzłego i bezpiecznego kodu kontrolerów.

</details>

<details>
<summary>20. Wyjaśnij implicit vs explicit route model binding.</summary>

#### Laravel

Oba podejścia rozwiązują parametry trasy do modeli, ale różnią się stylem konfiguracji.

1. **Implicit binding**

- Laravel wnioskuje binding na podstawie nazwy parametru + type-hintu.
- Wymaga minimalnej konfiguracji.

```php
Route::get('/posts/{post}', fn (Post $post) => $post);
```

2. **Explicit binding**

- Ręcznie definiujesz, jak parametr mapuje się na model.
- Przydatne przy niestandardowej logice lub nietypowym sposobie rozwiązywania.

```php
Route::bind('post', function (string $value) {
    return Post::where('slug', $value)->firstOrFail();
});
```

3. **Kiedy co wybrać**

- Domyślnie używaj implicit binding (czyste i konwencyjne).
- Explicit binding stosuj dla specjalnych reguł wyszukiwania, customowych transformacji lub edge case’ów.

4. **Powiązana customizacja**

- W wielu przypadkach wystarczy nadpisać `getRouteKeyName()` w modelu (np. dla sluga), bez pełnego explicit bindingu.

Implicit = automatyczny binding oparty na konwencji. Explicit = ręcznie kontrolowane zachowanie bindingu.

</details>

<details>
<summary>21. Czym jest rate limiting w Laravel i jak działa?</summary>

#### Laravel

Rate limiting kontroluje, ile żądań klient może wykonać w danym oknie czasowym, aby chronić API przed nadużyciami i przeciążeniem.

1. **Co robi**

- Ogranicza częstotliwość żądań per klucz (ID użytkownika, IP, token lub własny identyfikator).
- Zwraca `429 Too Many Requests`, gdy limit zostanie przekroczony.

2. **Jak Laravel to implementuje**

- Używa nazwanych limiterów definiowanych przez `RateLimiter::for(...)`.
- Stosuje limiter przez middleware (najczęściej `throttle`).
- Przechowuje liczniki przez backend cache (Redis/Memcached/database cache zależnie od konfiguracji).

3. **Podstawowy przykład**

```php
RateLimiter::for('api', function (Request $request) {
    return Limit::perMinute(60)->by($request->user()?->id ?: $request->ip());
});
```

4. **Gdzie stosować**

- Publiczne endpointy API.
- Logowanie, OTP, reset hasła i inne wrażliwe endpointy.
- Kosztowne operacje (wyszukiwanie, eksport, generowanie raportów).

5. **Dlaczego to ważne**

- Poprawia niezawodność i fairness.
- Ogranicza ryzyko brute-force i wpływ skoków ruchu.

</details>

<details>
<summary>22. Czym są invokable controllers?</summary>

#### Laravel

Invokable controllers to klasy kontrolerów z jedną metodą `__invoke()`, zaprojektowane pod jedną konkretną akcję.

1. **Struktura**

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

3. **Korzyści**

- Bardzo skoncentrowana odpowiedzialność.
- Czystsze mapowanie route -> action.
- Dobrze pasują do architektury action-oriented.

4. **Kiedy przydatne**

- Endpointy o jasnym, pojedynczym celu.
- Styl CQRS/action-based.
- Duże codebase’y, gdzie mniejsze klasy ułatwiają nawigację.

Invokable controllers to praktyczny sposób na utrzymanie warstwy HTTP jako jawnej i modularnej.

</details>

<details>
<summary>23. Czym są Single Action Controllers?</summary>

#### Laravel

Single Action Controllers to to samo podejście co invokable controllers: jedna klasa kontrolera obsługuje jedną akcję przez `__invoke()`.

1. **Główna idea**

- Jedna klasa = jeden use case.
- Brak wielu metod typu `index/store/update` w tym samym kontrolerze.

2. **Dlaczego zespoły ich używają**

- Lepsza separacja odpowiedzialności.
- Łatwiejsze testowanie per endpoint.
- Mniej konfliktów merge w dużych zespołach.

3. **Przykładowe use case’y**

- `ApproveInvoiceController`
- `SendWelcomeEmailController`
- `GenerateReportController`

4. **Trade-off**

- Więcej plików/klas.
- Ale zwykle lepsza długoterminowa utrzymywalność w projektach średnich i dużych.

Single Action Controllers to w istocie wybór stylu architektonicznego, który stawia na klarowność i skalę.

</details>

<details>
<summary>24. Jaka jest różnica między Resource Controllers a API Resource Controllers?</summary>

#### Laravel

Różnica dotyczy głównie generowanych akcji i docelowego stylu odpowiedzi.

1. **Resource Controller (`Route::resource`)**

- Generuje pełne trasy CRUD dla weba:
  `index`, `create`, `store`, `show`, `edit`, `update`, `destroy`.
- Zawiera trasy `create` i `edit`, zwykle dla formularzy/widoków HTML.

2. **API Resource Controller (`Route::apiResource`)**

- Generuje trasy CRUD zorientowane na API:
  `index`, `store`, `show`, `update`, `destroy`.
- Pomija `create` i `edit` (strony formularzy UI nie są potrzebne w API).

3. **Typowe użycie**

- `resource`: serwerowo renderowane aplikacje webowe.
- `apiResource`: API JSON, backendy mobilne, backendy dla SPA.

4. **Powiązana koncepcja**

- Odpowiedzi API często formatuje się klasami `JsonResource`, by utrzymać spójne kontrakty wyjścia.

</details>

<details>
<summary>25. Jak tworzyć własne komendy Artisan?</summary>

#### Laravel

Własne komendy Artisan to klasy CLI używane do automatyzacji, zadań utrzymaniowych, importów i workflow operacyjnych.

1. **Wygeneruj klasę komendy**

```bash
php artisan make:command SyncInvoicesCommand
```

2. **Zdefiniuj sygnaturę i opis**

```php
protected $signature = 'billing:sync {--dry-run}';
protected $description = 'Sync invoices from billing provider';
```

3. **Zaimplementuj logikę w `handle()`**

```php
public function handle(): int
{
    // logika komendy
    return self::SUCCESS;
}
```

4. **Używaj DI w komendzie**

- Wstrzykuj serwisy przez konstruktor albo rozwiązywanie na poziomie metod.

5. **Uruchom komendę**

```bash
php artisan billing:sync --dry-run
```

6. **Opcjonalne harmonogramowanie**

- Zarejestruj w schedulerze, aby uruchamiała się automatycznie przez cron.

Własne komendy są idealne do powtarzalnych operacji backendowych i automatyzacji przyjaznej DevOps.

</details>

<details>
<summary>26. Czym są makra i kiedy są przydatne?</summary>

#### Laravel

Makra pozwalają dodawać własne metody do klas frameworka w runtime (klasy macroable), bez modyfikowania kodu źródłowego frameworka.

1. **Częste cele macroable**

- `Collection`, `Str`, `ResponseFactory`, `Route` itd.

2. **Przykład**

```php
use Illuminate\Support\Collection;

Collection::macro('toKeyValue', function (string $key, string $value) {
    return $this->mapWithKeys(fn ($item) => [$item[$key] => $item[$value]]);
});
```

3. **Kiedy przydatne**

- Powtarzalna logika utility w całej codebase.
- Domenowe helpery dla kolekcji/stringów.
- Czystsze, ekspresyjne API dla częstych transformacji.

4. **Dobre praktyki**

- Rejestruj makra w service providerze.
- Trzymaj jasne nazwy, aby unikać kolizji.
- Nie nadużywaj; dla złożonego zachowania lepsze są zwykłe klasy.

Makra są najlepsze dla małych, reużywalnych rozszerzeń frameworka o wysokiej częstotliwości użycia.

</details>

<details>
<summary>27. Czym są Actions w architekturze Laravel i kiedy ich używać?</summary>

#### Laravel

Actions to wyspecjalizowane klasy enkapsulujące pojedynczy use case biznesowy (operację aplikacyjną).

1. **Czym jest Action**

- Klasa typu `CreateOrderAction`, `PublishPostAction`, `RefundPaymentAction`.
- Zwykle udostępnia jedną metodę (`handle()` albo `execute()`).

2. **Dlaczego używać Actions**

- Usuwają logikę biznesową z kontrolerów/modeli.
- Można je reużywać z kontrolerów HTTP, jobów, komend konsolowych i listenerów.
- Łatwiejsze testy jednostkowe dzięki czytelnemu input/output.

3. **Typowa struktura**

```php
final class CreateOrderAction
{
    public function __construct(private OrderRepository $orders) {}

    public function handle(CreateOrderData $data): Order
    {
        // logika biznesowa
    }
}
```

4. **Kiedy używać**

- Nietrywialne use case’y z regułami orkiestracji.
- Logika używana ponownie przez wiele punktów wejścia.
- Zespoły stosujące architekturę service/action lub podejście zbliżone do CQRS.

Actions poprawiają modularność i czynią workflow biznesowy bardziej jawnym.

</details>

<details>
<summary>28. Wyjaśnij Repository Pattern i jego korzyści.</summary>

#### Laravel

Repository Pattern abstrahuje dostęp do danych za interfejsami, dzięki czemu logika biznesowa nie jest silnie sprzężona ze szczegółami ORM/query.

1. **Główna idea**

- Definiujesz kontrakt (np. `OrderRepository`).
- Dostarczasz implementację (np. `EloquentOrderRepository`).
- Wstrzykujesz repozytorium do serwisów/actions.

2. **Korzyści**

- Wyraźna separacja logiki domenowej/aplikacyjnej od persystencji.
- Łatwiejsze testowanie z fake/in-memory repozytoriami.
- Scentralizowana złożona logika zapytań i strategie cache.
- Łatwiejsze przyszłe zmiany źródła danych.

3. **Trade-offy**

- Dodatkowa warstwa abstrakcji i więcej boilerplate’u.
- Nie zawsze potrzebne w prostych aplikacjach CRUD-heavy.

4. **Pragmatyczna wskazówka**

- Używaj repozytoriów tam, gdzie dostęp do danych jest złożony lub współdzielony.
- Unikaj over-engineeringu prostych modułów.

Repository Pattern jest wartościowy, gdy redukuje sprzężenie i złożoność, a nie gdy tylko dodaje pośrednictwo.

</details>

<details>
<summary>29. Czym są Traits w PHP i jak są używane w Laravel?</summary>

#### Laravel

Traits to elementy języka PHP do horyzontalnego reużywania kodu między klasami bez dziedziczenia.

1. **Co dają traits**

- Reużywalne metody/properties dołączane przez `use`.
- Wspólne zachowanie dla niepowiązanych klas.

2. **Przykłady użycia w Laravel**

- Traity frameworkowe, takie jak `SoftDeletes`, `HasFactory`, `Notifiable`, `AuthorizesRequests`, `DispatchesJobs`, `ValidatesRequests`.

3. **Przykład modelu**

```php
use Illuminate\Database\Eloquent\SoftDeletes;

class Post extends Model
{
    use SoftDeletes;
}
```

4. **Dobre praktyki**

- Utrzymuj traity małe i spójne.
- Używaj traitów do reużywania zachowań, a nie do ukrywania zbyt szerokich odpowiedzialności klasy.
- Dla złożonej logiki domenowej preferuj composition/serwisy.

Traity to praktyczny mechanizm reużycia, intensywnie używany wewnątrz Laravel i w kodzie aplikacji.

</details>

<details>
<summary>30. Jakie są różnice między Laravel a Lumen i czy Lumen jest nadal istotny w 2026 roku?</summary>

#### Laravel

Laravel i Lumen mają wspólne korzenie, ale celują w różne kompromisy rozwojowe.

1. **Główne różnice**

- **Laravel**: pełny framework (bogaty ekosystem, pakiety first-party, rozbudowane konwencje, szerokie wsparcie integracji).
- **Lumen**: wariant micro-frameworka, skupiony na minimalnym narzucie i prostszych setupach w stylu API.

2. **Architektura i ekosystem**

- Laravel ma szerszą kompatybilność z pakietami first-party i pełniejsze narzędzia deweloperskie.
- Lumen jest celowo „szczuplejszy” i nie dąży do pełnej kompatybilności z szeroką powierzchnią pakietów Laravel.

3. **Kontekst wydajności**

- Historycznie Lumen był wybierany do lekkich API.
- W nowoczesnych wersjach wydajność Laravel znacząco wzrosła, zmniejszając praktyczną różnicę dla wielu obciążeń.

4. **Czy Lumen jest istotny w 2026?**

- **Dla nowych projektów:** ogólnie **niezalecany** według guidance ekosystemu Laravel.
- **Dla istniejących systemów:** nadal istotny, jeśli już działa stabilnie na produkcji.
- **Domyślny wybór w 2026:** Laravel (po poprawnej optymalizacji) dla większości nowych backendów API i web.

5. **Praktyczna zasada decyzyjna**

- Nowe produkty zaczynaj na Laravel.
- Lumen utrzymuj tylko przy serwisach legacy, gdy są ku temu jasne powody operacyjne.

</details>

<details>
<summary>31. Czym jest Eloquent ORM?</summary>

#### Laravel

Eloquent ORM to implementacja Active Record w Laravel, która pozwala pracować z bazą danych przez obiekty PHP zamiast surowego SQL.

1. **Co zapewnia**

- Mapowanie model -> tabela.
- Integrację z query builderem.
- Zarządzanie relacjami.
- Casty atrybutów, accessors/mutators, scope’y, eventy.

2. **Dlaczego zespoły go używają**

- Szybszy development dzięki ekspresyjnej składni.
- Czystszy kod domenowy dla typowych workflow CRUD.
- Wbudowane konwencje ograniczające boilerplate.

3. **Przykład**

```php
$users = User::query()
    ->where('is_active', true)
    ->latest()
    ->take(10)
    ->get();
```

4. **Ważna uwaga**

- Eloquent świetnie sprawdza się w większości use case’ów aplikacyjnych.
- Dla mocno wyspecjalizowanych/zestawieniowych zapytań lepszy bywa raw SQL albo query builder.

Eloquent to domyślna warstwa dostępu do danych w aplikacjach Laravel.

</details>

<details>
<summary>32. Czym są modele Eloquent?</summary>

#### Laravel

Modele Eloquent to klasy PHP reprezentujące tabele bazy danych i enkapsulujące zachowanie danych.

1. **Główna rola**

- Każdy model zwykle mapuje się na jedną tabelę.
- Instancje modelu reprezentują pojedyncze wiersze.

2. **Co zwykle zawierają modele**

- Atrybuty fillable/guarded.
- Casty i obsługę dat.
- Relacje.
- Scope’y i metody domenowe.

3. **Podstawowy przykład**

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

4. **Dlaczego są ważne**

- Centralizują logikę persystencji i zachowania encji.
- Poprawiają czytelność i spójność operacji na danych.

Modele Eloquent to podstawowe klocki aplikacji Laravel opartych o bazę danych.

</details>

<details>
<summary>33. Wyjaśnij relacje one-to-one, one-to-many, many-to-many i polymorphic.</summary>

#### Laravel

Relacje Eloquent definiują, jak modele są ze sobą powiązane w modelu danych.

1. **One-to-one (`hasOne` / `belongsTo`)**

- Jeden rekord jest powiązany dokładnie z jednym rekordem.
- Przykład: `User` ma jeden `Profile`.

2. **One-to-many (`hasMany` / `belongsTo`)**

- Jeden rodzic ma wiele dzieci.
- Przykład: `Post` ma wiele `Comment`.

3. **Many-to-many (`belongsToMany`)**

- Obie strony mogą mieć wiele powiązanych rekordów.
- Wymaga tabeli pivot.
- Przykład: `User` należy do wielu `Role`.

4. **Polymorphic**

- Model może należeć do więcej niż jednego typu rodzica przez wspólny interfejs.
- Przykład: `Comment` może należeć do `Post` albo `Video`.

5. **Dlaczego to ważne**

- Relacje pozwalają jasno wyrazić strukturę domeny.
- Eloquent może ładować powiązane dane, ograniczać zapytania i upraszczać joiny.

Dobór właściwego typu relacji jest kluczowy dla czystego projektu schematu i wydajnych zapytań.

</details>

<details>
<summary>34. Czym są relacje polimorficzne i kiedy ich używać?</summary>

#### Laravel

Relacje polimorficzne pozwalają jednemu modelowi wiązać się z wieloma typami modeli, używając jednej pary kolumn (zwykle `*_type` i `*_id`).

1. **Jak to działa**

- Tabela dziecka przechowuje typ rodzica + ID rodzica.
- Jeden model dziecka może wskazywać różne modele rodzica.

2. **Typowe przykłady**

- `Comment` dla `Post`, `Video`, `Product`.
- `Image` przypięty do `User`, `Team`, `Article`.
- `Activity` celujące w różne typy encji.

3. **Metody relacji w Laravel**

- `morphTo` po stronie dziecka.
- `morphMany` / `morphOne` po stronie rodzica.
- `morphToMany` / `morphedByMany` dla relacji many-to-many polimorficznych.

4. **Kiedy używać**

- Gdy zachowanie jest współdzielone między heterogenicznymi encjami rodzica.
- Gdy chcesz jedną reużywalną tabelę dziecka zamiast wielu równoległych tabel.

5. **Trade-off**

- Bardziej elastyczny schemat, ale potencjalnie większa złożoność zapytań i potrzeba uważnego indeksowania.

Używaj relacji polimorficznych, gdy redukują duplikację i naturalnie pasują do modelu domeny.

</details>

<details>
<summary>35. Czym jest eager loading?</summary>

#### Laravel

Eager loading oznacza ładowanie powiązanych modeli z wyprzedzeniem, jako część głównego przepływu zapytania, zamiast dogrywania każdej relacji później osobno dla każdego elementu.

1. **Jak to zrobić**

```php
$posts = Post::with(['author', 'comments'])->latest()->get();
```

2. **Dlaczego to ważne**

- Redukuje łączną liczbę zapytań.
- Zapobiega problemowi N+1.
- Poprawia czas odpowiedzi i efektywność bazy danych.

3. **Przydatne warianty**

- Zagnieżdżony eager loading: `with('comments.user')`.
- Eager loading z ograniczeniami przez closures.
- Domyślny eager loading przez `$with` w modelu, gdy zawsze potrzebny.

Eager loading to podstawowa praktyka optymalizacyjna w aplikacjach opartych o Eloquent.

</details>

<details>
<summary>36. Czym jest problem zapytań N+1 i jak go rozwiązać?</summary>

#### Laravel

N+1 występuje wtedy, gdy wykonujesz 1 zapytanie po listę, a następnie dodatkowe zapytanie dla każdego elementu po dane relacji.

1. **Typowy scenariusz**

- Pobierasz 100 postów.
- W pętli odwołujesz się do `$post->author`.
- Kończy się to 101 zapytaniami (1 + 100).

2. **Dlaczego to jest złe**

- Duża liczba zapytań.
- Wyższa latencja i większe obciążenie bazy.
- Słaba skalowalność pod ruchem.

3. **Jak rozwiązać w Laravel**

- Użyj eager loadingu przez `with()`.

```php
$posts = Post::with('author')->get();
```

- Użyj `load()` / `loadMissing()`, gdy masz już kolekcję modeli.
- Używaj narzędzi profilowania zapytań (Telescope/Debugbar/logi), by wykrywać hotspoty.

4. **Dobra praktyka**

- Przewiduj potrzebne relacje już na etapie budowy zapytania.
- Przeglądaj pętle po modelach pod kątem ukrytego lazy loadingu.

Rozwiązywanie N+1 to jedno z najbardziej wpływowych usprawnień wydajności Eloquent.

</details>

<details>
<summary>37. Czym jest lazy eager loading?</summary>

#### Laravel

Lazy eager loading ładuje relacje po tym, jak modele zostały już pobrane, ale nadal hurtowo, a nie per model.

1. **Kiedy się go używa**

- Najpierw pobrałeś modele.
- Później decydujesz, które relacje są potrzebne.

2. **Metody**

- `load()` ładuje wskazane relacje.
- `loadMissing()` ładuje tylko relacje, które nie są jeszcze załadowane.

```php
$posts = Post::latest()->take(50)->get();
$posts->load('author', 'comments');
```

3. **Dlaczego pomaga**

- Zapobiega N+1, zachowując elastyczny przepływ sterowania.
- Przydatne w logice warunkowej lub warstwowych serwisach.

4. **Różnica względem eager loadingu**

- Eager loading: `with()` przed wykonaniem zapytania.
- Lazy eager loading: `load()` po wykonaniu zapytania.

Lazy eager loading to praktyczny kompromis między elastycznością a wydajnością.

</details>

<details>
<summary>38. Czym są global scopes i local scopes?</summary>

#### Laravel

Scope’y to reużywalne ograniczenia zapytań w Eloquent.

1. **Global scopes**

- Stosowane automatycznie do wszystkich zapytań danego modelu.
- Dobre dla ograniczeń przekrojowych (np. izolacja tenantów, zachowanie soft delete, tylko aktywne rekordy).

2. **Local scopes**

- Wywoływane jawnie w zapytaniach, gdy są potrzebne.
- Definiują zwięzłe, reużywalne filtry.

```php
public function scopePublished(Builder $query): Builder
{
    return $query->whereNotNull('published_at');
}

$posts = Post::published()->get();
```

3. **Kiedy co wybrać**

- Global scope: domyślna reguła biznesowa, która ma działać prawie wszędzie.
- Local scope: opcjonalny filtr dla konkretnych use case’ów.

4. **Uwaga**

- Nadużywanie global scopes może nieoczekiwanie ukrywać dane; dokumentuj je wyraźnie.

Scope’y poprawiają spójność i ograniczają powtarzanie warunków zapytań.

</details>

<details>
<summary>39. Czym są query scopes?</summary>

#### Laravel

Query scopes to metody modelu, które enkapsulują reużywalne ograniczenia zapytań, dzięki czemu zapytania są czystsze i kompozycyjne.

1. **Wzorzec local query scope**

- Nazwa metody zaczyna się od `scope`.
- Wywołanie odbywa się bez tego prefiksu.

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

2. **Korzyści**

- Reużywalne filtry.
- Bardziej czytelne łańcuchy zapytań.
- Scentralizowana logika ograniczeń.

3. **Praktyczne użycie**

- Filtry statusu (`active`, `published`, `archived`).
- Okna czasowe (`recent`, `betweenDates`).
- Ograniczenia biznesowe (`visibleTo`, `forTenant`).

Query scopes to kluczowe narzędzie utrzymania ekspresyjnych i łatwych w utrzymaniu zapytań Eloquent.

</details>

<details>
<summary>40. Czym są accessors i mutators?</summary>

#### Laravel

Accessors i mutators definiują, jak atrybuty modelu są transformowane podczas odczytu i zapisu.

1. **Accessor**

- Transformuje wartość, gdy jest pobierana z modelu.

2. **Mutator**

- Transformuje wartość zanim zostanie zapisana w modelu.

3. **Nowoczesny styl (`Attribute`)**

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

4. **Typowe use case’y**

- Normalizacja inputu (trim/formatowanie wielkości liter).
- Prezentacja wartości wyliczonych/sformatowanych.
- Obsługa transformacji szyfrowania/deszyfrowania.

5. **Różnica względem casts**

- Casts obsługują typowe konwersje typów.
- Accessors/mutators obsługują customowe transformacje domenowe.

Pomagają utrzymać logikę transformacji atrybutów scentralizowaną i spójną.

</details>

<details>
<summary>41. Czym są casts w Eloquent?</summary>

#### Laravel

Casts definiują, jak Eloquent konwertuje atrybuty modelu między surowymi wartościami z bazy a typami PHP.

1. **Co robią casts**

- Automatycznie konwertują wartości przy odczycie i zapisie.
- Utrzymują spójną i type-safe obsługę atrybutów.

2. **Typowe typy castów**

- `integer`, `float`, `decimal:2`, `boolean`
- `datetime`, `immutable_datetime`
- `array`, `json`, `object`, `collection`
- `encrypted`, `hashed`

3. **Przykład**

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

4. **Dlaczego to ważne**

- Ogranicza ręczny kod parsowania/formatowania.
- Zapobiega subtelnym błędom typów.
- Poprawia czytelność kodu domenowego.

Casts to fundamentalna funkcja czystego zarządzania atrybutami modeli.

</details>

<details>
<summary>42. Czym są obiekty Attribute w nowoczesnym Laravel?</summary>

#### Laravel

Obiekty `Attribute` to nowoczesny sposób definiowania accessorów i mutatorów w jednym miejscu dla pola modelu.

1. **Główna idea**

- Metoda zwraca `Attribute::make(get: ..., set: ...)`.
- Jasno enkapsuluje transformacje odczytu i zapisu.

2. **Przykład**

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

3. **Korzyści**

- Czystsze niż legacy `getXxxAttribute` / `setXxxAttribute`.
- Grupuje zachowanie getter/setter w jednej metodzie.
- Łatwiejsze do czytania, testowania i utrzymania.

4. **Kiedy używać**

- Customowe formatowanie, normalizacja, logika szyfrowania albo mapowanie value-objectów na konkretnych atrybutach.

Obiekty Attribute to preferowany nowoczesny wzorzec accessor/mutator w aktualnych wersjach Laravel.

</details>

<details>
<summary>43. Czym są Eloquent Collections?</summary>

#### Laravel

Eloquent Collections to wyspecjalizowane obiekty kolekcji zwracane przez zapytania Eloquent, rozszerzające bazową `Collection` Laravel o zachowanie świadome modeli.

1. **Czym są**

- Zwracane przez metody takie jak `get()` oraz ładowanie relacji.
- Zawierają instancje modeli, a nie zwykłe tablice.

2. **Dodatkowe możliwości**

- Dziedziczą bogate API kolekcji (`map`, `filter`, `groupBy`, `pluck` itd.).
- Dodają helpery specyficzne dla Eloquent, np. `load()`, `loadMissing()`, `modelKeys()`, `fresh()`.

3. **Przykład**

```php
$users = User::where('is_active', true)->get(); // Eloquent Collection
$emails = $users->pluck('email');
```

4. **Dlaczego przydatne**

- Ekspresyjne transformacje po zapytaniu.
- Wygodne operacje zbiorcze na zestawach modeli.

Eloquent Collections łączą świadomość ORM z funkcyjnym stylem operacji na danych.

</details>

<details>
<summary>44. Jaka jest różnica między tablicami a kolekcjami?</summary>

#### Laravel

Tablice to natywne struktury danych PHP, a kolekcje to obiektowe opakowania z fluent API do transformacji.

1. **Tablice**

- Szybka natywna struktura.
- Dostęp przez składnię języka.
- Domyślnie mniej helperów wysokiego poziomu do transformacji.

2. **Kolekcje**

- Obiekt `Illuminate\Support\Collection`.
- Łańcuchowe metody: `map`, `filter`, `reduce`, `sortBy`, `groupBy` itd.
- Bardziej ekspresyjne i czytelne dla złożonych pipeline’ów danych.

3. **Przykład**

```php
$names = collect($users)
    ->filter(fn ($u) => $u->is_active)
    ->pluck('name')
    ->values();
```

4. **Kiedy czego używać**

- Używaj tablic do prostych, niskopoziomowych operacji.
- Używaj kolekcji dla czytelności i kompozycyjnych transformacji.

Kolekcje zamieniają niewielki narzut na znacznie lepszą ergonomię kodu aplikacyjnego.

</details>

<details>
<summary>45. Czym są Lazy Collections?</summary>

#### Laravel

Lazy Collections przetwarzają elementy jako strumień (oparty na generatorze), zamiast ładować wszystko naraz do pamięci.

1. **Kluczowa cecha**

- Pamięciooszczędna iteracja po bardzo dużych zbiorach danych.

2. **Jak działają**

- Elementy są generowane i przetwarzane pojedynczo.
- Łańcuch transformacji wykonuje się leniwie podczas iteracji.

3. **Typowe źródła**

- Zapytania `lazy()`.
- `cursor()` z Eloquent/query buildera.
- Własne generatory opakowane w `LazyCollection`.

4. **Kiedy używać**

- Skrypty migracji danych.
- Duże eksporty/importy.
- Joby w tle na milionach rekordów.

5. **Trade-off**

- Część operacji kolekcji wymagających pełnej materializacji jest mniej odpowiednia.

Lazy Collections są idealne, gdy bezpieczeństwo pamięci jest ważniejsze niż wygoda random access.

</details>

<details>
<summary>46. Jaki jest cel metody cursor()?</summary>

#### Laravel

`cursor()` zwraca leniwie iterowalny wynik, pozwalając przechodzić po rekordach jeden po drugim przy niskim zużyciu pamięci.

1. **Dlaczego warto używać**

- Unikasz ładowania pełnego zestawu wyników do RAM.
- Możesz wydajnie przetwarzać duże tabele.

2. **Przykład**

```php
foreach (User::where('is_active', true)->cursor() as $user) {
    // przetwarzanie użytkownika
}
```

3. **Cechy**

- Iteracja oparta na generatorze.
- Dobre dla pipeline’ów read/process.
- Działa dobrze z kolejkami i długotrwałymi jobami.

4. **Kiedy nie jest idealne**

- Gdy potrzebujesz random access do wszystkich wyników naraz.
- Gdy potrzebujesz ciężkiej materializacji pełnego grafu eager loading dla wszystkich rekordów.

`cursor()` to kluczowe narzędzie do skalowalnego przetwarzania rekord po rekordzie.

</details>

<details>
<summary>47. Czym jest chunking i kiedy używać chunk() lub lazy()?</summary>

#### Laravel

Chunking oznacza przetwarzanie wyników zapytania małymi partiami zamiast ładowania wszystkiego naraz.

1. **`chunk()`**

- Pobiera rekordy w partiach o stałym rozmiarze i wykonuje callback dla każdego chunka.

```php
User::query()->chunk(1000, function ($users) {
    foreach ($users as $user) {
        // przetwarzanie
    }
});
```

2. **`lazy()`**

- Wewnątrz też działa na chunkach, ale udostępnia je jako jeden leniwy strumień.
- Bardziej kompozycyjne dla kodu w stylu pipeline.

```php
User::query()->lazy(1000)->each(function (User $user) {
    // przetwarzanie
});
```

3. **Kiedy co wybrać**

- Użyj `chunk()` do jawnych operacji per partia.
- Użyj `lazy()` do płynnych transformacji strumieniowych.

4. **Ważna uwaga**

- Przy aktualizacji wierszy podczas iteracji preferuj warianty oparte o ID (`chunkById`, `lazyById`), aby uniknąć pomijania/duplikowania rekordów.

Chunking jest kluczowy dla przetwarzania dużych zbiorów danych przy kontrolowanym zużyciu pamięci.

</details>

<details>
<summary>48. Wyjaśnij query builder w Laravel.</summary>

#### Laravel

Laravel Query Builder to fluent API do budowy zapytań SQL, działające „nad” PDO i „pod” modelami Eloquent.

1. **Czym jest**

- Niezależny od konkretnej bazy interfejs zapytań przez `DB::table(...)`.
- Obsługuje selecty, joiny, where, grupowanie, sortowanie, paginację, inserty/updates/deletes.

2. **Przykład**

```php
$users = DB::table('users')
    ->select('id', 'name', 'email')
    ->where('is_active', true)
    ->orderByDesc('created_at')
    ->limit(20)
    ->get();
```

3. **Dlaczego używać**

- Daje większą kontrolę nad SQL niż wzorce wysokopoziomowego ORM.
- Świetny do zapytań raportowych i złożonych joinów.
- Nadal wspiera binding i bezpieczną obsługę parametrów przeciw SQL injection.

4. **Eloquent vs builder**

- Eloquent: modelocentryczny, bogate cechy domenowe.
- Query Builder: tabelo-/zapytaniocentryczny, niższy poziom i często bardziej „lekki”.

Query Builder to podstawowa fluent warstwa do precyzyjnej pracy z SQL w Laravel.

</details>

<details>
<summary>49. Jak wyświetlić surowe zapytania SQL w Laravel?</summary>

#### Laravel

SQL i bindingi można podejrzeć na kilka sposobów, zależnie od głębokości debugowania.

1. **`toSql()` + `getBindings()`**

```php
$query = User::where('email', 'like', '%@example.com%');

$sql = $query->toSql();
$bindings = $query->getBindings();
```

2. **`toRawSql()` (nowoczesny Laravel)**

- Zwraca SQL z podstawionymi bindingami dla łatwiejszego odczytu.

```php
$sql = User::where('id', 5)->toRawSql();
```

3. **Query listener**

```php
DB::listen(function ($query) {
    logger()->debug($query->sql, $query->bindings);
});
```

4. **Narzędzia**

- Laravel Telescope / Debugbar mogą pokazywać wykonane zapytania i czasy ich trwania.

Używaj tych metod w development/debugowaniu, a nie jako stałego outputu produkcyjnego.

</details>

<details>
<summary>50. Jakie metody agregujące są dostępne w query builderze?</summary>

#### Laravel

Laravel Query Builder udostępnia standardowe helpery agregujące SQL.

1. **Główne metody agregujące**

- `count()`
- `sum($column)`
- `avg($column)` / `average($column)`
- `min($column)`
- `max($column)`

2. **Przykłady**

```php
$totalUsers = DB::table('users')->count();
$totalRevenue = DB::table('orders')->sum('amount');
$avgOrder = DB::table('orders')->avg('amount');
$firstDate = DB::table('orders')->min('created_at');
$latestDate = DB::table('orders')->max('created_at');
```

3. **Przy zapytaniach grupowanych**

- Łącz `selectRaw(...)` + `groupBy(...)`, aby liczyć agregaty per grupa.

4. **Dlaczego to przydatne**

- Wydajne obliczenia po stronie serwera.
- Unikasz przenoszenia zbędnych wierszy do pamięci aplikacji.

Agregaty są kluczowe dla dashboardów, analityki i endpointów z metrykami biznesowymi.

</details>

<details>
<summary>51. Czym są transakcje bazodanowe i jak ich używać?</summary>

#### Laravel

Transakcja bazodanowa grupuje wiele operacji w jedną jednostkę atomową: albo wszystkie się powiodą, albo wszystkie zostaną wycofane.

1. **Dlaczego transakcje są potrzebne**

- Zachowują spójność danych przy powiązanych zapisach.
- Zapobiegają częściowym aktualizacjom, gdy wystąpi wyjątek.

2. **Użycie w Laravel**

```php
DB::transaction(function () use ($orderData) {
    $order = Order::create($orderData);
    Inventory::reserveForOrder($order);
    Payment::captureForOrder($order);
});
```

3. **Ręczna kontrola (opcjonalnie)**

```php
DB::beginTransaction();

try {
    // operacje
    DB::commit();
} catch (Throwable $e) {
    DB::rollBack();
    throw $e;
}
```

4. **Dobre praktyki**

- Trzymaj zakres transakcji mały i szybki.
- Unikaj długich zewnętrznych wywołań HTTP wewnątrz transakcji.
- Łącz z blokowaniem wierszy, gdy to potrzebne w flow wrażliwym na współbieżność.

Transakcje są krytyczne dla niezawodnych workflow finansowych, magazynowych i wieloetapowych procesów biznesowych.

</details>

<details>
<summary>52. Czym są migracje i dlaczego są ważne?</summary>

#### Laravel

Migracje to wersjonowane pliki PHP, które definiują zmiany schematu bazy danych w czasie.

1. **Co robią migracje**

- Tworzą/modyfikują/usuwają tabele, kolumny, indeksy i constraints.
- Utrzymują reprodukowalność zmian schematu między środowiskami.

2. **Dlaczego są ważne**

- Umożliwiają współpracę zespołu nad schematem z code review.
- Zapewniają deterministyczne deploymenty i rollbacki.
- Realizują podejście infrastructure-as-code dla ewolucji bazy.

3. **Typowa struktura migracji**

- `up()` stosuje zmiany.
- `down()` cofa zmiany.

4. **Wartość operacyjna**

- Łatwiejszy onboarding i setup CI.
- Mniejszy drift bazy typu „works on my machine”.

Migracje są fundamentem utrzymywalnego zarządzania cyklem życia schematu w Laravel.

</details>

<details>
<summary>53. Jak generować i cofać migracje?</summary>

#### Laravel

Laravel dostarcza komendy Artisan do tworzenia migracji i zarządzania ich wykonaniem.

1. **Generowanie migracji**

```bash
php artisan make:migration create_orders_table
php artisan make:migration add_status_to_orders_table --table=orders
```

2. **Uruchamianie migracji**

```bash
php artisan migrate
```

3. **Cofnięcie ostatniej paczki**

```bash
php artisan migrate:rollback
```

4. **Cofnięcie wielu kroków**

```bash
php artisan migrate:rollback --step=3
```

5. **Inne przydatne komendy**

- `php artisan migrate:reset` (cofnięcie wszystkich)
- `php artisan migrate:refresh` (reset + migrate)
- `php artisan migrate:fresh` (usuń wszystkie tabele + migrate)

Używaj komend rollback/refresh ostrożnie na środowiskach produkcyjnych.

</details>

<details>
<summary>54. Czym są seedery i factory?</summary>

#### Laravel

Seedery i factory pomagają wydajnie generować oraz wstawiać dane testowe lub początkowe.

1. **Seedery**

- Klasy, które zasilają bazę znanymi zestawami danych.
- Dobre dla danych bazowych/referencyjnych (role, uprawnienia, ustawienia).

2. **Factory**

- „Blueprinty” do generowania instancji modeli z fake/custom danymi.
- Przydatne w testach oraz danych demo/dev.

3. **Jak współdziałają**

- Seeder wywołuje factory, aby szybko utworzyć wiele rekordów.

```php
User::factory()->count(50)->create();
```

4. **Use case’y**

- Bootstrap lokalnego developmentu.
- Setup testów automatycznych.
- Generowanie danych dla środowisk staging/demo.

Seedery definiują co wstawić, a factory definiują jak generować dane modelu.

</details>

<details>
<summary>55. Jak działają factory w nowoczesnym Laravel?</summary>

#### Laravel

Nowoczesne factory w Laravel są oparte o klasy i zorientowane na modele, zwykle w `database/factories`.

1. **Factory oparte na definicji**

- `definition()` zwraca domyślne fake atrybuty.

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

- Nazwane warianty dla konkretnych scenariuszy.

```php
public function admin(): static
{
    return $this->state(fn () => ['is_admin' => true]);
}
```

3. **Użycie**

```php
User::factory()->admin()->count(3)->create();
User::factory()->make(); // niepersistowane
```

4. **Relacje**

- Factory wspierają tworzenie relacji przez `has()`, `for()` i callbacki.

Factory czynią generowanie danych testowych/dev ekspresyjnym, kompozycyjnym i deterministycznym.

</details>

<details>
<summary>56. Czym jest database seeding?</summary>

#### Laravel

Database seeding to proces wstawiania do bazy danych predefiniowanych lub wygenerowanych danych.

1. **Cel**

- Przygotowanie aplikacji z wymaganymi danymi początkowymi.
- Dostarczenie realistycznych zestawów danych do developmentu/testów.

2. **Jak to działa**

- Klasy seederów uruchamia się przez Artisan.

```bash
php artisan db:seed
php artisan db:seed --class=UserSeeder
```

3. **Typowy przepływ**

- `DatabaseSeeder` orkiestruje inne seedery.
- Factory są używane do masowego tworzenia syntetycznych rekordów.

4. **Dobre praktyki**

- Trzymaj kluczowe dane referencyjne deterministyczne.
- Unikaj destrukcyjnej logiki seedingu na produkcji, chyba że jest to celowe.
- Wersjonuj seedery razem z codebase.

Seeding zapewnia, że środowiska są reprodukowalne i gotowe do developmentu lub testów.

</details>

<details>
<summary>57. Czym są soft deletes?</summary>

#### Laravel

Soft deletes oznaczają rekordy jako usunięte bez fizycznego usuwania ich z tabeli.

1. **Jak to działa**

- Używa kolumny timestamp `deleted_at`.
- Usunięcie ustawia `deleted_at`; wiersz zostaje w DB.
- Domyślne zapytania wykluczają soft-usunięte rekordy.

2. **Włączenie w modelu**

```php
use Illuminate\Database\Eloquent\SoftDeletes;

class Post extends Model
{
    use SoftDeletes;
}
```

3. **Kluczowe helpery zapytań**

- `withTrashed()` uwzględnia usunięte wiersze.
- `onlyTrashed()` tylko usunięte wiersze.
- `restore()` przywraca rekord.
- `forceDelete()` usuwa trwale.

4. **Dlaczego przydatne**

- Lepsze odzyskiwanie danych i audytowalność.
- Bezpieczniejsze workflow biznesowe tam, gdzie ryzyko przypadkowego usunięcia jest wysokie.

Soft deletes to praktyczny kompromis między semantyką usuwania a możliwością odzyskiwania.

</details>

<details>
<summary>58. Jak optymalizować zapytania Eloquent pod wydajność?</summary>

#### Laravel

Optymalizacja wydajności Eloquent to przede wszystkim redukcja liczby zapytań, rozmiaru wierszy i zbędnej pracy modeli.

1. **Unikaj N+1**

- Używaj `with()` / `load()` dla relacji.

2. **Wybieraj tylko potrzebne kolumny**

```php
User::query()->select('id', 'name')->get();
```

3. **Używaj agregatów/sprawdzeń istnienia po stronie SQL**

- `count`, `sum`, `exists`, `withCount` zamiast ładowania pełnych kolekcji.

4. **Efektywnie przetwarzaj duże zbiory danych**

- Używaj `chunkById`, `lazyById`, `cursor` do iteracji bezpiecznej pamięciowo.

5. **Strategia indeksowania**

- Dodawaj właściwe indeksy DB pod częste filtry/sortowania/joiny.

6. **Cache tam, gdzie ma to sens**

- Cachuj stabilne lub kosztowne wyniki zapytań.

7. **Mierz i profiluj**

- Używaj Telescope/Debugbar/logów zapytań oraz planów `EXPLAIN`.

8. **Dla złożonych raportów używaj query buildera/raw SQL**

- Nie każde ciężkie zapytanie pasuje dobrze do wzorców wysokopoziomowego ORM.

Optymalizuj, zaczynając od pomiaru, a potem naprawiaj hotspoty o największym wpływie.

</details>

<details>
<summary>59. Czym są API Resources w Laravel?</summary>

#### Laravel

API Resources to warstwa transformacji, która konwertuje modele/kolekcje do spójnych struktur odpowiedzi JSON.

1. **Co robią**

- Kontrolują kształt outputu.
- Ukrywają pola wewnętrzne.
- Formatują/składają dane relacji w przewidywalny sposób.

2. **Przykład**

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

3. **Użycie**

```php
return new UserResource($user);
return UserResource::collection($users);
```

4. **Dlaczego ważne**

- Stabilne kontrakty API.
- Separacja między modelem persystencji a formatem transportowym.
- Łatwiejsze wersjonowanie API i kontrola polityki odpowiedzi.

API Resources to natywny, first-class sposób Laravel na standaryzację odpowiedzi JSON API.

</details>

<details>
<summary>60. Jaka jest różnica między API Resources a Transformers?</summary>

#### Laravel

Oba podejścia kształtują dane wyjściowe, ale „API Resources” to wbudowany standard Laravel, a „Transformers” zwykle odnoszą się do zewnętrznych/customowych warstw mapowania.

1. **API Resources (wbudowane)**

- Natywna funkcja Laravel (`JsonResource`).
- Ścisła integracja z frameworkiem i proste użycie.
- Dobry domyślny wybór dla większości API w Laravel.

2. **Transformers (ogólny wzorzec / pakiety)**

- Koncepcja architektoniczna mapowania danych domenowych na DTO odpowiedzi.
- Mogą to być własne klasy albo rozwiązania pakietowe (np. wzorce w stylu Fractal).
- Przydatne, gdy zespół potrzebuje pipeline’ów transformacji niezależnych od frameworka lub mocno customowych.

3. **Różnica praktyczna**

- Resource = oficjalne podejście Laravel.
- Transformer = szerszy wzorzec, który może, ale nie musi używać natywnych prymitywów Laravel.

4. **Co wybrać**

- W aplikacjach Laravel-first domyślnie preferuj API Resources.
- Użyj własnej warstwy transformerów, gdy granice domena/API wymagają większego decouplingu.

Oba podejścia rozwiązują kwestie reprezentacji; wybór zależy od złożoności architektury i potrzeb przenośności.

</details>

<details>
<summary>61. Jak działa uwierzytelnianie w Laravel?</summary>

#### Laravel

Uwierzytelnianie w Laravel weryfikuje tożsamość użytkownika i utrzymuje ją między żądaniami za pomocą guards oraz providers.

1. **Podstawowe klocki**

- **Guards** definiują, jak użytkownicy są uwierzytelniani per żądanie (session, token itd.).
- **Providers** definiują, jak użytkownicy są pobierani (zwykle model Eloquent).

2. **Przepływ sesyjny (web)**

- Użytkownik wysyła dane logowania.
- Laravel waliduje dane względem providera.
- Po sukcesie ID użytkownika jest zapisywane w sesji.
- Kolejne żądania rozwiązują bieżącego użytkownika z sesji/cookie.

3. **Przepływ tokenowy (API)**

- Klient wysyła token (np. bearer token Sanctum/Passport).
- Guard waliduje token i rozwiązuje uwierzytelnionego użytkownika.

4. **Helpery frameworka**

- `Auth::attempt()`, `Auth::user()`, `auth()->check()`.
- Middleware typu `auth` chroni trasy.

5. **Dobra praktyka**

- Używaj wbudowanego auth scaffolding/pakietów dla typowych flow.
- Trzymaj logikę auth scentralizowaną i unikaj własnej obsługi crypto/sesji, chyba że to konieczne.

Uwierzytelnianie w Laravel jest guard-driven i spójne między punktami wejścia web oraz API.

</details>

<details>
<summary>62. Jaka jest różnica między authentication a authorization?</summary>

#### Laravel

Authentication i authorization to powiązane, ale odrębne obszary bezpieczeństwa.

1. **Authentication**

- Odpowiada na pytanie: „Kim jesteś?”.
- Weryfikuje tożsamość (login/session/token).

2. **Authorization**

- Odpowiada na pytanie: „Co możesz zrobić?”.
- Sprawdza uprawnienia/abilities do akcji i zasobów.

3. **Mapowanie w Laravel**

- Authentication: guards, providers, middleware `auth`.
- Authorization: gates, policies, middleware `can`, dyrektywy Blade `@can`.

4. **Przykład**

- Użytkownik jest uwierzytelniony (zalogowany), ale nadal może nie mieć prawa usunąć posta innego użytkownika.

Authentication ustala tożsamość, a authorization egzekwuje reguły kontroli dostępu.

</details>

<details>
<summary>63. Czym są Gates i Policies?</summary>

#### Laravel

Gates i Policies to mechanizmy authorization w Laravel.

1. **Gates**

- Reguły authorization oparte na closure.
- Dobre dla prostych abilities, które nie są ściśle powiązane z modelem.

2. **Policies**

- Authorization oparta na klasach, organizowana per model/zasób.
- Metody takie jak `view`, `create`, `update`, `delete` itd.

3. **Kiedy czego używać**

- Używaj **Gates** do małych/globalnych sprawdzeń.
- Używaj **Policies** do authorization zorientowanego na modele i w większych aplikacjach.

4. **Przykłady użycia**

- `Gate::allows('export-reports')`
- `$this->authorize('update', $post)`

Gates dają lekkie sprawdzenia; Policies dają skalowalną, uporządkowaną autoryzację.

</details>

<details>
<summary>64. Jak działają dyrektywy Blade @can i @cannot?</summary>

#### Laravel

`@can` i `@cannot` to dyrektywy Blade, które warunkowo renderują markup na podstawie sprawdzeń authorization.

1. **`@can`**

- Renderuje treść, jeśli użytkownik ma uprawnienie do danej ability.

```blade
@can('update', $post)
    <a href="{{ route('posts.edit', $post) }}">Edit</a>
@endcan
```

2. **`@cannot`**

- Renderuje treść, jeśli użytkownik nie ma uprawnienia.

```blade
@cannot('delete', $post)
    <span>You cannot delete this post.</span>
@endcannot
```

3. **Jak to jest oceniane**

- Wewnętrznie wywoływana jest logika authorization gate/policy.
- Używany jest kontekst aktualnie uwierzytelnionego użytkownika.

4. **Dlaczego przydatne**

- Utrzymują UI zgodne z backendowymi regułami uprawnień.
- Zapobiegają pokazywaniu akcji, których użytkownik nie może wykonać.

Te dyrektywy upraszczają renderowanie UI świadomego uprawnień w szablonach Blade.

</details>

<details>
<summary>65. Czym jest multi-authentication i jak je zaimplementować?</summary>

#### Laravel

Multi-authentication oznacza wsparcie wielu typów użytkowników/guardów w tej samej aplikacji (np. `web`, `admin`, `api`).

1. **Typowe scenariusze**

- Oddzielne portale admina i klienta.
- Dostęp dla pracowników wewnętrznych i partnerów zewnętrznych.
- Różne strategie auth zależnie od kanału.

2. **Jak zaimplementować**

- Zdefiniuj wiele guardów/providerów w konfiguracji auth.
- Przypisz middleware z konkretnym guardem: `auth:admin`, `auth:web`, `auth:sanctum`.
- Opcjonalnie użyj osobnych flow logowania/kontrolerów/tras dla każdego guarda.

3. **Przykład ochrony tras**

```php
Route::middleware('auth:admin')->group(function () {
    Route::get('/admin/dashboard', AdminDashboardController::class);
});
```

4. **Dobre praktyki**

- Izoluj grupy tras i flow sesji specyficzne dla guarda.
- Utrzymuj jawne reguły authorization dla każdego typu użytkownika.

Multi-auth zapewnia czysty podział tożsamości i uprawnień między domenami aplikacji.

</details>

<details>
<summary>66. Porównaj Laravel Sanctum i Laravel Passport.</summary>

#### Laravel

Sanctum i Passport zapewniają uwierzytelnianie API, ale celują w różny poziom złożoności.

1. **Sanctum**

- Lekki token auth + uwierzytelnianie sesyjne SPA.
- Personal access tokens i proste abilities.
- Łatwy setup, minimalna złożoność OAuth.

2. **Passport**

- Pełna implementacja serwera OAuth2.
- Wspiera authorization code, client credentials, password (legacy usage), refresh tokens, scopes.
- Lepszy dla scenariuszy delegowanej autoryzacji z udziałem third-party.

3. **Trade-off złożoności**

- Sanctum: prostszy i szybszy dla aplikacji first-party.
- Passport: bardziej rozbudowany, ale cięższy w konfiguracji i utrzymaniu.

4. **Typowe dopasowanie**

- Sanctum: SPA/aplikacja mobilna + własny backend.
- Passport: API ekosystemowe/platformowe z zewnętrznymi klientami OAuth.

Wybieraj na podstawie wymagań protokołu auth, a nie tylko popularności pakietu.

</details>

<details>
<summary>67. Kiedy wybrać Sanctum zamiast Passport?</summary>

#### Laravel

Wybierz Sanctum, gdy potrzebujesz prostego uwierzytelniania first-party bez pełnych flow OAuth2.

1. **Dobre przypadki dla Sanctum**

- SPA + backend Laravel z auth sesja/cookie.
- Klienci mobilni lub wewnętrzni używający personal access tokens.
- Małe/średnie API, gdzie delegacja OAuth2 nie jest potrzebna.

2. **Dlaczego Sanctum**

- Szybsza implementacja.
- Niższa złożoność operacyjna.
- Mniej elementów do zarządzania tokenami.

3. **Kiedy to za mało**

- Aplikacje third-party potrzebują delegowanej autoryzacji użytkownika.
- Wymagasz pełnych grant flow OAuth2 i możliwości serwera auth na poziomie standardu.

4. **Reguła decyzyjna**

- Domyślnie wybieraj Sanctum dla aplikacji first-party.
- Przechodź na Passport tylko wtedy, gdy wymagania OAuth2 są jawne.

Sanctum to pragmatyczny domyślny wybór dla większości produktowych API w Laravel.

</details>

<details>
<summary>68. Jak Laravel chroni przed SQL Injection?</summary>

#### Laravel

Laravel ogranicza ryzyko SQL injection dzięki domyślnemu użyciu parameter binding i bezpiecznych abstrakcji zapytań.

1. **Prepared statements/bindingi**

- Query Builder i Eloquent używają parametrów wiązanych zamiast konkatenacji stringów SQL.

2. **Bezpieczne przykłady**

```php
User::where('email', $email)->first();
DB::table('orders')->where('status', $status)->get();
```

3. **Gdzie ryzyko nadal istnieje**

- Niebezpieczna konkatenacja surowego SQL.

```php
// ryzykowne, jeśli $input jest niezaufane
DB::select("SELECT * FROM users WHERE email = '$input'");
```

4. **Bezpieczne użycie raw SQL**

- Używaj placeholderów i bindingów:

```php
DB::select('SELECT * FROM users WHERE email = ?', [$input]);
```

5. **Dobre praktyki**

- Preferuj Eloquent/Query Builder.
- Waliduj input i unikaj ręcznego składania SQL z niezaufanych wartości.

Laravel jest tu domyślnie bezpieczny, ale błędne użycie raw SQL może ponownie wprowadzić ryzyko injection.

</details>

<details>
<summary>69. Jak Laravel chroni przed atakami CSRF?</summary>

#### Laravel

Laravel chroni przed CSRF, wymagając poprawnego tokenu CSRF dla webowych żądań zmieniających stan.

1. **Jak to działa**

- Token per sesja jest generowany i przechowywany po stronie serwera.
- Formularze zawierają token (`@csrf`).
- Middleware weryfikuje token dla przychodzących żądań POST/PUT/PATCH/DELETE.

2. **Użycie w Blade**

```blade
<form method="POST" action="/profile">
    @csrf
    <!-- pola -->
</form>
```

3. **AJAX/SPA**

- Token można wysyłać w nagłówku (np. `X-CSRF-TOKEN`) dla flow sesyjnych same-site.

4. **Dlaczego to skuteczne**

- Atakujący nie może podrobić poprawnego tokenu powiązanego z sesją z kontekstu innej strony.

5. **Uwaga o zakresie**

- CSRF dotyczy głównie żądań przeglądarkowych opartych o cookie/session auth, a nie typowych bezstanowych API z bearer tokenem.

Middleware CSRF to kluczowa domyślna warstwa bezpieczeństwa webowego w Laravel.

</details>

<details>
<summary>70. Jak Laravel chroni przed atakami XSS?</summary>

#### Laravel

Laravel pomaga zapobiegać XSS głównie przez escapowanie outputu i bezpieczne domyślne ustawienia templatingu.

1. **Domyślne escapowanie w Blade**

- `{{ $value }}` jest automatycznie escapowane do HTML.
- Zapobiega renderowaniu/wykonywaniu niezaufanego HTML/JS.

2. **Uwaga na nieescapowany output**

- `{!! $value !!}` renderuje surowy HTML i powinno być używane wyłącznie dla zaufanej/sanitized treści.

3. **Dodatkowe zabezpieczenia**

- Walidacja i normalizacja inputu ograniczają propagację niebezpiecznych payloadów.
- Nagłówki CSP/security (przez middleware/konfigurację serwera) dodają defense-in-depth.

4. **Aspekty frontend/API**

- Zwracanie JSON jest bezpieczniejsze niż renderowanie surowych snippetów HTML.
- Renderowanie po stronie klienta też musi escapować niezaufaną treść.

5. **Dobra praktyka**

- Escapuj domyślnie, sanitizuj gdy HTML jest potrzebny i minimalizuj ścieżki renderowania raw.

Laravel ma mocne domyślne zabezpieczenia, ale bezpieczna obsługa outputu w kodzie aplikacji nadal jest kluczowa.

</details>

<details>
<summary>71. Jak działa szyfrowanie w Laravel?</summary>

#### Laravel

Laravel zapewnia szyfrowanie symetryczne przez facade `Crypt`, używając klucza aplikacji.

1. **Jak to działa**

- Używa klucza aplikacji z environment/config.
- Szyfruje dane i dodaje ochronę integralności, aby wykrywać manipulację.
- Odszyfrowanie jest możliwe tylko tym samym kluczem.

2. **Typowe użycie**

```php
$encrypted = Crypt::encryptString('secret-value');
$plain = Crypt::decryptString($encrypted);
```

3. **Gdzie jest używane**

- Wrażliwe wartości przechowywane w DB/skonfigurowanych payloadach.
- Wewnętrzne mechanizmy frameworka, np. zaszyfrowane cookie (gdy włączone).

4. **Dobre praktyki**

- Trzymaj `APP_KEY` w tajemnicy i stabilny w danym środowisku.
- Rotuj klucze ostrożnie, z przygotowaną strategią migracji.
- Nie szyfruj tego, co powinno być hashowane (np. hasła).

Szyfrowanie w Laravel daje łatwą ochronę „secure at rest” dla odwracalnych danych wrażliwych.

</details>

<details>
<summary>72. Jak hashowane są hasła w Laravel?</summary>

#### Laravel

Laravel hashuje hasła jednokierunkowo przez facade `Hash`, a nie przez odwracalne szyfrowanie.

1. **Domyślne podejście**

- Używa nowoczesnych algorytmów hashowania haseł (zwykle `bcrypt` lub `argon2id` zależnie od konfiguracji).
- Przechowuje tylko hash, nigdy jawne hasło.

2. **Tworzenie hasha**

```php
$hash = Hash::make($password);
```

3. **Weryfikacja hasła**

```php
if (Hash::check($plainPassword, $user->password)) {
    // poprawne
}
```

4. **Rehashing**

- `Hash::needsRehash()` pomaga zaktualizować hashe, gdy zmienia się konfiguracja/cost.

5. **Dobre praktyki**

- Nigdy nie zapisuj ani nie loguj surowych haseł.
- Stosuj mocne polityki walidacji i rate-limited próby logowania.

Hashowanie haseł w Laravel jest domyślnie bezpieczne przy poprawnym użyciu wbudowanego API.

</details>

<details>
<summary>73. Jakie best practices bezpieczeństwa powinna stosować każda aplikacja Laravel?</summary>

#### Laravel

Każda aplikacja Laravel powinna łączyć domyślne zabezpieczenia frameworka z rygorystyczną dyscypliną operacyjną.

1. **Auth i kontrola dostępu**

- Wymuszaj uwierzytelnianie na chronionych trasach.
- Używaj gates/policies do sprawdzeń authorization.
- Stosuj projekt uprawnień least-privilege.

2. **Bezpieczeństwo input/output**

- Waliduj wszystkie przychodzące dane żądań.
- Domyślnie escapuj output (Blade `{{ }}`).
- Unikaj konkatenacji raw SQL; używaj bindingów.

3. **Bezpieczeństwo sesji i cookie**

- Włącz `HttpOnly`, `Secure` i poprawne ustawienia `SameSite`.
- Regeneruj sesje przy login/logout.

4. **Sekrety i konfiguracja**

- Chroń `.env`, rotuj sekrety, rozdzielaj środowiska.
- Nigdy nie commituj credentiali do gita.

5. **Transport i nagłówki**

- Wymuszaj HTTPS.
- Dodaj nagłówki bezpieczeństwa (CSP, HSTS, X-Frame-Options itd.).

6. **Higiena zależności i platformy**

- Utrzymuj Laravel/PHP/paczki aktualne.
- Monitoruj podatności i szybko łataj.

7. **Ochrona przed nadużyciami**

- Stosuj rate limiting dla auth i endpointów wrażliwych.
- Loguj i monitoruj podejrzaną aktywność.

8. **Ochrona danych**

- Hashuj hasła, szyfruj wrażliwe dane odwracalne.
- Rób backupy danych i testuj procedury odtwarzania.

Bezpieczeństwo to nie jedna funkcja; to warstwowa, ciągła praktyka obejmująca kod i operacje.

</details>

<details>
<summary>74. Jak działają signed URLs w Laravel?</summary>

#### Laravel

Signed URLs zawierają podpis kryptograficzny, który potwierdza, że URL został wygenerowany przez Twoją aplikację i nie został zmodyfikowany.

1. **Co chronią**

- Integralność ścieżki URL + parametrów query.
- Opcjonalnie czas wygaśnięcia dla linków czasowych.

2. **Generowanie signed URL**

```php
$url = URL::signedRoute('unsubscribe', ['user' => $user->id]);
$temporary = URL::temporarySignedRoute('download', now()->addMinutes(30), ['file' => $fileId]);
```

3. **Walidacja podpisu**

- Użyj middleware `signed` na trasie albo sprawdź helperem requestu.

```php
Route::get('/unsubscribe/{user}', UnsubscribeController::class)
    ->name('unsubscribe')
    ->middleware('signed');
```

4. **Use case’y**

- Linki wypisu z subskrypcji.
- Akcje weryfikacji e-mail.
- Tymczasowe linki pobierania lub wykonywania akcji.

Signed URLs to prosty sposób zabezpieczania publicznych linków bez wymagania pełnej uwierzytelnionej sesji.

</details>

<details>
<summary>75. Czym są encrypted cookies i signed cookies?</summary>

#### Laravel

Encrypted cookies i signed cookies chronią integralność cookie, ale szyfrowanie dodatkowo chroni poufność.

1. **Encrypted cookies**

- Wartość cookie jest zaszyfrowana i uwierzytelniona.
- Klient nie może odczytać ani zmienić oryginalnej wartości.
- Middleware Laravel może automatycznie szyfrować/odszyfrowywać.

2. **Signed cookies (nacisk na integralność)**

- Wartość pozostaje czytelna, ale zawiera/weryfikuje podpis.
- Wykrywa manipulację, ale nie ukrywa treści.

3. **Domyślne zachowanie Laravel**

- Laravel najczęściej używa encrypted cookies dla cookie aplikacyjnych przez swój stos cookie middleware.

4. **Kiedy używać**

- Używaj encrypted cookies dla wartości wrażliwych/stanowych.
- Używaj semantyki signed-only, gdy akceptowalna jest jawność treści, ale wymagana jest detekcja manipulacji.

5. **Uwaga bezpieczeństwa**

- Zawsze ustawiaj atrybuty `Secure`, `HttpOnly` i odpowiedni `SameSite`.

W praktyce encrypted cookies są zwykle bezpieczniejszym domyślnym wyborem dla aplikacji webowych Laravel.

</details>

<details>
<summary>76. Wyjaśnij system kolejek Laravel.</summary>

#### Laravel

System kolejek Laravel przenosi czasochłonne zadania poza cykl żądania HTTP do asynchronicznego przetwarzania w tle.

1. **Dlaczego używa się kolejek**

- Szybsze odpowiedzi dla użytkownika.
- Lepsza skalowalność pod obciążeniem.
- Niezawodne wykonanie dzięki retry i obsłudze błędów.

2. **Jak to działa**

- Aplikacja dispatchuje job do backendu kolejki.
- Proces worker kolejki konsumuje joby i je wykonuje.
- Nieudane joby mogą być ponawiane albo przenoszone do storage błędów.

3. **Typowe zadania kolejkowane**

- E-maile, notyfikacje, generowanie raportów.
- Integracje API i webhooki.
- Przetwarzanie obrazów/wideo oraz ciężkie importy/eksporty.

4. **Kluczowe narzędzia ekosystemu**

- Workery `queue:work`.
- Śledzenie `failed_jobs`.
- Horizon (dla kolejek Redis) do monitoringu i kontroli.

Architektura kolejek jest kluczowa dla responsywnych i odpornych aplikacji Laravel.

</details>

<details>
<summary>77. Czym są joby i queue workery?</summary>

#### Laravel

Joby i workery to podstawowe komponenty producer-consumer asynchronicznego przetwarzania w Laravel.

1. **Joby**

- Enkapsulowane klasy zadań (zwykle w `app/Jobs`).
- Reprezentują jednostkę pracy do wykonania teraz lub później.
- Często implementują `ShouldQueue` dla wykonania asynchronicznego.

2. **Queue workery**

- Długotrwałe procesy wykonujące joby z kolejki.
- Uruchamiane przez Artisan (`php artisan queue:work`).
- Wspierają opcje retry, timeout, sleep, wybór kolejki.

3. **Przepływ**

- Kod dispatchuje job (`dispatch(...)`).
- Payload joba trafia do wybranego backendu kolejki.
- Worker pobiera job i uruchamia `handle()`.

4. **Uwaga operacyjna**

- Na produkcji workery są zwykle zarządzane przez process managera (Supervisor/systemd).

Joby definiują pracę, a workery wykonują ją ciągle w tle.

</details>

<details>
<summary>78. Jakie queue driverry są dostępne w Laravel?</summary>

#### Laravel

Laravel wspiera wiele backendów kolejek przez konfigurowalne driverry.

1. **Najczęściej używane wbudowane driverry**

- `sync`
- `database`
- `redis`
- `sqs` (Amazon SQS)
- `null`

2. **Ogólna charakterystyka**

- `sync`: natychmiastowe wykonanie w bieżącym żądaniu.
- `database`: przechowuje joby w tabelach DB.
- `redis`: szybki backend kolejek in-memory.
- `sqs`: zarządzana chmurowa usługa kolejek.
- `null`: odrzuca joby (przydatne w niektórych scenariuszach local/testing).

3. **Konfiguracja**

- Definiowana w `config/queue.php` oraz zmiennych środowiskowych.

Wybieraj driver na podstawie niezawodności, przepustowości, infrastruktury i potrzeb operacyjnych.

</details>

<details>
<summary>79. Jaka jest różnica między driverami kolejek sync, database, Redis i SQS?</summary>

#### Laravel

Te driverry różnią się modelem wykonania, wydajnością, charakterystyką niezawodności i operacjami.

1. **`sync`**

- Wykonuje job natychmiast podczas żądania.
- Nie wymaga workera w tle.
- Dobre do local dev/prostych flow, ale nie do ciężkich asynchronicznych workloadów produkcyjnych.

2. **`database`**

- Persistuje joby w relacyjnej tabeli DB.
- Łatwy setup, trwały, ale wolniejszy przy wysokiej przepustowości kolejki.

3. **`redis`**

- In-memory backend kolejek o wysokiej wydajności.
- Świetny dla workloadów o wysokiej przepustowości i niskiej latencji.
- Często łączony z Horizon do monitoringu.

4. **`sqs`**

- W pełni zarządzana usługa kolejek AWS.
- Bardzo skalowalna i trwała.
- Dobra dla architektur rozproszonych/cloud-native; dochodzi kwestia latencji/kosztów chmurowych.

5. **Praktyczny wybór**

- Małe/proste: `database`.
- Stos o wysokiej przepustowości z Redis: `redis`.
- Systemy rozproszone AWS-native: `sqs`.
- Local lub wymuszone wykonanie inline: `sync`.

Wybór drivera powinien odpowiadać profilowi ruchu i strategii infrastrukturalnej.

</details>

<details>
<summary>80. Jak obsługiwać failed jobs?</summary>

#### Laravel

Laravel zapewnia wbudowane mechanizmy do rejestrowania, przeglądania, ponawiania i czyszczenia nieudanych jobów kolejkowanych.

1. **Rejestrowanie błędów**

- Skonfiguruj storage failed jobów (najczęściej tabela `failed_jobs`).
- Wyjątki podczas wykonania joba oznaczają job jako failed po przekroczeniu limitu retry.

2. **Zachowanie retry**

- Kontroluj ponawianie przez właściwości/opcje joba (`tries`, strategie backoff).

3. **Przydatne komendy**

```bash
php artisan queue:failed
php artisan queue:retry all
php artisan queue:forget <id>
php artisan queue:flush
```

4. **Obsługa na poziomie joba**

- Zaimplementuj metodę `failed(Throwable $e)` dla cleanupu/alertów/logiki kompensacji.

5. **Dobre praktyki**

- Twórz joby idempotentne.
- Dodaj ustrukturyzowane logowanie i alertowanie.
- Rozdziel obsługę błędów przejściowych i trwałych.

Solidna obsługa failed jobów jest krytyczna dla niezawodnych systemów asynchronicznych.

</details>

<details>
<summary>81. Czym jest job batching?</summary>

#### Laravel

Job batching grupuje wiele jobów w jedną śledzoną paczkę ze współdzielonymi callbackami cyklu życia i monitoringiem postępu.

1. **Co daje batching**

- Dispatch wielu jobów jako jednej logicznej jednostki.
- Śledzenie postępu, zakończenia i błędów.
- Wykonywanie callbacków dla `then`, `catch`, `finally`.

2. **Koncepcja przykładu**

- Import pliku podzielony na wiele jobów przetwarzających chunki w jednej paczce.

3. **Typowe use case’y**

- Importy/eksporty danych.
- Duże operacje reindeksacji.
- Workloady fan-out, gdzie liczy się globalne zakończenie.

4. **Korzyści operacyjne**

- Lepsza observability i orkiestracja dla workflow wielojobowych.
- Łatwiejsze anulowanie/monitoring z poziomu UI/narzędzi administracyjnych.

Batching jest przydatny, gdy wiele równoległych jobów należy do jednego procesu biznesowego.

</details>

<details>
<summary>82. Czym są queued listeners?</summary>

#### Laravel

Queued listeners to listenery eventów uruchamiane asynchronicznie przez system kolejek zamiast inline podczas dispatchu eventu.

1. **Czym różnią się od zwykłych listenerów**

- Zwykły listener wykonuje się od razu.
- Queued listener trafia do kolejki i jest przetwarzany przez workera.

2. **Jak włączyć**

- Listener implementuje `ShouldQueue`.

3. **Dlaczego ich używać**

- Utrzymują szybki dispatch eventu i cykl żądania.
- Przenoszą ciężkie side effecty (e-maile, zewnętrzne wywołania API, zapisy analityczne).

4. **Dobre praktyki**

- Upewnij się, że logika listenera jest idempotentna.
- Odpowiednio konfiguruj retry/timeouty.
- Obsługuj awarie zależności zewnętrznych w sposób graceful.

Queued listeners są kluczowe dla skalowalnego przetwarzania eventów bez blokowania żądań użytkownika.

</details>

<details>
<summary>83. Czym są eventy i listenery w Laravel?</summary>

#### Laravel

Eventy i listenery realizują komunikację w stylu publish-subscribe wewnątrz aplikacji Laravel.

1. **Event**

- Reprezentuje coś, co wydarzyło się w domenie/aplikacji.
- Przykład: `OrderPaid`, `UserRegistered`, `InvoiceOverdue`.

2. **Listener**

- Klasa reagująca na event i wykonująca side effect.
- Przykład: wysłanie e-maila, aktualizacja CRM, enqueue kolejnego joba.

3. **Dlaczego ten wzorzec jest przydatny**

- Oddziela główny workflow od side effectów.
- Poprawia modularność i utrzymywalność.
- Umożliwia wiele reakcji na jeden event bez zmiany producenta eventu.

4. **Dispatch i obsługa**

- Dispatchuj event z serwisu/kontrolera.
- Framework routuje event do zarejestrowanych listenerów.

Eventy modelują fakty, a listenery implementują reakcje.

</details>

<details>
<summary>84. Jak generować eventy i listenery?</summary>

#### Laravel

Laravel dostarcza generatory Artisan i wzorce automatycznej rejestracji dla eventów i listenerów.

1. **Wygeneruj event**

```bash
php artisan make:event OrderPaid
```

2. **Wygeneruj listener**

```bash
php artisan make:listener SendOrderReceipt --event=OrderPaid
```

3. **Zarejestruj mapowanie**

- Zmapuj event na listener w event service providerze albo użyj konfiguracji framework discovery.

4. **Dispatchuj event**

```php
event(new OrderPaid($order));
```

5. **Skolejkuj listener, jeśli trzeba**

- Zaimplementuj `ShouldQueue` w listenerze dla obsługi asynchronicznej.

Generowanie + czytelna rejestracja utrzymują workflow eventów jawny i utrzymywalny.

</details>

<details>
<summary>85. Czym jest event-driven architecture w Laravel?</summary>

#### Laravel

Event-driven architecture (EDA) w Laravel organizuje zachowanie aplikacji wokół eventów domenowych/aplikacyjnych i reakcji asynchronicznych.

1. **Główna zasada**

- Emituj eventy, gdy występują ważne fakty.
- Niezależne listenery obsługują działania downstream.

2. **Korzyści**

- Luźne sprzężenie między modułami.
- Łatwiejsze rozszerzanie funkcji bez modyfikowania głównego flow.
- Lepsza skalowalność, gdy listenery są kolejkowane.

3. **Typowy wzorzec**

- Kończy się akcja transakcyjna.
- Event jest dispatchowany (`OrderPaid`).
- Uruchamia się wiele listenerów (e-mail, analityka, synchronizacja fulfillmentu).

4. **Wskazówki projektowe**

- Utrzymuj nazwy eventów znaczące biznesowo.
- Unikaj umieszczania ciężkiej logiki biznesowej bezpośrednio w listenerach, chyba że to celowe.
- Zapewnij idempotencję i observability dla listenerów asynchronicznych.

EDA w Laravel pomaga budować modularne i skalowalne systemy, które czysto ewoluują w czasie.

</details>

<details>
<summary>86. Czym jest Laravel Broadcasting?</summary>

#### Laravel

Laravel Broadcasting to warstwa dostarczania eventów realtime, służąca do wypychania eventów z serwera do klientów frontendowych przez WebSockety (lub kompatybilne driverry).

1. **Co robi**

- Broadcastuje wybrane eventy Laravel do kanałów.
- Pozwala klientom subskrybować i reagować natychmiast.

2. **Typowe use case’y**

- Powiadomienia na żywo.
- Chat i wskaźniki obecności.
- Dashboardy realtime i aktualizacje statusu.

3. **Kluczowe pojęcia**

- Kanały: `public`, `private`, `presence`.
- Authorization dla kanałów private/presence.
- Klasy eventów implementujące zachowanie broadcastingu.

4. **Przegląd stosu**

- Backend emituje event broadcastowany.
- Broadcast driver wysyła go przez infrastrukturę websocket.
- Frontend (zwykle Laravel Echo) nasłuchuje i aktualizuje UI.

Broadcasting umożliwia responsywne UX oparte o eventy bez architektury opartej na ciężkim pollingu.

</details>

<details>
<summary>87. Jak działa Laravel Echo?</summary>

#### Laravel

Laravel Echo to biblioteka klienta JavaScript, która subskrybuje kanały broadcastingu i nasłuchuje eventów Laravel w przeglądarce.

1. **Rola w stosie realtime**

- Dostarcza wygodne frontendowe API nad transportem websocket.
- Integruje się z konwencjami nazw kanałów i eventów Laravel.

2. **Jak działa**

- Aplikacja inicjalizuje Echo konfiguracją broadcastera.
- Klient dołącza do kanałów (`channel`, `private`, `presence`).
- Nasłuchuje eventów broadcastowanych z serwera i uruchamia callbacki.

3. **Koncepcja przykładu**

```js
Echo.private(`orders.${orderId}`)
  .listen('OrderShipped', (payload) => {
    // aktualizacja UI
  });
```

4. **Dlaczego zespoły go używają**

- Czyste API do subskrypcji realtime.
- Mniej boilerplate’u wokół obsługi eventów websocket.
- Dobra współpraca z flow broadcasting/auth w Laravel.

Echo to standardowy frontendowy most dla funkcji realtime w Laravel.

</details>

<details>
<summary>88. Czym jest Laravel Reverb i dlaczego jest ważny we współczesnym Laravel?</summary>

#### Laravel

Laravel Reverb to first-party serwer WebSocket dla broadcastingu realtime.

1. **Co zapewnia Reverb**

- Natywną infrastrukturę websocket zarządzaną przez Laravel.
- Ścisłą integrację z broadcastingiem Laravel, channel auth i Echo.

2. **Dlaczego jest ważny**

- Ogranicza zależność od third-party providerów realtime w wielu use case’ach.
- Poprawia local development i spójność operacyjną w stosach Laravel-first.
- Daje zespołom bezpośrednią kontrolę nad skalowaniem, deploymentem i observability.

3. **Gdzie pasuje**

- Powiadomienia realtime.
- Funkcje live collaboration.
- Dashboardy operacyjne i strumienie eventów.

4. **Wpływ praktyczny**

- Nowoczesne aplikacje Laravel mogą utrzymywać więcej architektury realtime wewnątrz ekosystemu Laravel, z mniejszą liczbą granic integracyjnych.

Reverb to kluczowy element nowoczesnej „historii realtime” w Laravel.

</details>

<details>
<summary>89. Czym jest Laravel Horizon?</summary>

#### Laravel

Laravel Horizon to dashboard do monitoringu i zarządzania kolejkami opartymi o Redis.

1. **Co robi**

- Wizualizuje przepustowość kolejek, czasy wykonania, błędy i czasy oczekiwania.
- Udostępnia zarządzanie konfiguracją workerów/supervisorów.
- Pomaga stroić wydajność i niezawodność kolejek.

2. **Kluczowe funkcje**

- Metryki i trendy jobów.
- Inspekcja failed jobów.
- Strategie balansowania kolejek.
- Definicje supervisorów per środowisko.

3. **Dlaczego to ważne**

- Lepsza widoczność operacyjna.
- Szybsza reakcja na incydenty w workloadach asynchronicznych.
- Bezpieczniejsze skalowanie przetwarzania w tle.

Horizon to podstawowa warstwa operacyjna produkcji dla workloadów kolejkowych Redis w Laravel.

</details>

<details>
<summary>90. Czym jest task scheduling w Laravel?</summary>

#### Laravel

Task scheduling w Laravel to warstwa orkiestracji crona definiowana w kodzie dla cyklicznych komend/jobów.

1. **Główna idea**

- Definiujesz harmonogram w kodzie aplikacji.
- Systemowy cron uruchamia scheduler Laravel co minutę.

2. **Typowe użycie**

- Okresowe synchronizacje danych.
- Joby cleanup.
- Generowanie raportów.
- Notyfikacyjne digesty.

3. **Korzyści**

- Scentralizowane, wersjonowane definicje harmonogramów.
- Czyściej niż zarządzanie wieloma osobnymi wpisami crona na serwerze.
- Wsparcie dla zapobiegania nakładaniu, ograniczeń środowiskowych i kontroli częstotliwości.

4. **Przepływ operacyjny**

- Ustawiasz jeden wpis crona dla `schedule:run`.
- Laravel decyduje, które zaplanowane taski mają wykonać się teraz.

Task scheduling daje przewidywalną i utrzymywalną automatyzację cykliczną w aplikacjach Laravel.

</details>

<details>
<summary>91. Jak działa współbieżność w kolejkach?</summary>

#### Laravel

Współbieżność kolejek osiąga się przez uruchamianie wielu workerów (i/lub wielu kolejek) równolegle, co pozwala przetwarzać wiele jobów jednocześnie.

1. **Model współbieżności**

- Każdy worker przetwarza joby niezależnie.
- Więcej workerów = większa równoległa przepustowość (w granicach infrastruktury).

2. **Dźwignie kontroli**

- Liczba procesów workerów.
- Separacja priorytetów kolejek (`high`, `default`, `low`).
- Ustawienia timeout, retry i memory workerów.
- Strategie balansowania Horizon (dla Redis).

3. **Wymagania bezpieczeństwa**

- Joby powinny być idempotentne.
- Współdzielone zasoby mogą wymagać locków/operacji atomowych.
- Obsługuj race conditions przy zmianach stanu.

4. **Wzorzec skalowania**

- Skaluj workery horyzontalnie pod obciążeniem.
- Monitoruj queue lag i metryki błędów, aby stroić współbieżność.

Współbieżność zwiększa przepustowość, ale poprawność zależy od projektu jobów i mechanizmów spójności danych.

</details>

<details>
<summary>92. Czym jest idempotencja w jobach kolejkowanych?</summary>

#### Laravel

Idempotencja oznacza, że wielokrotne uruchomienie tego samego joba daje ten sam końcowy efekt co uruchomienie jednokrotne.

1. **Dlaczego to ważne w kolejkach**

- Joby mogą być ponawiane po błędach/timeoutach.
- Mogą wystąpić duplikaty dispatchu.
- Workery mogą się wykrzaczyć po częściowym postępie.

2. **Jak to zaimplementować**

- Używaj unikalnych kluczy biznesowych/idempotency keys.
- Sprawdzaj bieżący stan przed wykonaniem side effectów.
- Używaj constraints DB lub operacji atomowych.
- Wykonuj wywołania zewnętrzne z idempotencją po stronie providera, gdy to dostępne.

3. **Przykłady**

- „Wyślij e-mail z fakturą tylko raz na ID faktury.”
- „Pobierz płatność tylko jeśli status nadal jest pending.”

4. **Dobra praktyka**

- Projektuj idempotencję na poziomie use case’u, a nie jako późniejszy dodatek.

Idempotentne joby są kluczowe dla niezawodnych, bezpiecznych względem retry systemów asynchronicznych.

</details>

<details>
<summary>93. Jak działa cache w Laravel?</summary>

#### Laravel

Cache w Laravel przechowuje wyliczone dane w szybkim storage, aby ograniczyć powtarzanie kosztownych operacji.

1. **Główna idea**

- Najpierw odczyt z cache.
- Jeśli brak, wyliczenie danych i zapis z TTL.

2. **Główne API**

- `Cache::get()`, `put()`, `remember()`, `rememberForever()`, `forget()`.

3. **Typowy wzorzec**

```php
$users = Cache::remember('users.active', 300, function () {
    return User::where('is_active', true)->get();
});
```

4. **Gdzie jest używany**

- Cache wyników zapytań.
- Odczyty konfiguracji/metadanych.
- Storage powiązany z rate limitingiem i sesjami (zależnie od drivera).

5. **Cel**

- Mniejsze obciążenie DB, niższa latencja, lepsza przepustowość.

Cache to jedna z głównych dźwigni wydajności w produkcyjnych systemach Laravel.

</details>

<details>
<summary>94. Jakie cache driverry są dostępne?</summary>

#### Laravel

Laravel wspiera wiele backendów cache przez konfigurowalne driverry.

1. **Najczęściej używane driverry**

- `array` (tylko runtime, bez persystencji)
- `file`
- `database`
- `redis`
- `memcached`
- `dynamodb` (gdy skonfigurowany)
- `null`

2. **Charakterystyka driverów**

- `array`: przydatny do testów/lokalnego runtime.
- `file`/`database`: prosty setup, niższa wydajność.
- `redis`/`memcached`: wysoka wydajność cache produkcyjnego.
- `null`: wyłącza zachowanie cache.

3. **Reguła wyboru**

- Dla produkcji high-load zwykle preferowane są Redis albo Memcached.

Wybór drivera zależy od infrastruktury, wymagań latencji i preferencji operacyjnych.

</details>

<details>
<summary>95. Jakie strategie cache zastosować w aplikacji Laravel pod wysokim obciążeniem?</summary>

#### Laravel

Strategia cache dla high-load powinna łączyć warstwę danych, warstwę aplikacji i dyscyplinę invalidacji.

1. **Cache-aside (`remember`)**

- Wzorzec read-through dla kosztownych zapytań/obliczeń.
- Ustawiaj sensowne TTL zależnie od zmienności danych.

2. **Podejście wielopoziomowe**

- Gorące dane key/value w Redis.
- Cache HTTP/CDN dla odpowiedzi publicznych, gdy to możliwe.

3. **Zapobieganie stampede**

- Używaj locków (`Cache::lock`) wokół regeneracji krytycznych hot keys.
- Staggeruj TTL albo stosuj jitter.

4. **Invalidacja oparta na tagach (jeśli wspierana)**

- Grupuj powiązane klucze cache per domena i flushuj celowane zestawy.

5. **Optymalizacja payloadów**

- Cachuj zwarte projekcje DTO/array, a nie przerośnięte grafy obiektów.

6. **Ciągły pomiar**

- Śledź hit rate, latencję p95, churn kluczy i użycie pamięci.

7. **Fallback i odporność**

- Projektuj graceful zachowanie na cache miss/outage.

W systemach high-load strategia invalidacji i observability są tak samo ważne jak surowa szybkość cache.

</details>

<details>
<summary>96. Czym są cache tags?</summary>

#### Laravel

Cache tags pozwalają logicznie grupować wpisy cache i unieważniać je razem.

1. **Jaki problem rozwiązują**

- Łatwiejsza, precyzyjna invalidacja powiązanych kluczy.
- Unikanie pełnego flushu cache przy lokalnych zmianach danych.

2. **Koncepcja przykładu**

```php
Cache::tags(['users', 'team:42'])->put('users.team.42.list', $data, 600);
Cache::tags(['users', 'team:42'])->flush();
```

3. **Typowe use case’y**

- Unieważnienie całego cache dla tenanta/projektu/kategorii.
- Grupowanie fragmentów dashboardu/API wg kontekstu domenowego.

4. **Ważna uwaga**

- Cache tags są wspierane tylko przez wybrane driverry (najczęściej Redis/Memcached), nie przez wszystkie.

Cache tags są wartościowe, gdy invalidacja cache wymaga precyzji i grupowania domenowego.

</details>

<details>
<summary>97. Jak czyścić i rozgrzewać cache?</summary>

#### Laravel

Czyszczenie usuwa nieaktualne wpisy; rozgrzewanie pre-populuje gorące wpisy, aby uniknąć latencji cold-start.

1. **Komendy czyszczenia cache**

```bash
php artisan cache:clear
php artisan config:clear
php artisan route:clear
php artisan view:clear
php artisan event:clear
```

2. **Budowanie/optymalizacja cache**

```bash
php artisan config:cache
php artisan route:cache
php artisan view:cache
php artisan event:cache
```

3. **Strategia warm-up**

- Po deployu proaktywnie wyliczaj i zapisuj znane hot keys.
- Uruchamiaj joby/komendy warm-up dla krytycznych endpointów i dashboardów.

4. **Praktyka operacyjna**

- Preferuj selektywną invalidację zamiast globalnego flushu.
- Uruchamiaj kroki budowy cache w pipeline deploymentowym.

Dobry flow clear/warm-up cache ogranicza skoki latencji po deployu i regresje widoczne dla użytkownika.

</details>

<details>
<summary>98. Czym jest Laravel Octane?</summary>

#### Laravel

Laravel Octane uruchamia Laravel na długowiecznych workerach aplikacyjnych (Swoole lub RoadRunner), zamiast bootstrapować framework przy każdym żądaniu.

1. **Co zmienia**

- Utrzymuje aplikację w pamięci między żądaniami.
- Wykorzystuje ponownie procesy workerów dla wielu żądań.

2. **Główny efekt**

- Niższy narzut na żądanie i wyższa przepustowość.
- Lepsza latencja dla odpowiednich workloadów.

3. **Opcje runtime**

- Runtime oparty o Swoole.
- Runtime oparty o RoadRunner.

4. **Najlepsze dopasowanie**

- API/aplikacje webowe z dużym ruchem, gdzie narzut bootstrapu na żądanie jest istotny.

Octane to warstwa runtime zorientowana na wydajność dla nowoczesnych deploymentów Laravel.

</details>

<details>
<summary>99. Jak Laravel Octane poprawia wydajność?</summary>

#### Laravel

Octane poprawia wydajność przez redukcję bootstrapu frameworka per żądanie i wykorzystanie długowiecznych procesów workerów.

1. **Brak pełnego bootu aplikacji przy każdym żądaniu**

- Container/config/routes Laravel pozostają w pamięci per worker.

2. **Wyższa przepustowość**

- Workery przetwarzają wiele żądań bez powtarzalnych kosztów inicjalizacji.

3. **Niższa latencja**

- Szybsze czasy odpowiedzi dla wielu typów żądań, szczególnie przy stałym obciążeniu.

4. **Możliwości runtime**

- Używa wydajnych modeli event-loop/process ze Swoole/RoadRunner.

5. **Ważne zastrzeżenie**

- Zyski wydajności wymagają kodu bezpiecznego dla Octane (unikaj stale mutowalnego stanu między żądaniami).

Wydajność Octane wynika z persystencji i efektywności runtime, a nie z automatycznej optymalizacji kodu.

</details>

<details>
<summary>100. Czym są Swoole i RoadRunner?</summary>

#### Laravel

Swoole i RoadRunner to wysokowydajne serwery aplikacyjne używane jako runtime’y Octane.

1. **Swoole**

- Rozszerzenie/runtime PHP zapewniające async I/O, coroutines i wysokowydajne prymitywy sieciowe.
- Bardzo szybkie, ale wymaga środowiska opartego o rozszerzenia.

2. **RoadRunner**

- Serwer aplikacyjny oparty o Go, uruchamiający persistent PHP workery.
- Nie wymaga rozszerzenia Swoole; ma inny model operacyjny.

3. **Wspólna rola w Laravel**

- Utrzymują workery aplikacji Laravel żywe między żądaniami.
- Poprawiają przepustowość i obniżają latencję względem klasycznego bootstrapu per żądanie w PHP-FPM.

4. **Wybór między nimi**

- Zależy od doświadczenia zespołu ops, ograniczeń hostingu, polityki rozszerzeń i dopasowania do ekosystemu.

Oba runtime’y umożliwiają architekturę długowiecznych workerów w Octane.

</details>

<details>
<summary>101. Jakie problemy mogą wystąpić przy persystencji stanu w Octane?</summary>

#### Laravel

Ponieważ workery Octane są długowieczne, mutowalny stan może „przeciekać” między żądaniami, jeśli kod nie jest zaprojektowany pod persystencję.

1. **Typowe ryzyka**

- Przestarzały stan singletonów.
- Przypadkowe cache’owanie w pamięci danych specyficznych dla żądania/użytkownika.
- Statyczne properties zachowujące kontekst poprzedniego żądania.
- Wzrost pamięci przez niezwolnione referencje.

2. **Typowe symptomy**

- Zanieczyszczenie danych między żądaniami.
- Niespójne zachowanie trudne do odtworzenia.
- Stopniowe puchnięcie pamięci i niestabilność workerów.

3. **Jak zapobiegać**

- Utrzymuj serwisy możliwie stateless.
- Unikaj przechowywania danych specyficznych dla żądania w singletonach/statykach.
- Poprawnie resetuj/flushuj stan per żądanie.
- Testuj konkretnie pod zachowaniem runtime Octane.

4. **Mitigacja operacyjna**

- Monitoruj pamięć workerów.
- Stosuj okresowe polityki przeładowania workerów.

Octane wymaga bardziej rygorystycznej dyscypliny stanu niż tradycyjne aplikacje PHP-FPM z izolacją per żądanie.

</details>

<details>
<summary>102. Jak optymalizować aplikację Laravel pod produkcję?</summary>

#### Laravel

Optymalizacja produkcyjna to połączenie optymalizacji build-time, tuningu runtime i observability.

1. **Buduj i cachuj metadane frameworka**

- Używaj `config:cache`, `route:cache`, `view:cache`, `event:cache` tam, gdzie ma to sens.

2. **Używaj OPcache i właściwych ustawień PHP**

- Włącz i dostrój OPcache pod workload produkcyjny.

3. **Architektura kolejek i async**

- Przenieś ciężkie operacje do kolejek.
- Dostrój współbieżność workerów/timeouty/retry.

4. **Wydajność bazy danych**

- Eliminuj zapytania N+1.
- Dodawaj właściwe indeksy i używaj `EXPLAIN`.
- Optymalizuj hot queries i rozmiar payloadów.

5. **Strategia cache**

- Używaj Redis/Memcached dla cache aplikacyjnego.
- Definiuj reguły invalidacji i warm-up hot keys.

6. **Optymalizacja HTTP/perimetru**

- Używaj CDN/reverse proxy, gdzie to odpowiednie.
- Włącz kompresję i bezpieczne nagłówki.

7. **Monitoring i niezawodność**

- Scentralizowane logi, metryki, tracing.
- Alertuj na latencję, error rate, queue lag i failed jobs.

8. **Higiena deploymentu**

- Workflow zero-downtime deployment.
- Bezpieczne uruchamianie migracji.
- Aktualizowanie zależności i łatanie frameworka.

Wydajność produkcyjna to proces ciągły: mierz, dostrajaj, weryfikuj, powtarzaj.

</details>

<details>
<summary>103. Jak optymalizować autoloading Composer?</summary>

#### Laravel

Optymalizacja autoloadingu Composer redukuje narzut ładowania klas, szczególnie na produkcji.

1. **Generowanie zoptymalizowanej class mapy**

```bash
composer install --no-dev --optimize-autoloader
```

lub

```bash
composer dump-autoload -o
```

2. **Użycie authoritative class mapy (opcjonalnie, stricte)**

```bash
composer dump-autoload -a
```

- Zapobiega fallbackowym lookupom plików PSR, poprawiając szybkość ładowania.
- Używaj, gdy class discovery jest stabilne i klasy generowane są poprawnie obsługiwane.

3. **Wykluczanie zależności dev na produkcji**

- Redukuje drzewo autoloadingu i narzut startowy.

4. **Praktyka deploymentowa**

- Odbudowuj zoptymalizowany autoload w pipeline build/deploy.
- Łącz z OPcache i cache’ami frameworka dla najlepszego efektu.

Tuning autoloadingu Composer to niskonakładowa optymalizacja o dużym wpływie na produkcji.

</details>

<details>
<summary>104. Czym jest OPcache i dlaczego jest ważny?</summary>

#### Laravel

OPcache to rozszerzenie PHP, które cache’uje skompilowany bytecode skryptów we współdzielonej pamięci.

1. **Jaki problem rozwiązuje**

- Unika ponownej kompilacji plików PHP przy każdym żądaniu.

2. **Dlaczego to ważne**

- Niższe zużycie CPU.
- Szybsza obsługa żądań.
- Lepsza przepustowość i niższa latencja.

3. **Znaczenie produkcyjne**

- Niezbędny dla każdego poważnego deploymentu PHP/Laravel.
- Działa szczególnie dobrze ze stabilnymi artefaktami deploymentu i zoptymalizowanym autoloadingiem.

4. **Uwaga operacyjna**

- Dostrajasz ustawienia pamięci i walidacji do modelu deploymentu.
- Zapewnij strategię resetu/restartu cache podczas deployów.

OPcache to jedna z najważniejszych bazowych funkcji wydajnościowych w produkcyjnym PHP.

</details>

<details>
<summary>105. Czym jest kompilator JIT w PHP 8+?</summary>

#### Laravel

Kompilator JIT (Just-In-Time) w PHP 8+ może kompilować wybrane opcode’y do natywnego kodu maszynowego w runtime.

1. **Czym różni się od OPcache**

- OPcache cache’uje bytecode.
- JIT może dodatkowo kompilować „gorące” ścieżki wykonania do kodu maszynowego.

2. **Główny cel**

- Workloady CPU-intensive z ciężkimi obliczeniami.
- Nie przede wszystkim logika web requestów I/O-bound.

3. **Gdzie się konfiguruje**

- Ustawienia PHP INI (`opcache.jit`, rozmiar bufora, tryb).

4. **Praktyczne oczekiwania**

- Korzyści zależą od workloadu; brak gwarancji uniwersalnego przyspieszenia dla typowych aplikacji web.

JIT to funkcja optymalizacji runtime, którą najlepiej oceniać benchmarkami specyficznymi dla danego workloadu.

</details>

<details>
<summary>106. Jakie usprawnienia wydajności daje JIT?</summary>

#### Laravel

JIT poprawia wydajność głównie dla ścieżek kodu obciążonych obliczeniami; zyski dla typowych webowych workloadów Laravel są często umiarkowane.

1. **Gdzie zyski są najbardziej prawdopodobne**

- Pętle numeryczne, przetwarzanie algorytmiczne, transformacje CPU-bound.
- Długotrwałe zadania obliczeniowe w workerach CLI.

2. **Gdzie zyski są ograniczone**

- Żądania I/O-bound (DB, Redis, wywołania HTTP, filesystem), które dominują w wielu aplikacjach Laravel.

3. **Oczekiwany profil wpływu**

- Potencjalnie umiarkowane do wysokich zysków w specyficznych hotspotach CPU-heavy.
- Mały lub pomijalny wpływ w typowych flow CRUD/API.

4. **Dobra praktyka**

- Benchmarkuj na realistycznym ruchu/workloadzie produkcyjnym.
- Najpierw traktuj OPcache, optymalizację zapytań i cache jako priorytetowe źródła zysków.

JIT jest sytuacyjny: mocny dla zadań compute-heavy, drugorzędny dla większości systemów Laravel I/O-bound.

</details>

<details>
<summary>107. Jak działa bundlowanie assetów i integracja Vite w Laravel?</summary>

#### Laravel

Laravel integruje Vite dla nowoczesnego bundlowania frontendu, HMR na dev serverze i produkcyjnych buildów assetów.

1. **Tryb developmentu**

- Vite dev server serwuje assety z hot module replacement.
- Blade używa `@vite(...)`, aby ładować assety z dev servera.

2. **Build produkcyjny**

- `npm run build` (lub odpowiednik) bundle’uje/minifikuje assety do wersjonowanych plików.
- Manifest mapuje wpisy źródłowe na zbudowane pliki.

3. **Punkty integracji Laravel**

- `vite.config.*` definiuje entry points/plugins.
- Dyrektywa Blade `@vite(['resources/css/app.css', 'resources/js/app.js'])` wstrzykuje poprawne tagi.

4. **Korzyści**

- Szybkie DX w lokalnym development.
- Efektywne bundle produkcyjne z fingerprintami cache-busting.

Vite daje Laravel nowoczesny i szybki pipeline frontendowy od developmentu po deployment.

</details>

<details>
<summary>108. Dlaczego Laravel przeszedł z Mix na Vite?</summary>

#### Laravel

Laravel przeszedł z Mix (opartego o Webpack) na Vite, aby uzyskać szybszy feedback w development i prostsze nowoczesne tooling.

1. **Główne powody**

- Znacznie szybszy start dev servera.
- Szybsze hot updates dzięki natywnemu pipeline’owi ESM.
- Lżejsza konfiguracja dla wielu nowoczesnych stacków frontendowych.

2. **Zyski w developer experience**

- Lepsza responsywność w średnich/dużych codebase’ach frontendowych.
- Mniejsza złożoność konfiguracji dla typowych use case’ów.

3. **Zachowanie produkcyjne**

- Wydajny output builda z hashowanymi assetami i integracją manifestu.

4. **Strategiczne dopasowanie**

- Dostosowuje Laravel do współczesnych standardów ekosystemu frontendowego.

Przejście na Vite poprawiło codzienną produktywność i utrzymało nowoczesność toolingu frontendowego Laravel.

</details>

<details>
<summary>109. Jak skalować aplikację Laravel horyzontalnie?</summary>

#### Laravel

Skalowanie horyzontalne oznacza uruchamianie wielu instancji aplikacji za load balancerem i wyniesienie współdzielonego stanu poza węzły aplikacyjne.

1. **Stateless app nodes**

- Utrzymuj serwery aplikacji jako zamienne.
- Przechowuj sesje/cache/kolejki we współdzielonych usługach (Redis/DB/SQS), a nie w lokalnej pamięci/plikach.

2. **Load balancing i autoscaling**

- Rozkładaj ruch na wiele instancji.
- Skaluj na podstawie CPU, latencji, queue lag i metryk przepustowości.

3. **Strategia bazy danych**

- Dostrajać główną DB, a w razie potrzeby dodawać read repliki.
- Optymalizować hot queries/indeksy przed dodawaniem kolejnych węzłów aplikacji.

4. **Skalowanie kolejek i async**

- Skaluj pule workerów niezależnie od węzłów web.
- Rozdzielaj kolejki high/low priority.

5. **Wspólne zagadnienia infrastrukturalne**

- Scentralizowane logi/metryki/traces.
- Wspólny object storage dla uploadów.
- Distributed locks dla krytycznych ścieżek współbieżności.

6. **Dyscyplina deploymentu**

- Deploymenty zero-downtime.
- Backward-compatible migracje podczas rolling updates.

Skalowanie horyzontalne działa skutecznie, gdy stan aplikacji jest zewnętrzny, a observability mocna.

</details>

<details>
<summary>110. Jak optymalizować endpointy mocno obciążające bazę danych?</summary>

#### Laravel

Optymalizacja endpointów DB-heavy powinna koncentrować się na efektywności zapytań, kształcie danych i cache.

1. **Eliminuj nieefektywności zapytań**

- Usuń N+1 przez eager loading.
- Wybieraj tylko wymagane kolumny.
- Używaj `exists`, agregatów i `withCount`, gdzie to możliwe.

2. **Tuning indeksów i planu wykonania**

- Dodawaj/koryguj indeksy dla częstych filtrów/sortowań/joinów.
- Analizuj plany `EXPLAIN` i eliminuj full scan tam, gdzie da się uniknąć.

3. **Redukuj payload i round-tripy**

- Paginuj duże zbiory danych.
- Zwracaj minimalny zestaw pól API resource.
- Unikaj over-fetchingu głębokich drzew relacji.

4. **Strategia cache**

- Cachuj stabilne, kosztowne wyniki.
- Stosuj reguły invalidacji powiązane z zapisami.

5. **Używaj właściwej warstwy dostępu do danych**

- Eloquent dla utrzymywalnych flow domenowych.
- Query builder/raw SQL dla złożonych zapytań analitycznych/hot queries.

6. **Mierz ciągle**

- Śledź liczbę zapytań, latencję p95/p99, CPU DB, lock waits i side effecty kolejek.

Najpierw optymalizuj najgorsze hotspoty; tuning oparty o pomiar daje najwyższy ROI.

</details>

<details>
<summary>111. Jak tworzyć REST API w Laravel?</summary>

#### Laravel

Tworzenie REST API w Laravel oznacza zdefiniowanie tras zorientowanych na zasoby, kontrolerów, walidacji, auth i spójnych odpowiedzi JSON.

1. **Zdefiniuj trasy API**

- Używaj `routes/api.php` oraz `Route::apiResource(...)` tam, gdzie pasuje.

2. **Używaj kontrolerów API**

- Utrzymuj kontrolery cienkie i deleguj logikę biznesową do serwisów/actions.

3. **Waliduj input**

- Używaj Form Requests do walidacji żądań i authorization.

4. **Zwracaj standaryzowany JSON**

- Używaj API Resources do kształtowania odpowiedzi.

5. **Zabezpieczaj endpointy**

- Używaj Sanctum/Passport, middleware, policies i rate limitingu.

6. **Aspekty operacyjne**

- Dodaj paginację, filtrowanie, sortowanie i spójne formaty błędów.

Produkcyjnie gotowe REST API w Laravel to głównie spójność, walidacja i czytelne kontrakty.

</details>

<details>
<summary>112. Jaka jest różnica między REST a GraphQL?</summary>

#### Laravel

REST i GraphQL to różne paradygmaty API dla wymiany danych klient-serwer.

1. **REST**

- Wiele endpointów mapowanych na zasoby (`/users`, `/orders/{id}`).
- Serwer definiuje kształt odpowiedzi per endpoint.
- Silna semantyka HTTP i konwencje cache.

2. **GraphQL**

- Zwykle pojedynczy endpoint z typowanym schematem.
- Klient pyta dokładnie o potrzebne pola.
- Unika under-fetchingu/over-fetchingu przy dobrym projekcie.

3. **Podsumowanie trade-offów**

- REST: prostszy model operacyjny, świetny dla standardowego CRUD/public API.
- GraphQL: elastyczne zapytania i agregacja, ale większa złożoność schematu/resolverów.

4. **Kiedy co wybrać**

- REST dla prostych API zasobowych.
- GraphQL, gdy klienci potrzebują bardzo dynamicznego składania danych.

Żadne z podejść nie jest uniwersalnie lepsze; wybór zależy od wzorców dostępu do danych po stronie klienta i kompetencji zespołu.

</details>

<details>
<summary>113. Jak zaimplementować GraphQL w Laravel?</summary>

#### Laravel

GraphQL w Laravel zwykle implementuje się podejściem opartym o pakiet oraz schemat/resolvery.

1. **Zainstaluj pakiet GraphQL**

- Użyj dojrzałego pakietu Laravel GraphQL kompatybilnego z bieżącą wersją Laravel/PHP.

2. **Zaprojektuj schemat**

- Zdefiniuj typy, queries, mutations i obiekty input.
- Utrzymuj schemat zgodny z granicami domeny.

3. **Zaimplementuj resolvery**

- Mapuj pola/operacje do warstwy service/action.
- Unikaj umieszczania logiki biznesowej bezpośrednio w „glue code” resolverów.

4. **Dodaj auth i policies**

- Chroń wrażliwe pola/mutations guardami i regułami authorization.

5. **Zabezpieczenia wydajnościowe**

- Używaj eager loadingu/batchingu w stylu DataLoader, aby zapobiegać N+1.
- Ograniczaj głębokość/złożoność zapytań.

6. **Praktyki operacyjne**

- Ostrożnie wersjonuj/deprecjonuj pola schematu.
- Dodaj observability dla wolnych zapytań i awarii resolverów.

Sukces GraphQL w Laravel zależy bardziej od dyscypliny schematu i resolverów niż od samego setupu transportu.

</details>

<details>
<summary>114. Czym jest wersjonowanie API i dlaczego jest ważne?</summary>

#### Laravel

Wersjonowanie API to praktyka zarządzania zmianami niekompatybilnymi wstecz przez jawne granice wersji.

1. **Dlaczego to ważne**

- Zapobiega psuciu istniejących klientów.
- Umożliwia stopniową migrację do nowych wersji kontraktu.
- Wspiera długowieczne integracje zewnętrzne.

2. **Typowe podejścia do wersjonowania**

- Wersjonowanie URI (`/api/v1/...`, `/api/v2/...`).
- Wersjonowanie przez header/media-type.

3. **Styl implementacji w Laravel**

- Rozdzielaj route groups/controllers/resources wg wersji.
- Wspólną logikę biznesową trzymaj w services/actions.

4. **Dobre praktyki**

- Minimalizuj breaking changes.
- Wyraźnie oznaczaj deprecations.
- Dostarczaj harmonogramy migracji i okna kompatybilności.

Wersjonowanie to narzędzie zarządzania kontraktem dla stabilnej ewolucji API.

</details>

<details>
<summary>115. Jak API Resources poprawiają odpowiedzi API?</summary>

#### Laravel

API Resources poprawiają odpowiedzi, czyniąc output jawnym, spójnym i odseparowanym od wewnętrznej struktury modelu.

1. **Spójność**

- Standaryzowane nazwy pól i wzorce zagnieżdżeń.

2. **Bezpieczeństwo/kontrola danych**

- Zapobiegają przypadkowemu ujawnieniu atrybutów wewnętrznych.

3. **Warstwa transformacji**

- Przewidywalnie formatuje wartości i pola warunkowe.

4. **Utrzymywalność**

- Scentralizowana logika outputu zamiast ad hoc tablic w kontrolerach.

5. **Wsparcie wersjonowania**

- Łatwiejsza ewolucja kontraktu przez wprowadzenie resource classes specyficznych dla wersji.

Resources to domyślna, czysta warstwa reprezentacji dla JSON API w Laravel.

</details>

<details>
<summary>116. Czym są DTO i czy warto ich używać w Laravel?</summary>

#### Laravel

DTO (Data Transfer Objects) to typowane obiekty używane do przenoszenia zwalidowanych danych między warstwami.

1. **Co dają DTO**

- Jawne kontrakty danych.
- Lepsze type safety i wsparcie IDE/static-analysis.
- Czystsze sygnatury metod service/action.

2. **Kiedy są przydatne w Laravel**

- Nietrywialne flow biznesowe.
- Transformacje wieloetapowe.
- Granice między warstwami (controller -> service -> job).

3. **Kiedy są opcjonalne**

- W bardzo prostych endpointach CRUD często wystarczą zwalidowane tablice.

4. **Pragmatyczna wskazówka**

- Używaj DTO tam, gdzie redukują niejednoznaczność i duplikację.
- Unikaj over-engineeringu DTO w małych modułach.

DTO są wartościowe w średnich/dużych codebase’ach ze złożonymi workflow domenowymi.

</details>

<details>
<summary>117. Jak walidować żądania API w Laravel?</summary>

#### Laravel

Walidacja żądań API w Laravel zwykle opiera się na Form Requests i jasnych regułach walidacji.

1. **Używaj klas Form Request**

- Enkapsuluj `authorize()` i `rules()` per endpoint/use case.

2. **Stosuj ścisłe reguły**

- Waliduj typy, formaty, pola wymagane, unikalność i zagnieżdżone tablice.

3. **Sanityzuj/normalizuj, gdzie potrzebne**

- Przygotuj input przed walidacją dla spójnej dalszej obsługi.

4. **Zwracaj spójne błędy**

- Utrzymuj wystandaryzowany kształt odpowiedzi błędów walidacji dla klientów.

5. **Nie ufaj inputowi klienta**

- Waliduj każdy endpoint zapisujący, nawet dla API wewnętrznych.

Walidacja to kluczowa granica API, która chroni integralność danych i jakość kontraktu.

</details>

<details>
<summary>118. Czym są Form Requests?</summary>

#### Laravel

Form Requests to własne klasy żądań dedykowane logice walidacji i authorization.

1. **Co zawierają**

- `authorize()` do sprawdzeń dostępu.
- `rules()` do reguł walidacji.

2. **Jak są używane**

- Type-hint w akcji kontrolera; Laravel auto-waliduje przed logiką akcji.

```php
public function store(StoreOrderRequest $request): JsonResponse
{
    $data = $request->validated();
    // ...
}
```

3. **Korzyści**

- Czystsze kontrolery.
- Reużywalna/uporządkowana logika walidacji.
- Testowalne reguły na poziomie requestu.

Form Requests to idiomatyczne podejście Laravel do walidacji na granicy żądania.

</details>

<details>
<summary>119. Jak obsługiwać wyjątki w API?</summary>

#### Laravel

Obsługa wyjątków w API powinna zamieniać błędy wewnętrzne na spójne, bezpieczne i czytelne maszynowo odpowiedzi.

1. **Centralizuj obsługę**

- Użyj globalnego exception handlera/logiki renderowania do mapowania wyjątków na odpowiedzi HTTP.

2. **Mapuj znane typy wyjątków**

- Validation -> `422`
- Authentication -> `401`
- Authorization -> `403`
- Not found -> `404`
- Konflikty domenowe/biznesowe -> odpowiednio `409`/`422`

3. **Ukrywaj szczegóły wewnętrzne**

- Nie ujawniaj stack trace’ów/wrażliwych danych na produkcji.

4. **Dodaj observability**

- Loguj wyjątki z kontekstem correlation/request.
- Alertuj przy błędach wysokiej wagi lub powtarzalnych awariach.

5. **Utrzymuj stabilny kontrakt**

- Standaryzuj format payloadu błędu we wszystkich endpointach.

Dobra obsługa wyjątków API równoważy klarowność dla klienta z bezpieczeństwem operacyjnym.

</details>

<details>
<summary>120. Jak standaryzować odpowiedzi błędów API?</summary>

#### Laravel

Standaryzowane błędy API używają jednego, spójnego schematu JSON dla wszystkich typów błędów.

1. **Zdefiniuj jeden kontrakt błędu**

- Pola takie jak `code`, `message`, `errors`, `meta`, `request_id`.

2. **Scentralizuj generowanie**

- Buduj odpowiedzi w exception handlerze albo dedykowanej warstwie odpowiedzi błędów.

3. **Używaj poprawnych statusów HTTP**

- Dopasuj kody statusu do kategorii błędu.

4. **Spójnie obsługuj walidację**

- Zachowuj szczegóły na poziomie pól w przewidywalnej strukturze.

5. **Korzyści**

- Łatwiejsza integracja po stronie klienta.
- Lepsze debugowanie i monitoring.
- Stabilny kontrakt między zespołami/usługami.

Standaryzacja zmniejsza tarcie po stronie konsumentów API i obniża narzut wsparcia.

</details>

<details>
<summary>121. Czym są rate limits w API?</summary>

#### Laravel

Rate limits w API ograniczają liczbę żądań, które klient może wykonać w określonym oknie czasowym.

1. **Cel**

- Zapobieganie nadużyciom i próbom brute-force.
- Ochrona pojemności systemu i zapewnienie fair use.

2. **Typowe wymiary limitów**

- Per IP, per użytkownik, per token, per grupa endpointów.

3. **Zachowanie widoczne dla klienta**

- Nadmiarowy ruch dostaje `429 Too Many Requests`.
- Opcjonalne nagłówki informują o limitach i oknie resetu.

4. **Wskazówki projektowe**

- Różnicuj limity dla klientów publicznych i uwierzytelnionych.
- Stosuj ostrzejsze limity dla endpointów wrażliwych (auth/reset hasła).

Rate limiting to kluczowy mechanizm niezawodności i bezpieczeństwa API.

</details>

<details>
<summary>122. Jak zabezpieczać API w Laravel?</summary>

#### Laravel

Bezpieczeństwo API w Laravel wymaga warstwowej ochrony: tożsamość, autoryzacja, transport, walidacja i operacje.

1. **Uwierzytelnianie**

- Używaj Sanctum/Passport zgodnie z wymaganiami.
- Rotuj/odbieraj tokeny i stosuj zasadę least privilege.

2. **Autoryzacja**

- Egzekwuj policies/gates dla akcji na zasobach.

3. **Bezpieczeństwo wejścia i wyjścia**

- Waliduj wszystkie inputy, unikaj konkatenacji raw SQL, sanitizuj ryzykowne ścieżki treści.

4. **Transport i nagłówki**

- Wymuszaj HTTPS, konfiguruj CORS restrykcyjnie, dodawaj nagłówki bezpieczeństwa.

5. **Ochrona przed nadużyciami**

- Stosuj rate limiting i monitoruj anomalie.

6. **Hardening operacyjny**

- Aktualizuj zależności, centralizuj logi, chroń sekrety, rób regularne security review.

Bezpieczeństwo API to defense-in-depth, a nie pojedynczy przełącznik middleware.

</details>

<details>
<summary>123. Czym jest CORS i jak konfiguruje się go w Laravel?</summary>

#### Laravel

CORS (Cross-Origin Resource Sharing) kontroluje, które originy mogą uzyskać dostęp do API z przeglądarek.

1. **Dlaczego jest potrzebny**

- Przeglądarki domyślnie egzekwują same-origin policy.
- CORS jawnie dopuszcza dozwolone żądania cross-origin.

2. **Konfiguracja w Laravel**

- Ustaw dozwolone originy, metody, nagłówki i credentials w ustawieniach CORS.
- Zastosuj konfigurację do ścieżek API wymagających cross-origin access.

3. **Wskazówki bezpieczeństwa**

- Unikaj zbyt szerokiego `*` na produkcji dla wrażliwych API.
- Ogranicz originy do znanych domen frontendowych.
- Włącz credentials tylko gdy to konieczne i bezpiecznie skonfigurowane.

4. **Uwaga operacyjna**

- Błędna konfiguracja CORS to częsta przyczyna problemów integracyjnych frontendu.

CORS to warstwa polityki dostępu przeglądarki, nie mechanizm uwierzytelniania.

</details>

<details>
<summary>124. Czym są podpisane żądania API?</summary>

#### Laravel

Podpisane żądania API zawierają podpis kryptograficzny potwierdzający integralność żądania i autentyczność źródła.

1. **Co chroni podpis**

- Zapobiega manipulacji parametrami.
- Może zawierać timestamp/nonce, by ograniczyć ryzyko replay.

2. **Typowy model implementacji**

- Klient liczy podpis po kanonicznych danych żądania przy użyciu shared secret/private key.
- Serwer przelicza i porównuje podpis.

3. **Kiedy przydatne**

- Weryfikacja webhooków.
- Integracje server-to-server.
- Krytyczne akcje wymagające dowodu integralności żądania.

4. **Relacja do auth**

- Często uzupełniają token auth, a nie ją zastępują.

Podpisane żądania dają silne gwarancje integralności dla wrażliwych interakcji API.

</details>

<details>
<summary>125. Jak zaimplementować WebSockety w Laravel?</summary>

#### Laravel

WebSockety w Laravel najczęściej wdraża się przez Broadcasting + Reverb (lub kompatybilną infrastrukturę) + klient Echo.

1. **Setup backendu**

- Skonfiguruj driver broadcastingu i serwer WebSocket.
- Zdefiniuj eventy broadcastowalne i autoryzację kanałów.

2. **Setup frontendu**

- Zainicjalizuj Laravel Echo z konektorem websocket.
- Subskrybuj kanały i nasłuchuj eventów.

3. **Bezpieczeństwo kanałów**

- Używaj kanałów private/presence dla strumieni uwierzytelnionych.

4. **Aspekty operacyjne**

- Skaluj instancje serwera websocket.
- Monitoruj liczbę połączeń, tempo wiadomości i zachowanie reconnect.

5. **Use case’y**

- Powiadomienia realtime, chat, współpraca, live dashboardy.

W nowoczesnym Laravel Reverb + Echo to standardowa ścieżка first-party dla funkcji WebSocket.

</details>

<details>
<summary>126. Jakie narzędzia testowe udostępnia Laravel?</summary>

#### Laravel

Laravel dostarcza pełny stack testowy dla testów unit, feature i integracyjnych.

1. **Wsparcie rdzenia**

- Oparte o PHPUnit.
- Silna integracja z Pest (popularna alternatywna składnia).

2. **Narzędzia testów HTTP**

- Symulacja żądań (`get`, `post`, `put` itd.).
- Asercje JSON i weryfikacja struktury odpowiedzi.

3. **Pomocniki testów bazy danych**

- Traity do odświeżania DB/transakcji.
- Factory modeli i pomocniki seedingu.

4. **Fakes i mockowanie**

- `Queue::fake()`, `Event::fake()`, `Notification::fake()`, `Mail::fake()`.
- Mockowanie fasad i zależności.

5. **Dodatkowe możliwości**

- Testowanie komend konsolowych.
- Time travel helpers.
- Wsparcie testów równoległych.

Narzędzia testowe Laravel pozwalają praktycznie testować zachowanie od logiki domenowej po pełne flow HTTP.

</details>

<details>
<summary>127. Jaka jest różnica między testami feature i unit?</summary>

#### Laravel

Testy feature i unit różnią się zakresem oraz głębokością integracji.

1. **Unit tests**

- Testują małą, izolowaną jednostkę (jedną klasę/metodę).
- Minimalny bootstrap frameworka.
- Zależności zwykle są mockowane/fake’owane.

2. **Feature tests**

- Testują zachowanie end-to-end przez granice frameworka.
- Często obejmują routing, middleware, walidację, DB, auth i asercje odpowiedzi.

3. **Kiedy używać**

- Unit: złożona czysta logika domenowa.
- Feature: krytyczne workflow użytkownika/API i pewność integracji.

4. **Strategia zbalansowana**

- Używaj obu: unit do szybkich testów logiki, feature do weryfikacji realnego zachowania.

Feature odpowiadają „czy system działa?”, unit odpowiadają „czy logika komponentu działa?”.

</details>

<details>
<summary>128. Czym jest trait RefreshDatabase?</summary>

#### Laravel

`RefreshDatabase` to trait testowy, który resetuje stan bazy między testami, aby zapewnić izolację.

1. **Co robi**

- Uruchamia migracje i zapewnia czysty stan DB zgodnie ze strategią uruchomienia testów.
- Zapobiega „przeciekaniu” danych między testami.

2. **Dlaczego ważne**

- Deterministyczne testy.
- Mniejsza flaky-ness przez pozostałe rekordy.

3. **Typowe użycie**

```php
use Illuminate\Foundation\Testing\RefreshDatabase;

class UserApiTest extends TestCase
{
    use RefreshDatabase;
}
```

4. **Uwaga praktyczna**

- Setup testowej bazy i szybkość migracji mocno wpływają na całkowity czas testów.

`RefreshDatabase` to standardowa baza dla wiarygodnych testów opartych o DB.

</details>

<details>
<summary>129. Jak factory poprawiają testowanie?</summary>

#### Laravel

Factory poprawiają testy, bo szybko i spójnie generują realistyczne, konfigurowalne dane modeli.

1. **Korzyści**

- Mniej ręcznego boilerplate’u fixture.
- Jasna intencja testu dzięki nazwanym states.
- Łatwe tworzenie grafów relacji.

2. **Przykład**

```php
$user = User::factory()->admin()->create();
$order = Order::factory()->for($user)->create();
```

3. **Dlaczego to podnosi jakość**

- Testy skupiają się na zachowaniu, a nie na „szumie” setupu.
- Scenariusze danych są reużywalne i kompozycyjne.

4. **Aspekt wydajnościowy**

- Szybsze pisanie testów i łatwiejsze utrzymanie w czasie.

Factory to jedno z narzędzi o najwyższej dźwigni w workflow testowym Laravel.

</details>

<details>
<summary>130. Jak testować API w Laravel?</summary>

#### Laravel

Testowanie API w Laravel wykorzystuje helpery testów HTTP do symulacji żądań i asercji statusu, payloadu, auth oraz side effectów.

1. **Wykonuj żądania w testach**

- Używaj metod takich jak `getJson`, `postJson`, `putJson`, `deleteJson`.

2. **Asercje odpowiedzi**

- Kody statusu, struktura/fragmenty JSON, błędy walidacji, metadane paginacji.

3. **Testuj auth/uprawnienia**

- Używaj uwierzytelnionych użytkowników/tokenów testowych.
- Weryfikuj ścieżki forbidden/unauthorized.

4. **Testuj side effecty w DB**

- Asercje, że rekordy zostały utworzone/zaktualizowane/usunięte.

5. **Przykład**

```php
$response = $this->actingAs($user)->postJson('/api/orders', $payload);
$response->assertCreated()->assertJsonStructure(['data' => ['id']]);
```

Kompleksowe testy API powinny obejmować zarówno happy path, jak i scenariusze błędów/autoryzacji.

</details>

<details>
<summary>131. Jak fake’ować kolejki, eventy, notyfikacje i mail w testach?</summary>

#### Laravel

Laravel udostępnia dedykowane fake’i do przechwytywania side effectów i asercji intencji bez wykonywania zachowań zewnętrznych.

1. **Queue fake**

```php
Queue::fake();
Queue::assertPushed(SendInvoiceJob::class);
```

2. **Event fake**

```php
Event::fake();
Event::assertDispatched(OrderPaid::class);
```

3. **Notification fake**

```php
Notification::fake();
Notification::assertSentTo($user, InvoicePaidNotification::class);
```

4. **Mail fake**

```php
Mail::fake();
Mail::assertSent(InvoicePaidMail::class);
```

5. **Dlaczego to ważne**

- Szybkie, deterministyczne testy.
- Weryfikacja orkiestracji bez kosztownych asynchronicznych/sieciowych side effectów.

Fake’i są kluczowe do izolowania zachowania przy zachowaniu wiarygodności testów.

</details>

<details>
<summary>132. Czym jest Pest PHP i dlaczego jest popularny w Laravel?</summary>

#### Laravel

Pest to framework testowy zbudowany na PHPUnit, z czystszą, ekspresyjną składnią i mocną integracją z Laravel.

1. **Co oferuje**

- Zwięzłą składnię testów.
- Bogate API expectation.
- Ekosystem pluginów i mocne domyślne wsparcie Laravel.

2. **Dlaczego zespoły Laravel go lubią**

- Szybsze pisanie testów.
- Czytelniejsze testy z mniejszym boilerplate’em.
- Płynna kompatybilność z istniejącą infrastrukturą PHPUnit.

3. **Przewaga adopcyjna**

- Zachowujesz możliwości PHPUnit, zyskując lepsze DX.

Pest jest popularny, bo poprawia klarowność i szybkość bez potrzeby pełnej zmiany paradygmatu testowania.

</details>

<details>
<summary>133. Czym jest mocking w testach Laravel?</summary>

#### Laravel

Mocking zastępuje prawdziwe zależności kontrolowanymi test double’ami, aby izolować testowaną jednostkę.

1. **Dlaczego mockować**

- Unikasz realnych wywołań DB/sieci/usług zewnętrznych.
- Symulujesz ścieżki błędów i edge case’y.
- Weryfikujesz interakcje z komponentami współpracującymi.

2. **Jak w Laravel**

- Mockuj interfejsy/serwisy rozwiązywane z containera.
- Używaj frameworkowych fake’ów tam, gdzie to właściwe.

3. **Dobra praktyka**

- Mockuj granice, nie czystą logikę rdzeniową.
- Utrzymuj oczekiwania skupione na obserwowalnym zachowaniu.

4. **Balans**

- Łącz unit testy z mockami z testami integration/feature dla pełniejszej pewności.

Mocking to precyzyjne narzędzie do izolacji i weryfikacji kontraktów współpracy.

</details>

<details>
<summary>134. Jak mockować Facades?</summary>

#### Laravel

Facades można mockować bezpośrednio, używając wbudowanych helperów mockowania.

1. **Podstawowe podejście**

```php
Cache::shouldReceive('put')
    ->once()
    ->with('key', 'value', 60);
```

2. **Typowe użycie**

- Asercja, że metoda facade została wywołana z oczekiwanymi argumentami.
- Zwracanie kontrolowanych wartości z wywołań facade.

3. **Kiedy zamiast tego preferować DI**

- W kluczowych serwisach biznesowych dependency injection z mockami interfejsów jest zwykle czystsze.
- Facade mocking jest wygodny dla frameworkowego glue code.

4. **Wskazówka**

- Używaj mocków facade świadomie; unikaj nadmiernego sprzęgania testów ze szczegółami implementacji.

Mockowanie facade jest użyteczne, ale na poziomie architektury DI pozostaje bardziej utrzymywalnym domyślnym wyborem dla logiki rdzeniowej.

</details>

<details>
<summary>135. Jak testować joby kolejkowane?</summary>

#### Laravel

Testowanie jobów kolejkowanych zwykle rozdziela sprawdzenie intencji dispatchu i zachowania samego joba.

1. **Test dispatchu (orkiestracja)**

- Zfake’uj kolejkę i asercją sprawdź, że job został wypchnięty.

```php
Queue::fake();
// wyzwól akcję
Queue::assertPushed(ProcessOrderJob::class);
```

2. **Test logiki joba**

- Utwórz instancję joba i wywołaj `handle()` z zamockowanymi zależnościami/serwisami.

3. **Zachowanie failure/retry**

- Testuj idempotencję i ścieżki błędów.
- Weryfikuj założenia retry/backoff dla krytycznych jobów.

4. **Dlaczego warto rozdzielać testy**

- Czytelniejsza diagnostyka: wiring dispatchu vs zachowanie biznesowe.

Dobre testy jobów kolejkowanych zapewniają zarówno poprawność planowania, jak i wykonania.

</details>

<details>
<summary>136. Jak testować eventy i listenery?</summary>

#### Laravel

Testy eventów/listenerów powinny weryfikować dispatch i reakcje listenerów z wyraźnym rozdzieleniem odpowiedzialności.

1. **Testy dispatchu eventów**

- Użyj `Event::fake()` i asercji dispatchu eventu z use case’u.

2. **Testy zachowania listenera**

- Testuj klasę listenera bezpośrednio (lub przez flow integracyjny).
- Asercją sprawdzaj side effecty (e-maile, aktualizacje DB, dispatch jobów).

3. **Queued listeners**

- Asercją sprawdzaj, że listener/job został skolejkowany zgodnie z oczekiwaniem.

4. **Dobra praktyka**

- Utrzymuj nazewnictwo eventów znaczące domenowo.
- Zapewnij, że listenery są idempotentne i bezpieczne dla retry.

Testowanie zarówno dispatchu, jak i ścieżek reakcji daje pewność w workflow event-driven.

</details>

<details>
<summary>137. Czym jest parallel testing?</summary>

#### Laravel

Parallel testing uruchamia suite’y testowe równolegle w wielu procesach, aby skrócić całkowity czas wykonania.

1. **Jak to działa**

- Dzieli pliki testowe na procesy workerów.
- Każdy proces uruchamia podzbiór testów współbieżnie.

2. **Korzyści**

- Szybsze pętle feedbacku w CI.
- Lepsza produktywność deweloperów przy dużych suite’ach.

3. **Wymagania**

- Poprawna izolacja testów.
- Osobne DB/zasoby per proces tam, gdzie to potrzebne.

4. **Typowe ryzyka**

- Współdzielony mutowalny stan lub nieizolowane zasoby powodujące flaky testy.

Parallel testing to jedna z najskuteczniejszych metod przyspieszania dużych suite’ów testowych Laravel.

</details>

<details>
<summary>138. Jak poprawić wydajność testów?</summary>

#### Laravel

Poprawa wydajności testów wymaga ograniczenia zbędnego kosztu integracji przy zachowaniu pewności jakości.

1. **Właściwy miks testów**

- Utrzymuj dużo szybkich unit testów.
- Ogranicz ciężkie feature testy do krytycznych flow.

2. **Używaj testów równoległych**

- Uruchamiaj testy w wielu procesach w CI/local.

3. **Optymalizuj użycie bazy danych**

- Używaj lekkiego setupu testowej DB.
- Unikaj nadmiernego seedingu per test, jeśli nie jest potrzebny.

4. **Fake’uj kosztowne granice**

- Fake’uj mail/queue/events/notifications, gdy side effecty nie są celem testu.

5. **Minimalizuj narzut setupu**

- Efektywnie reużywaj factory states/fixtures.
- Unikaj niepotrzebnej złożoności bootowania containera.

6. **Profiluj wolne testy**

- Śledź najwolniejsze pliki/przypadki testowe i refaktoruj hotspoty.

Szybkość testów rośnie najbardziej, gdy architektura i design testów stawiają na izolację i fokus.

</details>

<details>
<summary>139. Jakie korzyści daje używanie Vue.js z Laravel?</summary>

#### Laravel

Vue.js dobrze łączy się z Laravel, bo oba ekosystemy stawiają na szybką produktywność dewelopera i czytelne wzorce integracji.

1. **Płynna integracja**

- Natywne wsparcie przez Vite i prosty frontend scaffolding.
- Łatwe dopasowanie API + architektury komponentowej.

2. **Produktywność deweloperska**

- Reaktywne UI ze zwięzłym modelem komponentów.
- Dobry balans prostoty i możliwości dla produktów CRUD-heavy.

3. **Dopasowanie do ekosystemu**

- Silne community patterns dla stacków Laravel + Vue.
- Działa dobrze z Inertia lub podejściami SPA opartymi o API.

4. **Wartość praktyczna**

- Szybsze dostarczanie dynamicznych interfejsów przy zachowaniu Laravel jako solidnego backendu.

Vue z Laravel to pragmatyczny wybór full-stack dla wielu zespołów produktowych.

</details>

<details>
<summary>140. Czym jest Inertia.js i jak działa?</summary>

#### Laravel

Inertia.js pozwala budować nowoczesne doświadczenia single-page bez tworzenia osobnego backendu API.

1. **Główna idea**

- Trasy/kontrolery Laravel zwracają odpowiedzi Inertia.
- Strony frontendu to komponenty Vue/React/Svelte.
- Inertia obsługuje nawigację po stronie klienta i aktualizacje propsów strony.

2. **Jak działa przepływ**

- Żądanie trafia do kontrolera Laravel.
- Kontroler zwraca nazwę komponentu + propsy.
- Inertia podmienia komponent strony w przeglądarce bez pełnego przeładowania.

3. **Korzyści**

- UX zbliżony do SPA przy zachowaniu server-side routingu/kontroli.
- Brak potrzeby dublowania endpointów REST dla wewnętrznych stron aplikacji.
- Wspólne wzorce auth/walidacji/sesji z Laravel.

Inertia jest idealna, gdy chcesz interaktywność SPA z prostotą monolitycznego backendu.

</details>

<details>
<summary>141. Czym jest Livewire i kiedy go używać?</summary>

#### Laravel

Livewire to framework Laravel-first do budowania dynamicznych interfejsów z komponentami sterowanymi po stronie serwera i minimalną ilością własnego JavaScript.

1. **Jak działa**

- Komponenty UI to klasy PHP + widoki Blade.
- Interakcje w przeglądarce wywołują żądania AJAX.
- Serwer aktualizuje stan komponentu i zwraca różnice DOM.

2. **Kiedy używać**

- Panele administracyjne i narzędzia wewnętrzne.
- Workflow oparte o rozbudowane formularze.
- Zespoły preferujące PHP-first full-stack development.

3. **Korzyści**

- Szybki development przy niskiej złożoności frontendu.
- Ścisła integracja z Laravel auth/walidacją/policies.

4. **Trade-off**

- Dla bardzo interaktywnych, client-heavy aplikacji frameworki SPA mogą dać lepszą kontrolę frontendu.

Livewire świetnie nadaje się do dostarczania dynamicznego UI Laravel bez ciężkiej architektury frontendowej.

</details>

<details>
<summary>142. Porównaj podejścia Livewire, Inertia i tradycyjne SPA.</summary>

#### Laravel

Podejścia te różnią się głównie tym, gdzie „żyje” stan UI i logika renderowania.

1. **Livewire**

- Komponenty sterowane po stronie serwera (PHP + Blade).
- Wymaga minimalnego JS.
- Świetne dla zespołów Laravel-centric i UI formularzowo/adminowych.

2. **Inertia**

- Strony renderowane po stronie klienta (Vue/React/Svelte), z kontrolerami Laravel jako providerami stron backendowych.
- Nawigacja w stylu SPA bez osobnej publicznej warstwy API dla stron.

3. **Tradycyjne SPA (API + aplikacja frontendowa)**

- W pełni oddzielna aplikacja frontendowa konsumująca REST/GraphQL API.
- Maksymalna autonomia frontendu i decoupling.
- Większa złożoność (auth, kontrakty API, rozdzielenie deploymentu).

4. **Reguła decyzyjna**

- Szybkie PHP-first product UI: Livewire.
- Nowoczesny UX SPA z prostotą monolitu: Inertia.
- Architektura cross-platform/public API-first: tradycyjne SPA.

Wybór zależy od rozkładu kompetencji w zespole, wymagań UX produktu i granic architektonicznych.

</details>

<details>
<summary>143. Czym jest stack TALL?</summary>

#### Laravel

Stack TALL oznacza **Tailwind CSS, Alpine.js, Laravel, Livewire**.

1. **Komponenty**

- **Laravel**: framework backendowy.
- **Livewire**: reaktywne komponenty sterowane po stronie serwera.
- **Alpine.js**: lekka interaktywność frontendowa.
- **Tailwind CSS**: utility-first styling.

2. **Dlaczego zespoły używają TALL**

- Szybki full-stack development z minimalnym ciężkim toolingiem JS.
- Mocne dopasowanie do aplikacji CRUD/admin/business.
- Spójne Laravel-first developer experience.

3. **Typowe mocne strony**

- Szybka iteracja.
- Jasna architektura backend-centric.
- Niższa złożoność frontendu dla wielu use case’ów.

TALL to produktywny stack dla zespołów, które priorytetyzują szybkość rozwoju w stylu Laravel-centric.

</details>

<details>
<summary>144. Czym jest SSR (Server-Side Rendering) i czy Laravel go wspiera?</summary>

#### Laravel

SSR (Server-Side Rendering) oznacza, że HTML jest renderowany po stronie serwera, zanim trafi do przeglądarki.

1. **Dlaczego używa się SSR**

- Szybszy first content paint dla wielu stron.
- Lepsze SEO dla treści, które muszą być indeksowalne.
- Lepsza wydajność na wolniejszych urządzeniach/sieciach.

2. **Wsparcie Laravel**

- Natywne renderowanie Blade jest domyślnie po stronie serwera.
- SSR może być też używany w zintegrowanych z Laravel stackach frontendowych (np. frameworki JS ze wsparciem SSR + backend Laravel).

3. **Kiedy wybrać SSR**

- SEO-krytyczne/publiczne strony contentowe.
- Wrażliwe na wydajność doświadczenia pierwszego ładowania.

Laravel w pełni wspiera wzorce SSR, zarówno przez Blade, jak i hybrydowe architektury frontendowe.

</details>

<details>
<summary>145. Jak Laravel integruje się z React i Vue?</summary>

#### Laravel

Laravel integruje się z React/Vue przez Vite, wzorce routingu i wiele opcji architektonicznych.

1. **Tooling frontendowy**

- Vite buduje i serwuje assety React/Vue.
- Blade używa `@vite(...)` do ładowania skompilowanych entry.

2. **Style integracji**

- Blade + osadzone komponenty React/Vue.
- Inertia.js ze stronami React/Vue.
- Decoupled SPA konsumujące API Laravel.

3. **Punkty integracji backendu**

- Flow auth/session/token.
- Walidacja/obsługa błędów.
- Kontrakty oparte o API Resources/DTO.

4. **Praktyczna przewaga**

- Zespoły mogą wybrać poziom sprzężenia: integracja w stylu monolitu albo w pełni oddzielony frontend.

Laravel zapewnia elastyczne ścieżki integracji dla ekosystemów React i Vue.

</details>

<details>
<summary>146. Czym jest Ziggy w Laravel?</summary>

#### Laravel

Ziggy to pakiet, który udostępnia nazwane trasy Laravel w JavaScript, umożliwiając generowanie tras na frontendzie na podstawie definicji tras backendu.

1. **Jaki problem rozwiązuje**

- Unika hardkodowanych URL-i na frontendzie.
- Utrzymuje linki frontendowe zgodne z nazwami/parametrami tras Laravel.

2. **Jak działa**

- Udostępnia metadane tras frontendowi.
- Dostarcza helper `route()` w JavaScript.

3. **Koncepcja przykładu**

```js
route('posts.show', { post: 42 });
```

4. **Korzyści**

- Lepsza utrzymywalność podczas refaktoryzacji tras.
- Mniej błędów niedopasowania URL między backendem a frontendem.

Ziggy poprawia full-stackową spójność, gdy trasy Laravel są konsumowane przez klientów JS.

</details>

<details>
<summary>147. Czym jest Laravel Sail?</summary>

#### Laravel

Laravel Sail to oficjalne, lekkie, oparte o Docker lokalne środowisko developerskie dla Laravel.

1. **Co zapewnia**

- Wstępnie skonfigurowany setup Docker dla PHP, bazy danych, Redis i powiązanych usług.
- Spójne środowisko lokalne na maszynach całego zespołu.

2. **Dlaczego zespoły go używają**

- Szybszy onboarding.
- Mniej problemów typu „works on my machine”.
- Brak potrzeby ręcznej instalacji pełnego lokalnego stacku.

3. **Typowe użycie**

- Uruchamianie app/services/commands przez wrapper scripts Sail.

Sail to pragmatyczny domyślny wybór dla konteneryzowanego lokalnego developmentu Laravel.

</details>

<details>
<summary>148. Czym jest Laravel Forge?</summary>

#### Laravel

Laravel Forge to usługa provisioning’u serwerów i deploymentu dla aplikacji PHP/Laravel.

1. **Główny cel**

- Automatyzuje setup serwera (web server, PHP, podstawy bazy danych, SSL, deploy hooks).
- Upraszcza workflow deploymentu na dostawcach cloud VPS.

2. **Czym zarządza**

- Konfiguracją stron, skryptami deploymentowymi, setupem procesów queue/scheduler oraz certyfikatami.

3. **Dlaczego to ważne**

- Redukuje narzut DevOps dla zespołów Laravel.
- Standaryzuje wzorce deploymentu i zarządzania serwerami.

Forge pomaga zespołom utrzymywać aplikacje Laravel na produkcji bez budowania całej automatyzacji infrastruktury od zera.

</details>

<details>
<summary>149. Czym jest Laravel Vapor?</summary>

#### Laravel

Laravel Vapor to serverless platforma deploymentowa Laravel oparta o zarządzane usługi AWS.

1. **Co oferuje**

- Serverless runtime dla workloadów Laravel.
- Wzorce zarządzanej infrastruktury (compute, storage, integracje skalowania).

2. **Dlaczego zespoły ją wybierają**

- Autoscaling przy mniejszym narzucie zarządzania serwerami.
- Model pay-for-usage dopasowany do zmiennych wzorców ruchu.

3. **Najlepsze scenariusze użycia**

- Zespoły chcące serverless AWS z Laravel-focused DX.
- Aplikacje korzystające z elastycznego skalowania.

Vapor to Laravel-first ścieżka do serverless architektury produkcyjnej na AWS.

</details>

<details>
<summary>150. Czym jest Laravel Envoyer?</summary>

#### Laravel

Laravel Envoyer to narzędzie zero-downtime deploymentu dla aplikacji PHP/Laravel.

1. **Kluczowa zdolność**

- Deployuje nowe release’y bez wyłączania aplikacji.

2. **Jak to zwykle działa**

- Korzysta z release-based flow deploymentowego.
- Przełącza symlink aktywnego release’u po pomyślnym zakończeniu kroków.

3. **Dlaczego przydatne**

- Minimalizuje downtime widoczny dla użytkowników.
- Wspiera bezpieczniejsze rollbacki deploymentu.

Envoyer koncentruje się konkretnie na niezawodnej orkiestracji deploymentu zero-downtime.

</details>

<details>
<summary>151. Czym jest Laravel Pennant?</summary>

#### Laravel

Laravel Pennant to system feature flagów w Laravel do kontrolowania rolloutu funkcji.

1. **Co umożliwia**

- Włączanie/wyłączanie funkcji per użytkownik, grupa lub reguła.
- Stopniowe rollouty i wzorce eksperymentów.

2. **Use case’y**

- Canary releases.
- A/B-style ekspozycja funkcji.
- Bezpieczna progresywna migracja dużych zmian.

3. **Korzyści**

- Niższe ryzyko release’u.
- Szybszy rollback problematycznych funkcji bez pełnego rollbacku deploymentu.

Pennant zapewnia first-party feature flagging dla kontrolowanego dostarczania produktu.

</details>

<details>
<summary>152. Czym jest Laravel Pulse?</summary>

#### Laravel

Laravel Pulse to first-party pakiet do realtime application insights i monitoringu wydajności.

1. **Co pokazuje**

- Wysokopoziomowe metryki zdrowia aplikacji i trendy operacyjne.
- Widoczność sygnałów przepustowości/wydajności.

2. **Dlaczego jest przydatny**

- Szybka diagnostyka podczas incydentów.
- Lepsza świadomość zachowania runtime na produkcji.

3. **Pozycjonowanie**

- Uzupełnia logi oraz głębsze stacki tracingu/metryk.

Pulse pomaga zespołom Laravel obserwować zdrowie aplikacji narzędziami natywnymi dla frameworka.

</details>

<details>
<summary>153. Czym jest Laravel Telescope?</summary>

#### Laravel

Laravel Telescope to narzędzie debugowania i introspekcji dla środowisk local/staging.

1. **Co rejestruje**

- Żądania, wyjątki, zapytania, joby, maile, notyfikacje, zdarzenia cache i więcej.

2. **Dlaczego deweloperzy go używają**

- Szybsze debugowanie zachowania aplikacji.
- Łatwa widoczność wnętrza frameworka podczas developmentu.

3. **Wskazówka operacyjna**

- Zwykle ograniczany lub wyłączany na produkcji ze względu na wrażliwość danych i narzut.

Telescope to jedno z najbardziej użytecznych narzędzi observability natywnych dla Laravel w workflow developerskim.

</details>

<details>
<summary>154. Czym jest Laravel Scout?</summary>

#### Laravel

Laravel Scout to oparta o driverry abstrakcja full-text search dla modeli Eloquent.

1. **Co robi**

- Synchronizuje dane modeli z zewnętrznymi silnikami wyszukiwania.
- Udostępnia proste API do przeszukiwania modeli.

2. **Dlaczego jest potrzebny**

- Zapytania DB `LIKE` są ograniczone dla skalowalnego wyszukiwania z rankingiem trafności.
- Silniki wyszukiwania oferują lepsze możliwości indeksowania i rankingu.

3. **Typowy przepływ**

- Zmiany w modelach są indeksowane.
- Zapytania przechodzą przez skonfigurowany search driver.

Scout daje czysty interfejs Laravel do zaawansowanej infrastruktury wyszukiwania.

</details>

<details>
<summary>155. Jakich silników wyszukiwania może używać Laravel Scout?</summary>

#### Laravel

Laravel Scout wspiera wiele backendów wyszukiwania przez driverry.

1. **Najczęściej używane silniki**

- Algolia
- Meilisearch
- Typesense

2. **Inne opcje**

- Driverry w stylu database/collection dla prostych lub lokalnych scenariuszy.
- Community/custom driverry dla silników takich jak Elasticsearch/OpenSearch.

3. **Kryteria wyboru**

- Wymagana jakość trafności.
- Ograniczenia hostingowe/ops.
- Koszt, latencja i wolumen danych.

Abstrakcja Scout pozwala zespołom podmieniać lub rozwijać strategię backendu wyszukiwania przy mniejszym „churnie” warstwy aplikacji.

</details>

<details>
<summary>156. Czym jest Laravel Cashier?</summary>

#### Laravel

Laravel Cashier to pakiet do rozliczeń subskrypcyjnych, który upraszcza workflow płatności cyklicznych.

1. **Główny cel**

- Zarządzanie planami, subskrypcjami, trialami, kuponami, fakturami i logiką cyklu życia rozliczeń.

2. **Dlaczego jest przydatny**

- Enkapsuluje typowe wzorce rozliczeń SaaS.
- Redukuje boilerplate własnych integracji.

3. **Typowe scenariusze**

- Produkty SaaS oparte o subskrypcję.
- Implementacje rozliczeń metered lub tiered.

Cashier przyspiesza development płatności/subskrypcji w produktach opartych o Laravel.

</details>

<details>
<summary>157. Czym jest Laravel Socialite?</summary>

#### Laravel

Laravel Socialite to pakiet OAuth authentication w Laravel dla providerów social login.

1. **Co zapewnia**

- Helpery flow OAuth redirect/login.
- Pobieranie danych tożsamości użytkownika od providera.

2. **Typowi providerzy**

- Google, GitHub, Facebook i inni (zależnie od drivera).

3. **Dlaczego zespoły go używają**

- Szybsza implementacja funkcji „Login with ...”.
- Spójne API dla różnych providerów.

Socialite upraszcza integrację logowania OAuth third-party w aplikacjach Laravel.

</details>

<details>
<summary>158. Czym jest Laravel Pint?</summary>

#### Laravel

Laravel Pint to opinionated fixer stylu kodu PHP w Laravel, zbudowany na PHP-CS-Fixer.

1. **Cel**

- Automatyczne formatowanie kodu do spójnych reguł stylu.

2. **Dlaczego to ważne**

- Czystsze diffy i code review.
- Spójny styl w całym zespole przy minimalnym wysiłku ręcznym.

3. **Typowe użycie**

- Uruchamianie lokalnie i w CI dla egzekwowania zgodności stylu.

Pint poprawia spójność codebase i efektywność deweloperów.

</details>

<details>
<summary>159. Czym jest Laravel Folio?</summary>

#### Laravel

Laravel Folio to file-based podejście do routingu stron w aplikacjach Laravel.

1. **Główna idea**

- Bezpośrednie mapowanie plików na trasy/strony przy użyciu konwencji systemu plików.

2. **Dlaczego może być przydatne**

- Mniej boilerplate’u routingu dla aplikacji zorientowanych na strony.
- Szybsze scaffoldowanie prostych struktur tras.

3. **Kiedy używać**

- Aplikacje content/page-heavy, gdzie routing oparty o konwencję zwiększa szybkość developmentu.

Folio oferuje alternatywny styl routingu stron dla zespołów preferujących konwencje oparte o pliki.

</details>

<details>
<summary>160. Czym jest Laravel Precognition?</summary>

#### Laravel

Laravel Precognition umożliwia aplikacjom frontendowym prewalidację danych formularza względem reguł walidacji backendu przed pełnym wysłaniem.

1. **Co robi**

- Wysyła lekkie żądania z intencją walidacji.
- Zwraca feedback walidacyjny wcześnie, gdy użytkownik wypełnia formularz.

2. **Korzyści**

- Lepszy UX dzięki szybszemu feedbackowi walidacji.
- Reużycie logiki walidacji po stronie serwera jako source of truth.

3. **Gdzie pasuje**

- Złożone formularze w flow typu SPA/Inertia/Livewire.

Precognition pomaga dostarczać responsywne formularze bez duplikowania reguł walidacji między frontendem a backendem.

</details>

<details>
<summary>161. Czym są generatory PHP i kiedy ich używać?</summary>

#### PHP

Generatory to funkcje używające `yield`, aby produkować wartości leniwie, pojedynczo, zamiast budować pełne tablice w pamięci.

1. **Jaki problem rozwiązują**

- Pamięciooszczędna iteracja po dużych zbiorach danych lub strumieniach.

2. **Jak działają**

```php
function numbers(int $max): Generator
{
    for ($i = 1; $i <= $max; $i++) {
        yield $i;
    }
}
```

3. **Kiedy używać**

- Przetwarzanie dużych plików.
- Strumieniowanie rekordów z DB.
- Długie pipeline’y, gdzie pełna materializacja nie jest potrzebna.

4. **Korzyść**

- Mniejsze zużycie pamięci przy klarownej semantyce iteracji.

Używaj generatorów, gdy rozmiar danych jest duży lub nieznany, a przetwarzanie sekwencyjne jest wystarczające.

</details>

<details>
<summary>162. Czym są atrybuty PHP?</summary>

#### PHP

Atrybuty PHP to natywne adnotacje metadanych używające składni `#[...]`.

1. **Cel**

- Dołączanie ustrukturyzowanych metadanych do klas, metod, properties, parametrów itd.

2. **Przykład**

```php
#[Deprecated(reason: 'Use NewService')]
final class LegacyService {}
```

3. **Dlaczego są przydatne**

- Zastępują wiele wzorców adnotacji docblock metadanymi na poziomie języka.
- Poprawiają tooling, static analysis i integrację frameworkową.

4. **Kontekst Laravel**

- Mogą być używane w customowych rozszerzeniach frameworka, wzorcach metadanych walidacji/routingu i projektowaniu pakietów.

Atrybuty dostarczają jawne, czytelne maszynowo metadane bezpośrednio w kodzie.

</details>

<details>
<summary>163. Wyjaśnij strict types w PHP.</summary>

#### PHP

Strict types włącza się per plik przez `declare(strict_types=1);` i wymuszają bardziej rygorystyczne zachowanie typów skalarnych.

1. **Bez strict types**

- PHP może wykonywać coercion skalarów (`'10'` do `10`).

2. **Ze strict types**

- Niezgodne wartości skalarne wywołują `TypeError` zamiast cichej coercion.

```php
declare(strict_types=1);

function add(int $a, int $b): int
{
    return $a + $b;
}

add('2', 3); // TypeError
```

3. **Dlaczego to ważne**

- Lepsza poprawność i bezpieczniejszy refactoring.
- Silniejsze kontrakty i mniej ukrytych błędów konwersji.

Strict typing poprawia przewidywalność i jakość kodu w nowoczesnych codebase’ach PHP.

</details>

<details>
<summary>164. Wyjaśnij require, include, require_once i include_once.</summary>

#### PHP

Te konstrukcje języka ładują i wykonują pliki PHP, różniąc się zachowaniem przy błędach i duplikatach.

1. **`require`**

- Dołącza plik.
- Błąd fatalny, jeśli plik nie istnieje/jest nieczytelny.

2. **`include`**

- Dołącza plik.
- Warning, jeśli brakuje pliku; skrypt działa dalej.

3. **`require_once`**

- Jak `require`, ale gwarantuje dołączenie pliku tylko raz.

4. **`include_once`**

- Jak `include`, ale tylko raz.

5. **Praktyczna wskazówka**

- W nowoczesnych aplikacjach używaj autoloadingu Composera zamiast ręcznych wzorców include.
- Wariantów `require` używaj dla krytycznych zależności.

Warianty `_once` zapobiegają przypadkowym redeklaracjom przy podwójnym dołączaniu plików.

</details>

<details>
<summary>165. Czym są WeakMaps i jakie problemy rozwiązują?</summary>

#### PHP

`WeakMap` przechowuje asocjacje kluczowane obiektami, które nie blokują garbage collection tych obiektów.

1. **Rozwiązywany problem**

- Dołączanie metadanych/cache do obiektów bez powodowania memory leaków.

2. **Jak to działa**

- Kluczami muszą być obiekty.
- Gdy obiekt-klucz zostanie zniszczony, wpis znika automatycznie.

3. **Use case’y**

- Per-obiektowe cache’e wyliczonych metadanych.
- Śledzenie stanu zewnętrznego dla obiektów, których nie kontrolujesz.

4. **Dlaczego w tym przypadku lepsze niż tablice**

- Zwykłe tablice z kluczami/ID obiektów mogą utrzymywać przy życiu przestarzałe mapowania.

WeakMaps są przydatne do pamięciowo bezpiecznych danych pobocznych powiązanych z obiektami.

</details>

<details>
<summary>166. Czym jest operator spread/splat w PHP?</summary>

#### PHP

Operator spread `...` rozpakowuje tablice/iterables do argumentów funkcji albo literałów tablicowych.

1. **Rozpakowanie argumentów funkcji**

```php
$args = [2, 3];
$result = sum(...$args);
```

2. **Rozpakowanie tablicy**

```php
$a = [1, 2];
$b = [...$a, 3, 4];
```

3. **Variadic capture (powiązane użycie „splat”)**

```php
function logAll(string ...$messages): void {}
```

4. **Dlaczego przydatny**

- Czystsze przekazywanie argumentów i składanie tablic.

Operator poprawia czytelność i elastyczność wzorców kompozycji funkcji i tablic.

</details>

<details>
<summary>167. Czym są enumy w PHP 8.1+?</summary>

#### PHP

Enumy to natywne typy reprezentujące zamknięty zestaw dozwolonych wartości/case’ów.

1. **Rodzaje**

- Unit enums (bez wartości skalarnej).
- Backed enums (z wartością `string` lub `int`).

2. **Przykład**

```php
enum OrderStatus: string
{
    case Draft = 'draft';
    case Paid = 'paid';
    case Shipped = 'shipped';
}
```

3. **Dlaczego używać enumów**

- Zapobiegają nieprawidłowym stanom.
- Poprawiają type safety i czytelność.
- Lepsze wsparcie static analysis.

Enumy to preferowany nowoczesny sposób modelowania skończonych stanów domenowych w PHP.

</details>

<details>
<summary>168. Czym są readonly properties w PHP?</summary>

#### PHP

Readonly properties można przypisać tylko raz (zwykle w konstruktorze), a potem nie można ich modyfikować.

1. **Zachowanie**

- Jednorazowy zapis po inicjalizacji.
- Późniejsza mutacja rzuca błąd.

2. **Przykład**

```php
final class UserDto
{
    public function __construct(
        public readonly int $id,
        public readonly string $email,
    ) {}
}
```

3. **Dlaczego przydatne**

- Bezpieczniejsze immutable data objects.
- Mniej przypadkowych mutacji stanu.

Readonly properties wzmacniają niezmienność obiektów i klarowność kontraktów.

</details>

<details>
<summary>169. Czym są readonly classes w PHP 8.2+?</summary>

#### PHP

`Readonly class` sprawia, że wszystkie properties instancji są domyślnie readonly.

1. **Co to oznacza**

- Każde zadeklarowane property podlega semantyce readonly.
- Dobre dopasowanie dla immutable value/transfer objects.

2. **Przykład**

```php
readonly class Money
{
    public function __construct(
        public int $amount,
        public string $currency,
    ) {}
}
```

3. **Dlaczego warto używać**

- Wymusza politykę niezmienności na poziomie klasy.
- Redukuje boilerplate względem deklarowania każdego property osobno jako readonly.

Readonly classes czynią intencję niezmienności jawną i egzekwowalną.

</details>

<details>
<summary>170. Czym są intersection types i union types?</summary>

#### PHP

Union i intersection types wyrażają bogatsze kontrakty typów.

1. **Union type (`A|B`)**

- Wartość może być jednym z wymienionych typów.

2. **Intersection type (`A&B`)**

- Wartość musi jednocześnie spełniać wszystkie wymienione typy.

3. **Przykłady**

```php
function formatId(int|string $id): string { return (string) $id; }

function store(Cacheable&Jsonable $entity): void {}
```

4. **Dlaczego przydatne**

- Silniejsze kontrakty API.
- Lepsza static analysis i bezpieczniejszy refactoring.

Union = elastyczne alternatywy; intersection = połączone możliwości.

</details>

<details>
<summary>171. Czym są klasy anonimowe?</summary>

#### PHP

Klasy anonimowe to instancje klas tworzone inline, bez deklaracji nazwanej klasy.

1. **Przykład**

```php
$logger = new class {
    public function info(string $message): void {}
};
```

2. **Kiedy są przydatne**

- Małe, jednorazowe implementacje.
- Lokalne test doubles/stuby.
- Zachowanie typu strategia definiowane inline.

3. **Kompromis**

- Wygodne w zakresie lokalnym.
- Nazwane klasy są lepsze dla logiki reużywalnej lub złożonej.

Klasy anonimowe są pomocne do zwięzłych, lokalnych definicji obiektów.

</details>

<details>
<summary>172. Czym są first-class callables w PHP?</summary>

#### PHP

Składnia first-class callable (`...`) tworzy obiekty callable z funkcji/metod w zwięzły i bezpieczny typowo sposób.

1. **Przykład**

```php
$trimmer = trim(...);
$callable = $service->process(...);
```

2. **Dlaczego są przydatne**

- Czytelniejsze niż callable jako string lub tablica.
- Lepsza analiza statyczna i bezpieczniejszy refactoring.

3. **Przypadki użycia**

- Potoki funkcyjne (`array_map`, kolekcje).
- Wzorce wstrzykiwania callbacków.

First-class callables poprawiają czytelność i niezawodność kodu opartego na callbackach.

</details>

<details>
<summary>173. Czym są fibers w PHP?</summary>

#### PHP

Fibers to niskopoziomowe prymitywy współbieżności wprowadzone w PHP 8.1 do kooperacyjnej wielozadaniowości.

1. **Co umożliwiają**

- Ręczne wstrzymywanie i wznawianie kontekstu wykonania.
- Budowanie frameworków asynchronicznych i abstrakcji event loop.

2. **Ważna uwaga**

- Fibers nie są równoległymi wątkami.
- Wymagają orkiestracji przez runtime/bibliotekę.

3. **Gdzie są istotne**

- Biblioteki async i środowiska o wysokiej współbieżności.
- Zaawansowane abstrakcje nieblokującego I/O.

Fibers dostarczają fundamentów dla uporządkowanych modeli async w ekosystemie PHP.

</details>

<details>
<summary>174. Czym są backed enums?</summary>

#### PHP

Backed enums to enumy, których przypadki są mapowane na wartości skalarne (`string` lub `int`).

1. **Przykład**

```php
enum Status: string
{
    case Active = 'active';
    case Disabled = 'disabled';
}
```

2. **Dlaczego są ważne**

- Łatwe zapisywanie w DB i payloadach API.
- Type-safe reprezentacja domeny ze stabilnym mapowaniem skalarnym.

3. **Przydatne metody**

- `Status::from($value)` (rzuca wyjątek przy niepoprawnej wartości)
- `Status::tryFrom($value)` (zwraca `null` przy niepoprawnej wartości)

Backed enums są idealne dla skończonych stanów, które muszą czysto się serializować.

</details>

<details>
<summary>175. Jakie są różnice między interfejsami, klasami abstrakcyjnymi i traitami?</summary>

#### PHP

Te konstrukcje służą różnym celom związanym z abstrakcją i ponownym użyciem kodu.

1. **Interfejs**

- Definiuje wyłącznie kontrakt (sygnatury metod/stałe).
- Nie zawiera stanu implementacji.
- Pozwala na implementację wielu interfejsów.

2. **Klasa abstrakcyjna**

- Częściowa implementacja + współdzielony stan/zachowanie.
- Może zawierać metody abstrakcyjne i konkretne.
- Ograniczenie pojedynczego dziedziczenia.

3. **Trait**

- Jednostka horyzontalnego reuse kodu mieszana do klas.
- Współdzieli metody/właściwości między niepowiązanymi hierarchiami klas.

4. **Zasada wyboru**

- Interfejs dla kontraktów możliwości.
- Klasa abstrakcyjna dla wspólnego zachowania bazowego.
- Trait dla małych, reużywalnych fragmentów zachowania.

Prawidłowy wybór utrzymuje architekturę jawną i łatwą w utrzymaniu.

</details>

<details>
<summary>176. Czym są zasady SOLID i jak stosuje się je w Laravelu?</summary>

#### Laravel

Zasady SOLID to wytyczne projektowania OOP, które poprawiają utrzymywalność i rozszerzalność.

1. **S: Single Responsibility**

- Utrzymuj cienkie kontrolery; przenoś reguły biznesowe do usług/akcji.

2. **O: Open/Closed**

- Rozszerzaj zachowanie przez interfejsy, eventy, strategie, polityki.

3. **L: Liskov Substitution**

- Implementuj kontrakty spójnie, aby alternatywy były zamienne.

4. **I: Interface Segregation**

- Preferuj wyspecjalizowane interfejsy zamiast szerokich „god interfaces”.

5. **D: Dependency Inversion**

- Zależyj od kontraktów, a implementacje rozwiązuj przez service container.

W Laravelu SOLID stosuje się przez DI, kontrakty, warstwy usług i modularne granice architektury.

</details>

<details>
<summary>177. Jakie wzorce projektowe są najczęściej używane w aplikacjach Laravel?</summary>

#### Laravel

Aplikacje Laravel często łączą wzorce frameworkowe z klasycznymi wzorcami projektowymi.

1. **Najczęstsze wzorce**

- Repository
- Factory
- Strategy
- Observer
- Decorator
- Adapter
- Command (jobs/commands)

2. **Przykłady wzorców natywnych dla Laravel**

- Service container + dependency inversion.
- Event/listener pub-sub.
- Potok middleware.

3. **Dlaczego wzorce są ważne**

- Jasny podział odpowiedzialności.
- Łatwiejsze testowanie i podmiana implementacji.
- Lepsza długoterminowa skalowalność codebase.

Wzorce należy stosować tam, gdzie rozwiązują realną złożoność, a nie dodają zbędną abstrakcję.

</details>

<details>
<summary>178. Wyjaśnij wzorce Repository, Factory, Strategy i Observer.</summary>

#### PHP

Te wzorce rozwiązują różne problemy architektoniczne.

1. **Repository**

- Abstrahuje dostęp do danych za interfejsami.
- Oddziela logikę biznesową od szczegółów ORM/zapytań.

2. **Factory**

- Centralizuje logikę tworzenia obiektów.
- Przydatny, gdy proces tworzenia jest złożony lub wariantowy.

3. **Strategy**

- Enkapsuluje zamienne algorytmy/zachowania za wspólnym interfejsem.
- Pozwala wybrać implementację w runtime.

4. **Observer**

- Wzorzec powiadamiania one-to-many oparty na zdarzeniach.
- W Laravel: events/listeners oraz model observers.

Każdy wzorzec warto stosować tam, gdzie zmniejsza sprzężenie i porządkuje odpowiedzialności.

</details>

<details>
<summary>179. Czym jest PSR i które standardy PSR są najważniejsze dla programistów Laravel?</summary>

#### PHP

PSR (PHP Standards Recommendations) to standardy interoperacyjności tworzone przez PHP-FIG.

1. **Dlaczego PSR ma znaczenie**

- Spójne konwencje między pakietami/frameworkami.
- Lepsza interoperacyjność w ekosystemie Composer.

2. **Najważniejsze PSR dla developerów Laravel**

- **PSR-1/PSR-12**: styl kodowania/podstawowy standard kodu.
- **PSR-4**: standard autoloadingu.
- **PSR-3**: interfejs loggera.
- **PSR-7**: interfejsy wiadomości HTTP (konteksty integracji ekosystemowej).
- **PSR-11**: koncepcje interfejsu kontenera.

3. **Praktyczny wpływ**

- Łatwiejsze użycie bibliotek third-party i czystsze granice architektury.

Znajomość PSR pomaga programistom Laravel tworzyć bardziej przenośny i przyjazny dla ekosystemu kod.

</details>

<details>
<summary>180. Czym jest autoloading Composera i jak działa PSR-4?</summary>

#### PHP

Autoloading Composera mapuje nazwy klas na pliki, dzięki czemu klasy ładują się automatycznie bez ręcznych include/require.

1. **Rola autoloadu Composera**

- Generuje zoptymalizowany autoloader na podstawie mapowań pakietów/aplikacji.
- To standardowy punkt wejścia ładowania klas w nowoczesnych aplikacjach PHP.

2. **Zasada PSR-4**

- Prefiks przestrzeni nazw mapuje się na katalog bazowy.
- Segmenty namespace mapują się na podkatalogi.
- Nazwa klasy mapuje się na nazwę pliku.

3. **Przykładowa koncepcja mapowania**

- `App\` -> `app/`
- `App\Services\BillingService` -> `app/Services/BillingService.php`

4. **Dlaczego to ważne**

- Przewidywalna struktura.
- Brak ręcznych łańcuchów `require`.
- Lepsze wsparcie narzędzi i interoperacyjność pakietów.

Composer + PSR-4 to fundament ładowania klas w Laravelu i nowoczesnych projektach PHP.

</details>
