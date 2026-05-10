**Read in other languages: [English 🇺🇸](README.en.md),
[Polska 🇵🇱](README.pl.md), [German 🇩🇪](README.de.md), [French 🇫🇷](README.fr.md),
[Spanish 🇪🇸](README.es.md), [Українська 🇺🇦](README.md).**

<h1>
  PHP <img src="./assets/php.svg" width="40" height="40" alt="PHP logo"/>
</h1>

<h2>Most Popular PHP Interview Questions and Answers</h2>

<details>
<summary>1. What is PHP and what problems does it solve in modern backend development?</summary>

#### PHP

PHP is a server-side programming language designed primarily for web development. In modern backend development, PHP solves several practical problems:

1. **Fast HTTP backend development:** PHP makes it easy to build APIs, web applications, and server-rendered pages quickly.

2. **Request processing and business logic:** It handles incoming HTTP requests, validates data, executes business rules, and returns responses.

3. **Database integration:** PHP has mature tooling for working with databases (MySQL, PostgreSQL, SQLite) through PDO and ORMs.

4. **Session and authentication workflows:** It supports user sessions, login systems, cookie handling, and access control.

5. **Ecosystem for production apps:** Frameworks like Laravel and Symfony provide routing, dependency injection, queues, events, and testing infrastructure.

6. **Background processing:** PHP can run asynchronous jobs via queues (emails, reports, notifications, imports) outside of request-response flow.

7. **Scalability in real systems:** With OPcache, caching layers (Redis), containers, and horizontal scaling, PHP powers high-load systems.

8. **Integration with external services:** PHP is widely used for payment gateways, message brokers, third-party APIs, and cloud services.

In short, PHP solves the full backend cycle: receiving requests, processing data, interacting with storage, and delivering secure, maintainable web services.

</details>

<details>
<summary>2. What are the key differences between PHP and JavaScript (runtime, execution model)?</summary>

#### PHP

PHP and JavaScript are both widely used in web development, but they differ significantly in runtime model, execution flow, and typical backend behavior.

1. **Primary runtime environment:**
   PHP runs on the server (PHP-FPM, CLI, Swoole/RoadRunner), while JavaScript runs in the browser and on the server via Node.js/Deno/Bun.

2. **Execution model (classic):**
   Traditional PHP is request-per-process/request-per-worker: each HTTP request starts, executes, and ends with isolated state.
   JavaScript (Node.js) typically runs as a long-lived process with shared in-memory state.

3. **Concurrency model:**
   PHP concurrency is usually achieved by multiple workers/processes handling requests in parallel.
   JavaScript server runtimes use an event loop with async I/O and non-blocking operations in a single process (plus worker threads/process scaling when needed).

4. **State lifecycle:**
   In classic PHP, in-memory state is not durable across requests, so persistent state usually lives in Redis/DB/cache.
   In Node.js, process memory can persist between requests, which is convenient but requires careful state management.

5. **Typical web role:**
   PHP is traditionally backend-first (SSR, APIs, business logic).
   JavaScript is full-stack by nature: frontend UI language plus backend option.

6. **Ecosystem focus:**
   PHP ecosystem emphasizes backend frameworks (Laravel, Symfony), server templating, and enterprise web backends.
   JavaScript ecosystem strongly emphasizes frontend frameworks plus universal/full-stack tooling.

7. **Operational profile:**
   PHP is often deployed behind Nginx/Apache with PHP-FPM pools.
   JavaScript backends are commonly deployed as long-running app processes behind reverse proxies.

In practice, PHP is usually chosen for predictable request isolation and mature backend frameworks, while JavaScript is often chosen when teams want one language across frontend and backend with async-by-default server development.

</details>

<details>
<summary>3. What are the main features introduced in PHP 8.x (8.1–8.5)?</summary>

#### PHP

PHP 8.1–8.5 introduced major language and runtime improvements. The most important highlights by version:

1. **PHP 8.1 (released November 25, 2021):**
   Enums, readonly properties, fibers, first-class callable syntax, intersection types, and `never` return type.

2. **PHP 8.2 (released December 8, 2022):**
   Readonly classes, DNF types, stand-alone `null`/`false`/`true` types, new `Random` extension, and dynamic properties deprecation.

3. **PHP 8.3 (released November 23, 2023):**
   Typed class constants, `#[\Override]` attribute, dynamic class constant fetch (`Class::{$name}`), and readonly/cloning improvements.

4. **PHP 8.4 (released November 21, 2024):**
   Property hooks, asymmetric visibility (`public private(set)` style), `#[\Deprecated]` attribute, updated DOM API, and lazy object support.

5. **PHP 8.5 (released November 20, 2025):**
   Pipe operator (`|>`), URI extension, clone-with updates via `clone(...)`, `#[\NoDiscard]`, closures in constant expressions, and additional API/runtime improvements.

#### Why this matters

- **Better type safety:** stronger typing, safer contracts, fewer runtime surprises.
- **Cleaner domain modeling:** enums, readonly constructs, and modern property semantics.
- **More expressive code:** pipe operator, attributes, and improved callable support.
- **Performance and maintainability:** continuous engine, tooling, and standard-library evolution.

In short, PHP 8.x modernized the language significantly and made modern backend architecture easier to build and maintain.

</details>

<details>
<summary>4. What are enums, attributes, and readonly properties in PHP?</summary>

#### PHP

Enums, attributes, and readonly properties are modern PHP language features that improve correctness, readability, and maintainability.

1. **Enums**

- Enums define a fixed set of allowed values as a real type.
- They prevent invalid string/int states and make domain modeling safer.
- PHP supports:
  backed enums (`enum Status: string { ... }`) and unit enums (`enum Role { ... }`).

```php
enum OrderStatus: string
{
    case Draft = 'draft';
    case Paid = 'paid';
    case Shipped = 'shipped';
}
```

2. **Attributes**

- Attributes are native metadata (`#[...]`) attached to classes, methods, properties, parameters, and more.
- They replace many docblock annotation use cases with structured, machine-readable metadata.
- Common use cases: routing, validation, dependency injection, serialization rules, deprecation markers.

```php
#[Deprecated(reason: 'Use NewService instead')]
class LegacyService {}
```

3. **Readonly properties**

- A `readonly` property can be written only once (typically in the constructor).
- After initialization, mutation is forbidden.
- This is useful for immutable DTOs, value objects, and safer object design.

```php
final class UserDto
{
    public function __construct(
        public readonly int $id,
        public readonly string $email,
    ) {}
}
```

#### Why they matter together

- **Enums** protect allowed states.
- **Attributes** provide explicit metadata for frameworks and tools.
- **Readonly properties** enforce immutability of critical data.

Together, these features reduce bugs, make APIs clearer, and improve static analysis quality in modern PHP codebases.

</details>

<details>
<summary>5. What is strict typing in PHP and why is it important?</summary>

#### PHP

Strict typing in PHP is enabled per file with:

```php
declare(strict_types=1);
```

When strict typing is enabled, scalar type declarations are enforced more strictly for function arguments and return values.

1. **Without strict types (`strict_types=0`, default):**
   PHP may coerce scalar values (for example, `'10'` to `10`) when possible.

2. **With strict types (`strict_types=1`):**
   PHP throws a `TypeError` instead of silently converting incompatible scalar values.

```php
declare(strict_types=1);

function add(int $a, int $b): int
{
    return $a + $b;
}

add('2', 3); // TypeError in strict mode
```

#### Why it is important

- **Early error detection:** type mismatches fail immediately.
- **Safer refactoring:** clearer contracts reduce hidden breakages.
- **More predictable behavior:** less implicit conversion magic.
- **Better static analysis:** tools like PHPStan/Psalm become more effective.
- **Cleaner API boundaries:** function signatures are treated as strict contracts.

#### Practical recommendation

Use `declare(strict_types=1);` in all new PHP files and combine it with explicit type hints, DTOs/value objects, and static analysis for production-grade reliability.

</details>

<details>
<summary>6. What are union and intersection types?</summary>

#### PHP

Union and intersection types in PHP are tools for expressing stricter and more explicit type contracts.

1. **Union types (`A|B`)**

- A value can be of **one of several allowed types**.
- Useful when an argument or return value can legitimately vary.

```php
function formatId(int|string $id): string
{
    return (string) $id;
}
```

2. **Intersection types (`A&B`)**

- A value must satisfy **all listed types at the same time**.
- Commonly used with interfaces to require multiple capabilities.

```php
interface Cacheable {}
interface Jsonable { public function toJson(): string; }

function store(Cacheable&Jsonable $entity): void
{
    // $entity must implement both interfaces
}
```

3. **Key difference**

- `A|B` means **either A or B**.
- `A&B` means **A and B together**.

4. **Why they matter**

- Better API contracts and self-documenting code.
- Fewer runtime errors from invalid object/value shapes.
- Stronger static analysis and safer refactoring.

5. **Practical guidance**

- Use union types for flexible input boundaries.
- Use intersection types for capability-based design (especially with interfaces).
- Prefer specific types over `mixed` when possible.

</details>

<details>
<summary>7. What is the nullsafe operator and when would you use it?</summary>

#### PHP

The nullsafe operator in PHP is `?->`. It allows safe method/property access on objects that may be `null`.

1. **What it does**

- If the left side is an object, access continues normally.
- If the left side is `null`, evaluation stops and returns `null` instead of throwing an error.

```php
$country = $user?->getProfile()?->getAddress()?->country;
```

2. **Why it is useful**

- Prevents verbose nested null checks.
- Reduces boilerplate in optional object chains.
- Makes intent clearer when values are legitimately nullable.

3. **Typical use cases**

- API/DTO structures with optional nested fields.
- ORM relations that may be missing.
- Request context objects where some parts are optional.

4. **Equivalent without nullsafe (more verbose)**

```php
$country = null;
if ($user !== null) {
    $profile = $user->getProfile();
    if ($profile !== null) {
        $address = $profile->getAddress();
        if ($address !== null) {
            $country = $address->country;
        }
    }
}
```

5. **Important notes**

- `?->` works only for object access (methods/properties), not array offsets.
- It short-circuits left-to-right.
- If the chain resolves to `null`, final result is `null`.

Use the nullsafe operator when null is an expected state and you want concise, safe traversal of object graphs.

</details>

<details>
<summary>8. What are property hooks (PHP 8.4+)?</summary>

#### PHP

Property hooks (introduced in PHP 8.4) let you attach logic directly to property read/write operations using `get` and `set` hooks.

1. **What problem they solve**

- Reduce boilerplate getter/setter methods.
- Keep validation/transformation close to the property definition.
- Allow computed (virtual) properties with clearer syntax.

2. **Basic idea**

```php
class User
{
    public string $name {
        set => trim($value);
    }
}
```

Any assignment to `$user->name` goes through the `set` hook.

3. **Computed property example**

```php
class Person
{
    public function __construct(
        public string $firstName,
        public string $lastName,
    ) {}

    public string $fullName {
        get => $this->firstName . ' ' . $this->lastName;
    }
}
```

`$fullName` is derived from other fields and does not need manual getter methods.

4. **Validation/transformation example**

```php
class Product
{
    public float $price {
        set {
            if ($value < 0) {
                throw new InvalidArgumentException('Price cannot be negative');
            }
            $this->price = round($value, 2);
        }
    }
}
```

5. **When to use**

- Domain entities with strict invariants.
- DTO/value-like objects that need controlled writes.
- Cases where old-style get/set methods were mostly boilerplate.

Property hooks make object models more expressive and reduce repetitive accessor code while preserving strong validation and encapsulation.

</details>

<details>
<summary>9. What is the pipe operator (PHP 8.5) and when is it useful?</summary>

#### PHP

The pipe operator in PHP 8.5 is `|>`. It passes the result of the left expression into the callable on the right, enabling readable left-to-right data transformation.

1. **Core idea**

Instead of deeply nested calls, you can build a linear processing pipeline.

```php
$result = " Hello World "
    |> trim(...)
    |> strtolower(...)
    |> (fn(string $s) => str_replace(' ', '-', $s));
```

2. **Why it is useful**

- Improves readability of multi-step transformations.
- Reduces temporary variables.
- Avoids inside-out nested function calls.
- Makes refactoring transformation chains easier.

3. **Before vs after**

Without pipe:

```php
$slug = strtolower(str_replace(' ', '-', trim($title)));
```

With pipe:

```php
$slug = $title
    |> trim(...)
    |> (fn(string $s) => str_replace(' ', '-', $s))
    |> strtolower(...);
```

4. **Good use cases**

- String/data normalization pipelines.
- DTO mapping/transformation flows.
- Functional-style data processing in services.

5. **Practical note**

Use the pipe operator for clear sequential transformations. For complex branching logic, regular intermediate variables may still be easier to understand.

</details>

<details>
<summary>10. What are superglobals in PHP and how are they used?</summary>

#### PHP

Superglobals in PHP are built-in associative arrays available in all scopes (functions, methods, global scope) without using `global`.

1. **Main superglobals**

- `$_GET` - query string parameters from URL.
- `$_POST` - form/body parameters from POST requests.
- `$_REQUEST` - merged request data (depends on `request_order`/`variables_order`).
- `$_SERVER` - server and request metadata (headers, method, URI, host, etc.).
- `$_COOKIE` - client cookies sent with request.
- `$_SESSION` - session data stored between requests.
- `$_FILES` - uploaded file metadata.
- `$_ENV` - environment variables.
- `$GLOBALS` - reference to all global variables.

2. **Typical usage examples**

```php
$page = $_GET['page'] ?? 'home';
$method = $_SERVER['REQUEST_METHOD'] ?? 'GET';
$token = $_COOKIE['csrf_token'] ?? null;
```

3. **Why they matter**

- They are the primary interface between PHP code and HTTP/runtime environment.
- They provide request input, context, and persisted user/session state.

4. **Security and reliability practices**

- Never trust superglobal input directly.
- Always validate and sanitize external data.
- Use strict checks and defaults (`??`, `filter_input`, validators).
- Avoid relying on `$_REQUEST` in critical code because source precedence can vary.
- Escape output to prevent XSS and use prepared statements to prevent SQL injection.

Superglobals are foundational to PHP web development, but they should be treated as untrusted input boundaries.

</details>

<details>
<summary>11. What is the difference between GET and POST requests?</summary>

#### PHP

GET and POST are HTTP methods with different semantics and usage patterns.

1. **Purpose**

- **GET** is used to retrieve data (read-only operations).
- **POST** is used to submit data that may change server state (create/process actions).

2. **Where data is sent**

- **GET** sends parameters in the URL query string (`/users?page=2`).
- **POST** sends data in the request body.

3. **Visibility and logging**

- **GET** parameters are visible in URL, browser history, logs, and referrers.
- **POST** body is not shown in URL, but still must be treated as untrusted input.

4. **Caching and bookmarking**

- **GET** requests are cache-friendly and bookmarkable.
- **POST** requests are generally not cacheable by default and not bookmarkable with payload.

5. **Idempotency and safety (HTTP semantics)**

- **GET** should be safe and not change server state.
- **POST** is not guaranteed to be idempotent and usually performs side effects.

6. **PHP access**

```php
$search = $_GET['q'] ?? null;      // from query string
$email  = $_POST['email'] ?? null; // from request body
```

7. **When to use**

- Use **GET** for filtering, searching, pagination, and resource reads.
- Use **POST** for form submissions, authentication actions, and creating/updating server-side data (or use PUT/PATCH where appropriate in APIs).

The key rule: use GET for read operations and POST for state-changing operations, while validating all input in both cases.

</details>

<details>
<summary>12. How does PHP handle HTTP requests and responses?</summary>

#### PHP

In a typical web setup, PHP handles HTTP through a request-response lifecycle coordinated by a web server (Nginx/Apache) and a PHP runtime (commonly PHP-FPM).

1. **Request arrives**

- Client sends an HTTP request (method, URI, headers, body).
- Web server receives it and routes dynamic requests to PHP.

2. **PHP runtime executes script**

- PHP initializes request context and populates superglobals (`$_SERVER`, `$_GET`, `$_POST`, `$_COOKIE`, `$_FILES`).
- Application bootstrap runs (autoload, config, DI container, framework kernel).

3. **Application handles business logic**

- Router resolves controller/handler.
- Middleware/guards/validation run.
- Services/repositories access database, cache, or external APIs.

4. **Response is built**

- App sets status code, headers, and body (HTML/JSON/file/stream).
- In plain PHP, this is typically via `header()`, `http_response_code()`, and output.
- In frameworks, a Response object is returned and then emitted.

```php
http_response_code(200);
header('Content-Type: application/json; charset=utf-8');
echo json_encode(['ok' => true], JSON_THROW_ON_ERROR);
```

5. **Response is sent**

- PHP sends output to web server.
- Web server sends final HTTP response to client.
- In classic PHP-FPM, request state ends after response (shared external storage is used for persistence).

6. **Error handling**

- Exceptions are converted to HTTP error responses (for example, `404`, `422`, `500`) by framework/global handlers.
- Logs/monitoring capture failures for diagnostics.

PHP’s model is straightforward: receive request context, execute application code, produce an HTTP response, and finish the request cleanly.

</details>

<details>
<summary>13. How do sessions work and what are secure session practices?</summary>

#### PHP

PHP sessions allow you to persist user-specific state between stateless HTTP requests by storing data server-side and linking it to a session ID.

1. **How sessions work**

- Client makes first request.
- Server creates a session ID (SID).
- SID is sent to client, usually via cookie (commonly `PHPSESSID`).
- On next requests, client sends SID back.
- PHP loads corresponding server-side session data into `$_SESSION`.

2. **Basic usage**

```php
session_start();

$_SESSION['user_id'] = 42;
$userId = $_SESSION['user_id'] ?? null;
```

3. **Where data is stored**

- By default: filesystem session storage.
- In production: often Redis/database/memcached via custom handlers for scalability.

4. **Secure session practices**

- Regenerate session ID after login/privilege change:
  `session_regenerate_id(true);`
- Use cookie flags:
  `HttpOnly`, `Secure`, `SameSite` (`Lax` or `Strict` when possible).
- Enforce HTTPS for authenticated apps.
- Set session timeout and inactivity expiration.
- Invalidate session on logout (unset data + destroy session + expire cookie).
- Bind sessions carefully to context signals (for example, partial IP/UA checks) to reduce hijacking risk.
- Store minimal sensitive data in session; prefer IDs/references over full secrets.

5. **Common threats**

- **Session fixation:** attacker forces known SID before authentication.
- **Session hijacking:** stolen SID is reused by attacker.
- **XSS-assisted theft:** malicious scripts can exploit insecure session handling.

6. **Hardening checklist**

- `session.use_strict_mode=1`
- `session.cookie_httponly=1`
- `session.cookie_secure=1` (on HTTPS)
- Proper `session.cookie_samesite`
- Regular SID regeneration for authenticated flows

Sessions are secure and effective when IDs are protected, rotated appropriately, and transported only over trusted channels.

</details>

<details>
<summary>14. How are cookies set and secured in modern applications?</summary>

#### PHP

Cookies are small key-value data stored by the browser and sent with matching requests. In modern apps, they are used for sessions, preferences, and secure auth flows.

1. **How cookies are set in PHP**

Use `setcookie()` (or framework response helpers) before output is sent:

```php
setcookie(
    'session_token',
    $token,
    [
        'expires'  => time() + 3600,
        'path'     => '/',
        'domain'   => 'example.com',
        'secure'   => true,
        'httponly' => true,
        'samesite' => 'Lax',
    ]
);
```

2. **How cookies are read**

```php
$token = $_COOKIE['session_token'] ?? null;
```

3. **Security attributes (critical)**

- **`Secure`**: cookie sent only over HTTPS.
- **`HttpOnly`**: not accessible from JavaScript (`document.cookie`), reduces XSS theft risk.
- **`SameSite`**:
  `Strict` (strong CSRF protection), `Lax` (balanced), `None` (requires `Secure`, for cross-site use cases).
- **`Expires/Max-Age`**: limit lifetime.
- **`Path/Domain`**: scope cookie as narrowly as possible.

4. **Best practices**

- Use HTTPS everywhere and always set `Secure` for sensitive cookies.
- Set `HttpOnly` for session/auth cookies.
- Prefer `SameSite=Lax` or `Strict` unless cross-site behavior is explicitly required.
- Rotate auth/session tokens and expire them appropriately.
- Do not store sensitive plaintext data in cookies.
- Consider signing or encrypting cookie payloads if storing state client-side.

5. **Common mistakes**

- Missing `HttpOnly` or `Secure`.
- Overly broad `domain`/`path`.
- Very long expiration for auth cookies.
- Trusting cookie values without server-side verification.

Modern cookie security is about strict scope, secure transport, safe defaults, and server-side validation of all client-provided values.

</details>

<details>
<summary>15. What is CSRF and how do you prevent it?</summary>

#### PHP

CSRF (Cross-Site Request Forgery) is an attack where a victim’s browser is tricked into sending an authenticated request to your application without the user’s intent.

1. **How CSRF works**

- User is logged into `your-app.com`.
- Attacker lures user to a malicious page.
- That page triggers a request to `your-app.com` (for example, change email, transfer funds).
- Browser automatically includes cookies/session, so request may be accepted.

2. **Why it is dangerous**

- The server sees a valid authenticated session.
- State-changing actions can be executed on behalf of the victim.

3. **Primary defense: CSRF token**

- Generate a random token per session/request.
- Embed token in forms or request headers.
- Verify token server-side before processing state-changing actions.

```php
session_start();

// Generate token once
$_SESSION['csrf_token'] ??= bin2hex(random_bytes(32));

// Validate on POST
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $token = $_POST['_csrf'] ?? '';
    if (!hash_equals($_SESSION['csrf_token'], $token)) {
        http_response_code(419);
        exit('Invalid CSRF token');
    }
}
```

4. **Additional protections**

- Use `SameSite` cookies (`Lax`/`Strict`) to reduce cross-site cookie sending.
- Validate `Origin`/`Referer` headers for sensitive endpoints (as defense-in-depth).
- Require re-auth or step-up confirmation for critical operations.
- Do not use GET for state-changing actions.

5. **Best practice in frameworks**

- Use built-in CSRF middleware (Laravel/Symfony/etc.) instead of custom logic where possible.
- Ensure tokens are included in all mutating requests (POST/PUT/PATCH/DELETE), including AJAX calls.

CSRF protection is mandatory for cookie-based authentication flows and should be part of default security middleware.

</details>

<details>
<summary>16. What is XSS and how do you prevent it properly?</summary>

#### PHP

XSS (Cross-Site Scripting) is a vulnerability where attacker-controlled data is interpreted by the browser as executable script in your application’s pages.

1. **Main XSS types**

- **Stored XSS**: malicious payload is saved (DB/comment/profile) and served to users later.
- **Reflected XSS**: payload comes from request input and is reflected immediately in response.
- **DOM-based XSS**: client-side JavaScript writes unsafe data into the DOM.

2. **Root cause**

- Untrusted input reaches HTML/JS/URL/CSS contexts without correct output encoding.

3. **Primary defense: contextual output escaping**

- Escape data **at output**, based on rendering context.
- For HTML text context in PHP:

```php
echo htmlspecialchars($userInput, ENT_QUOTES | ENT_SUBSTITUTE, 'UTF-8');
```

4. **Context-specific rules**

- HTML body: `htmlspecialchars(...)`.
- HTML attributes: also escape quotes (`ENT_QUOTES`).
- JavaScript context: JSON-encode data, avoid direct string concatenation.
- URL context: `rawurlencode()` for parameter values.
- Avoid injecting untrusted HTML directly.

5. **Additional protections**

- Use templating engines/framework auto-escaping features.
- Sanitize rich HTML with allowlist-based sanitizers (if HTML input is required).
- Set strong Content Security Policy (CSP) as defense-in-depth.
- Avoid inline scripts where possible.
- Validate input, but do not treat validation as a replacement for output encoding.

6. **Common mistakes**

- Escaping input once and reusing in multiple contexts.
- Disabling template auto-escaping globally.
- Rendering raw user content in admin panels/internal tools.

XSS prevention is mostly about strict contextual encoding at the point of output plus CSP and safe rendering patterns.

</details>

<details>
<summary>17. What is SQL Injection and how do prepared statements prevent it?</summary>

#### PHP

SQL Injection is a vulnerability where attacker input changes the structure of SQL queries, allowing unauthorized data access or manipulation.

1. **How SQL Injection happens**

It occurs when untrusted input is concatenated directly into SQL strings.

```php
// Unsafe example
$sql = "SELECT * FROM users WHERE email = '" . $_POST['email'] . "'";
```

An attacker can inject SQL fragments and alter query logic.

2. **Impact**

- Authentication bypass
- Data leakage/modification/deletion
- Privilege escalation
- In severe cases, full database compromise

3. **How prepared statements prevent it**

Prepared statements separate:
- **SQL structure** (query template)
- **Data values** (bound parameters)

The database treats bound values as data, not executable SQL code.

```php
$pdo = new PDO($dsn, $user, $pass, [
    PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
]);

$stmt = $pdo->prepare('SELECT * FROM users WHERE email = :email');
$stmt->execute(['email' => $_POST['email']]);
$user = $stmt->fetch(PDO::FETCH_ASSOC);
```

4. **Important nuance**

- Prepared statements protect values, but not dynamic SQL identifiers (table/column names).
- If identifiers must be dynamic, use strict allowlists.

5. **Best practices**

- Use PDO/MySQLi prepared statements everywhere for external input.
- Never build SQL with string concatenation for user-provided values.
- Enforce least-privilege DB accounts.
- Validate input and log suspicious activity.
- Keep DB engine/drivers updated.

Prepared statements are the primary and mandatory defense against SQL injection in modern PHP applications.

</details>

<details>
<summary>18. What is Content Security Policy (CSP)?</summary>

#### PHP

Content Security Policy (CSP) is a browser security mechanism that restricts which resources (scripts, styles, images, frames, etc.) are allowed to load and execute on a page.

1. **What CSP protects against**

- Primarily reduces XSS impact by blocking unauthorized inline/external scripts.
- Helps mitigate data exfiltration via malicious resource loads.
- Restricts risky browser capabilities to trusted origins.

2. **How CSP is delivered**

- Usually via HTTP response header:
  `Content-Security-Policy: ...`
- Can also be sent in report-only mode first:
  `Content-Security-Policy-Report-Only: ...`

3. **Basic example**

```php
header("Content-Security-Policy: default-src 'self'; script-src 'self'; object-src 'none'; base-uri 'self'; frame-ancestors 'none'");
```

4. **Important directives**

- `default-src` - fallback source policy.
- `script-src` - controls JavaScript sources.
- `style-src` - controls CSS sources.
- `img-src` - controls image sources.
- `connect-src` - controls XHR/fetch/WebSocket targets.
- `frame-ancestors` - prevents clickjacking by controlling embedding.
- `object-src 'none'` - disables legacy plugin content.
- `base-uri` - restricts `<base>` tag injection.

5. **Best practices**

- Start with `Report-Only`, collect violations, then enforce.
- Prefer nonces/hashes for inline scripts instead of `'unsafe-inline'`.
- Keep policy strict and explicit per environment.
- Combine CSP with output escaping, CSRF protection, and secure cookies.

6. **CSP is not a silver bullet**

- It is defense-in-depth, not a replacement for secure coding.
- You still must sanitize/escape untrusted output and avoid unsafe DOM patterns.

CSP significantly strengthens frontend security posture when configured carefully and monitored continuously.

</details>

<details>
<summary>19. What is autoloading and how does PSR-4 work?</summary>

#### PHP

Autoloading is a mechanism that automatically loads PHP class/interface/trait files when they are first used, instead of manually writing many `require`/`include` statements.

1. **Why autoloading is needed**

- Removes manual file includes.
- Keeps project structure scalable.
- Makes dependencies and modules easier to manage.

2. **PSR-4 in short**

PSR-4 is the modern standard for mapping namespaces to filesystem paths.

- Namespace prefix maps to a base directory.
- Remaining namespace parts map to subdirectories.
- Class name maps to file name (`ClassName.php`).

3. **Example mapping**

If Composer config contains:

```json
{
  "autoload": {
    "psr-4": {
      "App\\": "src/"
    }
  }
}
```

Then:
- `App\Services\UserService` -> `src/Services/UserService.php`
- `App\Http\Controllers\HomeController` -> `src/Http/Controllers/HomeController.php`

4. **How Composer enables it**

- Define `autoload.psr-4` in `composer.json`.
- Run:

```bash
composer dump-autoload
```

- Include Composer autoloader once (usually in app bootstrap):

```php
require __DIR__ . '/vendor/autoload.php';
```

5. **Best practices**

- Follow one class per file.
- Keep namespace and directory names aligned.
- Use meaningful root namespace (`App\\`, `Domain\\`, `Company\\Project\\`).
- Regenerate autoload files after namespace/path changes.

Autoloading with PSR-4 is the default foundation of modern PHP application structure and dependency loading.

</details>

<details>
<summary>20. What is Composer and how does dependency management work?</summary>

#### PHP

Composer is the standard dependency manager for PHP. It installs, updates, and autoloads project libraries in a reproducible way.

1. **Core files**

- `composer.json` - declares project metadata, required packages, autoload rules, scripts.
- `composer.lock` - locks exact package versions resolved for the project.
- `vendor/` - installed dependencies and Composer autoloader.

2. **How dependency management works**

- You declare constraints in `composer.json` (for example, `^11.0`).
- Composer resolves a compatible dependency graph.
- Resolved exact versions are written to `composer.lock`.
- Team/CI installs the exact locked versions for deterministic builds.

3. **Basic workflow**

```bash
# Add dependency
composer require monolog/monolog

# Install from lock file
composer install

# Update dependencies (re-resolve constraints)
composer update
```

4. **Version constraints**

- `^1.2` - allows non-breaking updates up to `<2.0.0`.
- `~1.2.3` - allows patch/minor within that branch.
- Exact versions are possible but usually too rigid for libraries.

5. **Autoload integration**

Composer generates `vendor/autoload.php` and supports PSR-4 autoload mapping from `composer.json`.

```php
require __DIR__ . '/vendor/autoload.php';
```

6. **Best practices**

- Commit `composer.lock` for applications.
- Use `composer install` in CI/production.
- Use `composer update` intentionally and review lock-file changes.
- Prefer stable package versions.
- Audit dependencies regularly (`composer audit`).

Composer is essential in modern PHP because it standardizes package management, autoloading, and reproducible builds across environments.

</details>

<details>
<summary>21. What are PSR standards and why are they important?</summary>

#### PHP

PSR (PHP Standards Recommendations) are community standards published by PHP-FIG (PHP Framework Interop Group) to improve interoperability and consistency across PHP libraries and frameworks.

1. **What PSRs define**

- Coding style conventions (for example, PSR-12).
- Autoloading conventions (PSR-4).
- Common interfaces for HTTP messages, middleware, containers, logging, caching, etc.

2. **Why they are important**

- **Interoperability:** libraries from different vendors work together more easily.
- **Predictability:** familiar interfaces and structure across projects.
- **Maintainability:** team codebases are more consistent and easier to review.
- **Framework portability:** less vendor lock-in when architecture uses standard contracts.

3. **Commonly used PSRs**

- **PSR-1 / PSR-12** - basic coding style and extended coding style.
- **PSR-3** - logger interface (`LoggerInterface`).
- **PSR-4** - autoloading standard.
- **PSR-6 / PSR-16** - cache interfaces.
- **PSR-7** - HTTP message interfaces (Request/Response/Stream).
- **PSR-11** - container interface.
- **PSR-15** - HTTP server request handlers and middleware.
- **PSR-18** - HTTP client interface.

4. **Practical effect in real projects**

- You can swap implementations (for example, logger/client/container) without rewriting business logic.
- Frameworks and packages integrate faster through shared interfaces.
- Tooling (linters/static analyzers/framework adapters) becomes easier to adopt.

PSRs are not just style guides; they are architecture-level contracts that make modern PHP ecosystems composable and sustainable.

</details>

<details>
<summary>22. What is PSR-7 (HTTP messages)?</summary>

#### PHP

PSR-7 is a standard that defines interfaces for HTTP messages in PHP: requests, responses, streams, and uploaded files.

1. **What PSR-7 standardizes**

- `ServerRequestInterface` - incoming HTTP request from client/server context.
- `RequestInterface` - generic outbound request.
- `ResponseInterface` - HTTP response (status, headers, body).
- `StreamInterface` - message body abstraction.
- `UploadedFileInterface` - uploaded file abstraction.
- `UriInterface` - URI representation.

2. **Why it matters**

- Provides a common contract across frameworks and libraries.
- Enables middleware pipelines and reusable HTTP components.
- Reduces vendor lock-in by coding to interfaces, not concrete framework classes.

3. **Immutability principle**

PSR-7 messages are immutable. Methods like `withHeader()` return a new instance rather than modifying the original object.

```php
$newResponse = $response
    ->withStatus(201)
    ->withHeader('Content-Type', 'application/json');
```

4. **Typical usage**

- In middleware and handlers (often with PSR-15).
- In API frameworks for request parsing and response generation.
- In HTTP clients/servers that exchange standardized message objects.

5. **Practical benefit**

A component written for PSR-7 can usually be reused in different ecosystems (Slim, Laminas, Symfony bridges, Mezzio, etc.) with minimal adaptation.

PSR-7 is the core interoperability layer for HTTP message handling in modern PHP applications.

</details>

<details>
<summary>23. What is PSR-11 (dependency container)?</summary>

#### PHP

PSR-11 is the standard interface for dependency injection containers in PHP. It defines how application code can retrieve services from a container in a framework-agnostic way.

1. **Core PSR-11 interfaces**

- `Psr\Container\ContainerInterface`
- `Psr\Container\ContainerExceptionInterface`
- `Psr\Container\NotFoundExceptionInterface`

Main methods:
- `get(string $id): mixed`
- `has(string $id): bool`

2. **What it solves**

- Standardizes container access across libraries/frameworks.
- Allows components to depend on a common contract instead of specific container implementations.
- Improves interoperability and portability.

3. **Simple usage example**

```php
use Psr\Container\ContainerInterface;

function run(ContainerInterface $container): void
{
    if ($container->has('logger')) {
        $logger = $container->get('logger');
        $logger->info('Started');
    }
}
```

4. **Important design note**

PSR-11 defines **how to read services**, not how to register/build them. Registration APIs are container-specific.

5. **Best practices**

- Prefer constructor injection in application code.
- Use direct container lookup mostly in infrastructure/bootstrap layers.
- Avoid Service Locator anti-pattern in domain/business logic.
- Type-hint interfaces instead of concrete implementations whenever possible.

PSR-11 is a minimal but important standard that makes dependency container usage consistent across the PHP ecosystem.

</details>

<details>
<summary>24. What is PSR-15 (middleware)?</summary>

#### PHP

PSR-15 is the standard that defines HTTP server-side middleware and request handlers in PHP. It works together with PSR-7 request/response message interfaces.

1. **Core PSR-15 interfaces**

- `Psr\Http\Server\MiddlewareInterface`
- `Psr\Http\Server\RequestHandlerInterface`

Method contracts:
- Middleware: `process(ServerRequestInterface $request, RequestHandlerInterface $handler): ResponseInterface`
- Handler: `handle(ServerRequestInterface $request): ResponseInterface`

2. **How middleware pipeline works**

- Request enters middleware chain.
- Each middleware can:
  validate/modify request, short-circuit with response, or pass request forward.
- Final handler generates response.
- Response can be modified on the way back through middleware stack.

3. **Typical middleware responsibilities**

- Authentication/authorization
- CORS
- Logging/tracing
- Rate limiting
- Request validation
- Exception-to-response conversion

4. **Simple middleware example**

```php
use Psr\Http\Message\ResponseInterface;
use Psr\Http\Message\ServerRequestInterface;
use Psr\Http\Server\MiddlewareInterface;
use Psr\Http\Server\RequestHandlerInterface;

final class AuthMiddleware implements MiddlewareInterface
{
    public function process(ServerRequestInterface $request, RequestHandlerInterface $handler): ResponseInterface
    {
        // check auth, then continue
        return $handler->handle($request);
    }
}
```

5. **Why PSR-15 matters**

- Makes middleware reusable across frameworks/ecosystems.
- Standardizes request lifecycle extension points.
- Encourages clean cross-cutting concern separation.

PSR-15 provides the interoperability contract for middleware-based HTTP pipelines in modern PHP applications.

</details>

<details>
<summary>25. What is PSR-18 (HTTP client)?</summary>

#### PHP

PSR-18 is the standard interface for HTTP clients in PHP. It defines how application code sends outbound HTTP requests in an implementation-agnostic way.

1. **Core PSR-18 contract**

- Main interface: `Psr\Http\Client\ClientInterface`
- Main method: `sendRequest(RequestInterface $request): ResponseInterface`
- Works with PSR-7 request/response objects.

2. **What problem it solves**

- Decouples business logic from specific HTTP client libraries.
- Makes integrations portable and easier to test.
- Enables swapping client implementations without rewriting service code.

3. **Basic usage**

```php
use Psr\Http\Client\ClientInterface;
use Psr\Http\Message\RequestFactoryInterface;

final class GitHubApi
{
    public function __construct(
        private ClientInterface $client,
        private RequestFactoryInterface $requests,
    ) {}

    public function getUser(string $login): string
    {
        $request = $this->requests->createRequest('GET', "https://api.github.com/users/{$login}");
        $response = $this->client->sendRequest($request);

        return (string) $response->getBody();
    }
}
```

4. **Exceptions**

PSR-18 defines standard exception interfaces for client failures (request errors, network/transport errors), allowing consistent error handling across implementations.

5. **Best practices**

- Type-hint `ClientInterface` in services.
- Build requests through PSR-17 factories.
- Configure timeouts/retries/circuit-breakers in infrastructure layer.
- Mock the client interface in tests for deterministic behavior.

PSR-18 standardizes outbound HTTP communication and is a key piece of interoperable, maintainable integration code in modern PHP apps.

</details>

<details>
<summary>26. What is dependency injection and inversion of control?</summary>

#### PHP

Dependency Injection (DI) and Inversion of Control (IoC) are architectural principles for building loosely coupled, testable code.

1. **Inversion of Control (IoC)**

IoC means a class does not create and control its dependencies directly; that control is moved outside (to framework/container/bootstrap layer).

2. **Dependency Injection (DI)**

DI is a concrete way to implement IoC: dependencies are provided (injected) from outside instead of created with `new` inside the class.

3. **Why it matters**

- Reduces coupling between components.
- Improves testability (easy mocking/stubbing).
- Makes code easier to extend and refactor.
- Supports clean architecture boundaries.

4. **Without DI (tightly coupled)**

```php
final class OrderService
{
    private Mailer $mailer;

    public function __construct()
    {
        $this->mailer = new Mailer();
    }
}
```

5. **With DI (loosely coupled)**

```php
interface MailerInterface
{
    public function send(string $to, string $message): void;
}

final class OrderService
{
    public function __construct(private MailerInterface $mailer) {}
}
```

6. **Common DI styles**

- Constructor injection (preferred).
- Method injection.
- Setter/property injection (less preferred for required dependencies).

7. **Relation to containers**

A DI container automates object construction and wiring, but DI is a design principle independent of any specific container.

DI + IoC are foundational for modern PHP frameworks and are key to maintainable, scalable codebases.

</details>

<details>
<summary>27. What are service containers and how do they work?</summary>

#### PHP

A service container (DI container) is a component that manages object creation, dependency wiring, and lifecycle in an application.

1. **What a container does**

- Stores service definitions/bindings.
- Resolves dependencies automatically (often via reflection and type hints).
- Builds object graphs (service + all nested dependencies).
- Manages lifetimes (singleton/scoped/transient depending on framework).

2. **Why it is useful**

- Centralizes dependency configuration.
- Removes repetitive manual `new ...` wiring.
- Simplifies swapping implementations (interface -> concrete class).
- Improves maintainability in large applications.

3. **Typical flow**

- You register bindings:
  `LoggerInterface` -> `MonologLogger`
- You ask container for a service:
  `OrderService`
- Container builds `OrderService`, resolving required constructor arguments recursively.

4. **Conceptual example**

```php
$container->set(LoggerInterface::class, MonologLogger::class);
$container->set(OrderService::class, fn($c) => new OrderService($c->get(LoggerInterface::class)));

$service = $container->get(OrderService::class);
```

5. **Service lifetime concepts**

- **Singleton/shared:** one instance reused.
- **Transient/factory:** new instance each resolution.
- **Scoped/request:** one instance per request scope (framework-dependent).

6. **Best practices**

- Register abstractions (interfaces), not concrete classes, where possible.
- Keep business/domain code container-agnostic.
- Use constructor injection as default.
- Avoid calling container directly deep inside domain logic (Service Locator anti-pattern).

Service containers are infrastructure tools that automate dependency management and keep modern PHP applications modular and composable.

</details>

<details>
<summary>28. What is middleware and request lifecycle in frameworks?</summary>

#### PHP

In modern PHP frameworks, middleware are layers that process HTTP requests and responses around your core route/controller logic. The request lifecycle is the full path from incoming request to final response.

1. **What middleware is**

- A pipeline component that can:
  inspect/modify request, stop processing with its own response, or pass control to next layer.
- Often implemented via PSR-15 style contracts in modern ecosystems.

2. **Typical middleware responsibilities**

- Authentication and authorization
- CORS
- Rate limiting
- Input normalization/validation
- Logging, tracing, metrics
- Exception handling and response shaping

3. **Typical request lifecycle**

1. HTTP request reaches web server (Nginx/Apache) and PHP runtime.
2. Framework bootstrap loads configuration, services, and routes.
3. Global middleware pipeline starts.
4. Route is matched and route-specific middleware runs.
5. Controller/handler executes business logic.
6. Response is returned through middleware stack (post-processing).
7. Final response is sent to client.

4. **Why this model is useful**

- Separates cross-cutting concerns from controllers.
- Keeps route handlers focused on business logic.
- Makes behavior composable and reusable.
- Provides consistent extension points for platform-level policies.

5. **Practical guidance**

- Keep middleware focused on one responsibility.
- Order middleware intentionally (for example, error handling outermost).
- Avoid heavy business logic in middleware.
- Prefer stateless middleware when possible.

Middleware + request lifecycle are core architectural concepts behind clean, predictable HTTP processing in PHP frameworks.

</details>

<details>
<summary>29. What is MVC and how is it implemented in PHP frameworks?</summary>

#### PHP

MVC (Model-View-Controller) is an architectural pattern that separates application concerns into data/business layer, UI rendering, and request orchestration.

1. **MVC components**

- **Model** - domain/data logic, rules, and persistence interaction.
- **View** - presentation layer (templates/HTML/JSON formatting).
- **Controller** - receives request, coordinates use cases, returns response.

2. **How it works in PHP frameworks**

Typical flow:
1. Router matches URL to controller action.
2. Controller validates input and calls domain/service/model layer.
3. Model/service retrieves or mutates data.
4. Controller passes result to view/template or returns API response.
5. Framework emits final HTTP response.

3. **Example responsibilities**

- Controller: `UserController@show($id)`
- Model/Service: fetch user, apply business rules
- View: render `user/show.blade.php` (or JSON resource)

4. **Why MVC is useful**

- Clear separation of concerns.
- Easier maintenance and testing.
- Better team collaboration (frontend/backend concerns separated).
- Predictable project structure.

5. **Common pitfalls**

- Fat controllers with business logic.
- Fat models mixing too many responsibilities.
- Tight coupling between controllers and persistence details.

6. **Modern practice in PHP**

Many projects use MVC as a base but move business logic to service/use-case layers, keeping controllers thin and views simple.

MVC remains a practical foundation in frameworks like Laravel and Symfony-style applications, especially when combined with clean layering principles.

</details>

<details>
<summary>30. What is hexagonal / clean architecture in PHP?</summary>

#### PHP

Hexagonal (Ports and Adapters) and Clean Architecture are approaches that keep business logic independent from frameworks, databases, and external services.

1. **Core idea**

- Business rules are placed in the center (domain/use cases).
- External systems are treated as replaceable adapters.
- Dependencies point inward: infrastructure depends on domain, not vice versa.

2. **Main building blocks**

- **Domain layer**: entities, value objects, domain rules.
- **Application/use-case layer**: orchestrates business scenarios.
- **Ports (interfaces)**: contracts for needed capabilities (repositories, gateways, buses).
- **Adapters**: concrete implementations (MySQL repository, HTTP client, queue publisher).
- **Delivery layer**: HTTP controllers/CLI/consumers that call use cases.

3. **Why this matters**

- Framework or DB can be changed with minimal impact on core business logic.
- Use cases are easier to test in isolation.
- Clear boundaries reduce coupling and long-term maintenance risk.

4. **PHP-oriented example**

- `CreateOrderUseCase` depends on `OrderRepositoryInterface` and `PaymentGatewayInterface`.
- Laravel/Symfony controller invokes the use case.
- MySQL repository and Stripe adapter implement interfaces in infrastructure layer.

5. **Folder structure (conceptual)**

- `src/Domain/...`
- `src/Application/...`
- `src/Infrastructure/...`
- `src/Interface/Http/...` (or `Presentation/...`)

6. **Practical guidelines**

- Keep framework classes out of domain layer.
- Express boundaries via interfaces at application/domain edge.
- Map framework request/response DTOs at boundaries, not inside domain.
- Start simple and introduce layers where complexity justifies them.

Hexagonal/Clean architecture helps PHP systems stay adaptable, testable, and stable as product and infrastructure evolve.

</details>

<details>
<summary>31. What is the Repository pattern?</summary>

#### PHP

Repository is a pattern that abstracts data access behind a domain-oriented interface, so business logic works with collections/aggregates rather than SQL/ORM details directly.

1. **Core idea**

- Domain/application layers depend on repository interfaces.
- Infrastructure layer provides concrete implementations (PDO/Doctrine/Eloquent/API).
- Persistence concerns stay outside use-case logic.

2. **What Repository typically provides**

- Retrieve entities/aggregates (`findById`, `findByCriteria`).
- Persist changes (`save`, `remove`).
- Query operations expressed in domain terms.

3. **Example interface**

```php
interface OrderRepositoryInterface
{
    public function getById(string $id): ?Order;
    public function save(Order $order): void;
}
```

4. **Why it is useful**

- Decouples business logic from storage technology.
- Improves testability (easy in-memory/mock implementations).
- Supports architecture boundaries (hexagonal/clean).
- Makes migrations/refactors safer when persistence changes.

5. **Common mistakes**

- Turning repository into generic CRUD dump without domain intent.
- Duplicating all ORM methods one-to-one unnecessarily.
- Putting business logic into repository implementation.

6. **Practical guidance**

- Keep repository interfaces in domain/application boundary.
- Expose methods meaningful to use cases, not DB internals.
- Use specifications/query objects for complex filtering when needed.
- Let repositories handle persistence; keep orchestration in services/use cases.

Repository pattern is most valuable in medium/large PHP systems where domain logic longevity matters more than short-term CRUD speed.

</details>

<details>
<summary>32. What are DTOs and Value Objects?</summary>

#### PHP

DTOs and Value Objects are different patterns often used together in modern PHP architecture.

1. **DTO (Data Transfer Object)**

- A simple object used to transfer structured data between layers/processes.
- Usually contains fields and minimal/no business logic.
- Helps avoid passing raw arrays across boundaries.

```php
final class CreateUserDto
{
    public function __construct(
        public string $email,
        public string $name,
    ) {}
}
```

2. **Value Object (VO)**

- A domain object defined by its value, not identity.
- Usually immutable and self-validating.
- Encapsulates domain rules for a specific concept (Email, Money, Currency, etc.).

```php
final class Email
{
    public function __construct(public readonly string $value)
    {
        if (!filter_var($value, FILTER_VALIDATE_EMAIL)) {
            throw new InvalidArgumentException('Invalid email');
        }
    }
}
```

3. **Key differences**

- **Purpose**: DTO transports data; VO models domain meaning.
- **Logic**: DTO minimal; VO can enforce invariants.
- **Identity**: DTO often incidental; VO compared by value.
- **Mutability**: DTO may be mutable/immutable; VO should generally be immutable.

4. **When to use each**

- Use DTOs at boundaries (HTTP request/response, messaging, application layer input/output).
- Use Value Objects inside domain model to express validated concepts safely.

DTOs improve data flow clarity, while Value Objects improve domain correctness and prevent invalid states.

</details>

<details>
<summary>33. What is OOP in PHP?</summary>

#### PHP

OOP (Object-Oriented Programming) in PHP is a programming paradigm where code is organized around objects that combine data (state) and behavior (methods).

1. **Core OOP concepts**

- **Class**: blueprint defining properties and methods.
- **Object**: instance of a class.
- **Encapsulation**: controls access to internals (`public/protected/private`).
- **Inheritance**: child classes reuse/extend parent behavior.
- **Polymorphism**: common interfaces with interchangeable implementations.
- **Abstraction**: expose essential contracts, hide implementation details.

2. **Why OOP is used in PHP**

- Models domain concepts clearly.
- Encourages modular, reusable code.
- Improves maintainability in medium/large codebases.
- Works naturally with DI, interfaces, and framework architecture.

3. **Basic example**

```php
interface NotifierInterface
{
    public function send(string $message): void;
}

final class EmailNotifier implements NotifierInterface
{
    public function send(string $message): void
    {
        // send email
    }
}

final class AlertService
{
    public function __construct(private NotifierInterface $notifier) {}

    public function alert(string $message): void
    {
        $this->notifier->send($message);
    }
}
```

4. **Modern PHP OOP features**

- Typed properties and strict types
- Interfaces and abstract classes
- Traits for horizontal code reuse
- Attributes, enums, readonly properties/classes
- Constructor property promotion

5. **Best practices**

- Prefer composition over inheritance when possible.
- Program to interfaces, not concrete classes.
- Keep classes focused (single responsibility).
- Avoid “god objects” with too many responsibilities.

OOP in PHP is the foundation for most modern framework and domain-driven application design.

</details>

<details>
<summary>34. What is the difference between interface and abstract class?</summary>

#### PHP

Both interfaces and abstract classes define contracts, but they serve different design purposes.

1. **Interface**

- Defines only method signatures (contract) and constants.
- No instance state (no properties with runtime state).
- A class can implement multiple interfaces.
- Focus: capability contract and polymorphism.

```php
interface PaymentGatewayInterface
{
    public function charge(int $amount): bool;
}
```

2. **Abstract class**

- Can contain both abstract methods and implemented methods.
- Can have shared state/behavior (properties, protected helpers, constructor logic).
- A class can extend only one abstract/base class.
- Focus: partial implementation + common base behavior.

```php
abstract class BaseGateway
{
    public function __construct(protected string $apiKey) {}

    abstract public function charge(int $amount): bool;

    protected function log(string $message): void
    {
        // shared logic
    }
}
```

3. **Key differences**

- **Multiple inheritance of type**: many interfaces, only one parent class.
- **Shared code**: abstract class yes, interface no.
- **Coupling**: interface is usually looser; abstract class introduces inheritance coupling.

4. **When to choose**

- Use **interface** when you need interchangeable implementations and clear contracts.
- Use **abstract class** when implementations share meaningful base logic/state.

5. **Practical rule**

Prefer interfaces for public architecture boundaries; use abstract classes as internal reuse tools where inheritance is justified.

Interface = “what it can do”, abstract class = “what it is partly implemented as”.

</details>

<details>
<summary>35. What are traits and when should they be used?</summary>

#### PHP

Traits in PHP are a mechanism for horizontal code reuse: they let classes reuse methods (and related members) without inheritance.

1. **What a trait is**

- A reusable code unit declared with `trait`.
- Included into classes via `use`.
- Helps share behavior across unrelated class hierarchies.

```php
trait Timestampable
{
    public function touch(): void
    {
        $this->updatedAt = new DateTimeImmutable();
    }
}

final class Post
{
    use Timestampable;
}
```

2. **When traits are useful**

- Shared cross-cutting behavior (logging helpers, timestamps, small utility behaviors).
- Reuse across classes that cannot share a common parent class.
- Reducing duplication when composition would be overly verbose for tiny behavior blocks.

3. **Trait conflict resolution**

If two traits define the same method, PHP provides conflict resolution:
- `insteadof` to choose one implementation.
- `as` to alias/rename methods.

4. **Limitations and risks**

- Traits can hide coupling and blur class responsibilities if overused.
- Large “god traits” become hard to test and maintain.
- They are code inclusion, not true polymorphic contracts.

5. **Best practices**

- Keep traits small and focused.
- Use traits for behavior reuse, not for domain modeling.
- Prefer interfaces + composition for core architecture boundaries.
- Avoid storing complex mutable shared state inside traits.

Traits are a practical PHP tool for targeted reuse, but they work best as a lightweight supplement to good object design, not a replacement for it.

</details>

<details>
<summary>36. What are magic methods and when are they triggered?</summary>

#### PHP

Magic methods are special PHP methods (prefixed with `__`) that are automatically triggered by the engine on specific object lifecycle or interaction events.

1. **Object lifecycle magic methods**

- `__construct()` - called when object is created.
- `__destruct()` - called when object is destroyed (or script ends).
- `__clone()` - called after object cloning.

2. **Property access magic methods**

- `__get($name)` - reading inaccessible/undefined property.
- `__set($name, $value)` - writing inaccessible/undefined property.
- `__isset($name)` - `isset()`/`empty()` on inaccessible/undefined property.
- `__unset($name)` - `unset()` on inaccessible/undefined property.

3. **Method call interception**

- `__call($name, $arguments)` - calling inaccessible/undefined instance method.
- `__callStatic($name, $arguments)` - calling inaccessible/undefined static method.

4. **String/invocation/serialization**

- `__toString()` - object used as string.
- `__invoke(...$args)` - object used like a function.
- `__serialize()` / `__unserialize()` - custom serialization logic.

5. **State export/debug helpers**

- `__set_state(array $properties)` - called by `var_export()` recreation.
- `__debugInfo()` - custom output for `var_dump()`.

6. **Simple example**

```php
final class User
{
    private array $data = [];

    public function __get(string $name): mixed
    {
        return $this->data[$name] ?? null;
    }

    public function __set(string $name, mixed $value): void
    {
        $this->data[$name] = $value;
    }
}
```

7. **Best practices**

- Use magic methods intentionally, not as default architecture.
- Keep behavior explicit and predictable.
- Avoid hiding errors with overly permissive `__get/__set`.
- Prefer typed properties/methods where possible.

Magic methods are powerful extension points, but they should be used carefully because they can reduce clarity if overused.

</details>

<details>
<summary>37. What is late static binding?</summary>

#### PHP

Late Static Binding (LSB) in PHP allows static method/property resolution based on the class that is called at runtime, not just the class where the method is defined.

1. **`self::` vs `static::`**

- `self::` is bound to the class where the method is declared (early binding).
- `static::` is resolved to the called class at runtime (late static binding).

2. **Why it matters**

- Enables polymorphic behavior in static context.
- Useful in inheritance hierarchies where child classes should control returned class/values.
- Common in factory patterns and Active Record-style APIs.

3. **Example**

```php
class BaseModel
{
    public static function table(): string
    {
        return static::TABLE; // late static binding
    }
}

class User extends BaseModel
{
    protected const TABLE = 'users';
}

class Order extends BaseModel
{
    protected const TABLE = 'orders';
}

echo User::table();  // users
echo Order::table(); // orders
```

If `self::TABLE` were used, behavior would be fixed to the base declaration context.

4. **Related keyword**

- `static` return type (`public static function make(): static`) also uses late static semantics and returns the called class type.

5. **Practical guidance**

- Use `static::` when subclasses must customize static behavior.
- Use `self::` when behavior should intentionally remain fixed to base class implementation.

Late static binding is an important OOP feature for extensible class hierarchies in PHP.

</details>

<details>
<summary>38. How are objects handled in memory in PHP?</summary>

#### PHP

In PHP, objects are managed by the Zend Engine as heap-allocated structures referenced by object handles, with automatic memory management through reference counting and garbage collection.

1. **Object storage model**

- Object instances are allocated in engine-managed memory (heap).
- Variables hold references (handles) to object entries, not full object copies.
- Assigning one object variable to another copies the handle, not the object state.

```php
$a = new stdClass();
$a->x = 1;

$b = $a;      // same object reference
$b->x = 2;

echo $a->x;   // 2
```

2. **Reference counting**

- Engine tracks how many zvals reference a value/object.
- When count drops to zero, memory can be freed.
- For objects, this typically means destructor invocation and object cleanup.

3. **Garbage collector (GC)**

- Reference counting alone cannot collect cyclic references.
- PHP GC detects and cleans cyclic garbage (for example, object graphs referencing each other).

4. **Cloning behavior**

- `clone` creates a new object instance (separate identity).
- `__clone()` can customize post-clone state logic.

5. **Pass-by-reference nuance**

- Passing objects to functions is effectively by handle (object changes are visible outside).
- You usually do not need `&` to mutate object state across function boundaries.

6. **Performance/memory implications**

- Large object graphs increase memory pressure.
- Long-lived references (static caches, closures, global containers) can delay cleanup.
- Circular references in long-running workers should be monitored to avoid leaks-like growth.

7. **Practical guidance**

- Keep object graphs intentional and bounded.
- Explicitly unset large temporary structures in long-running processes when needed.
- Use profiling tools to inspect memory hotspots.
- Be careful with static singletons/global state in workers/daemons.

PHP object memory handling is efficient for typical request lifecycles, but long-running processes require deliberate memory discipline.

</details>

<details>
<summary>39. What is PDO and why is it preferred?</summary>

#### PHP

PDO (PHP Data Objects) is a database access abstraction layer in PHP that provides a consistent API for working with multiple database engines.

1. **What PDO provides**

- Unified interface for DB operations (`MySQL`, `PostgreSQL`, `SQLite`, etc.).
- Prepared statements and parameter binding.
- Transaction support.
- Configurable fetch modes and error handling.

2. **Why PDO is preferred**

- **Portability:** same coding style across different databases.
- **Security:** prepared statements reduce SQL injection risk.
- **Maintainability:** cleaner, standardized DB access code.
- **Control:** explicit transaction/error behavior.

3. **Basic example**

```php
$pdo = new PDO(
    'mysql:host=localhost;dbname=app;charset=utf8mb4',
    'user',
    'pass',
    [
        PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
        PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
    ]
);

$stmt = $pdo->prepare('SELECT id, email FROM users WHERE id = :id');
$stmt->execute(['id' => 42]);
$user = $stmt->fetch();
```

4. **PDO vs direct driver-specific APIs**

- PDO gives a common abstraction and cleaner architecture boundaries.
- Driver-specific APIs may expose niche features, but reduce portability.

5. **Best practices**

- Always enable exception mode (`PDO::ERRMODE_EXCEPTION`).
- Use prepared statements for all external input.
- Set explicit charset in DSN (for example, `utf8mb4`).
- Handle transactions explicitly for multi-step writes.

PDO is preferred in modern PHP because it combines security, portability, and clear database access patterns.

</details>

<details>
<summary>40. What are prepared statements and parameter binding?</summary>

#### PHP

Prepared statements are SQL queries compiled as templates with placeholders, where values are supplied separately via parameter binding.

1. **How they work**

- Step 1: prepare SQL with placeholders (`:email`, `?`).
- Step 2: bind/execute values separately.
- Database treats bound values strictly as data, not SQL syntax.

2. **Why they are important**

- Primary defense against SQL injection.
- Cleaner and safer query code.
- Better handling of data types and escaping by driver.
- Can improve performance for repeated query execution (DB/driver dependent).

3. **Named placeholder example (PDO)**

```php
$stmt = $pdo->prepare(
    'SELECT id, email FROM users WHERE email = :email AND status = :status'
);

$stmt->execute([
    'email' => $email,
    'status' => $status,
]);
```

4. **Positional placeholder example**

```php
$stmt = $pdo->prepare('SELECT * FROM users WHERE id = ?');
$stmt->execute([$id]);
```

5. **Binding with explicit types**

```php
$stmt = $pdo->prepare('SELECT * FROM users WHERE id = :id');
$stmt->bindValue(':id', $id, PDO::PARAM_INT);
$stmt->execute();
```

6. **Important nuance**

- Prepared statements protect values, not SQL identifiers (table/column names).
- Dynamic identifiers must be controlled by strict allowlists.

7. **Best practices**

- Use prepared statements for every query that includes external input.
- Avoid string concatenation for SQL conditions.
- Keep SQL templates readable and explicit.
- Combine with least-privileged DB users and transaction boundaries.

Prepared statements + parameter binding are the standard, non-optional baseline for secure DB access in PHP.

</details>

<details>
<summary>41. How do transactions work in PHP?</summary>

#### PHP

Transactions in PHP (via PDO/MySQLi) group multiple database operations into a single atomic unit: either all changes are committed, or all are rolled back.

1. **Core transaction operations**

- `beginTransaction()` - starts transaction.
- `commit()` - permanently saves all changes.
- `rollBack()` - cancels all uncommitted changes.

2. **Why transactions are needed**

- Ensure data consistency across multi-step writes.
- Prevent partial updates when an error occurs.
- Preserve business invariants (for example, debit and credit must both succeed).

3. **Basic PDO example**

```php
try {
    $pdo->beginTransaction();

    $stmt1 = $pdo->prepare('UPDATE accounts SET balance = balance - :amount WHERE id = :from');
    $stmt1->execute(['amount' => 100, 'from' => 1]);

    $stmt2 = $pdo->prepare('UPDATE accounts SET balance = balance + :amount WHERE id = :to');
    $stmt2->execute(['amount' => 100, 'to' => 2]);

    $pdo->commit();
} catch (Throwable $e) {
    if ($pdo->inTransaction()) {
        $pdo->rollBack();
    }
    throw $e;
}
```

4. **Isolation and concurrency**

- DB isolation level controls visibility/locking behavior between concurrent transactions.
- Common anomalies: dirty reads, non-repeatable reads, phantom reads.
- Choose isolation level based on consistency/performance trade-offs.

5. **Practical pitfalls**

- Long transactions hold locks and hurt concurrency.
- External API/network calls inside DB transaction increase failure window.
- Forgetting rollback on exceptions can leave workflow inconsistent.

6. **Best practices**

- Keep transactions as short as possible.
- Include only DB operations that must be atomic.
- Use explicit error handling and rollback guarantees.
- Design retry logic for deadlocks/serialization conflicts where needed.

Transactions are a core reliability mechanism for financial, inventory, and other integrity-critical workflows in PHP systems.

</details>

<details>
<summary>42. What is ORM (Eloquent / Doctrine) and trade-offs?</summary>

#### PHP

ORM (Object-Relational Mapping) is a technique that maps database tables/rows to PHP objects, allowing you to work with domain entities instead of raw SQL in most application code.

1. **What ORM gives you**

- Entity/model classes mapped to DB schemas.
- Query APIs/builders instead of manual SQL for common operations.
- Relationship handling (`hasMany`, `belongsTo`, etc.).
- Unit-of-work/change tracking (especially in Doctrine).
- Migrations/ecosystem tooling in many frameworks.

2. **Common PHP ORMs**

- **Eloquent (Laravel)**:
  Active Record style, quick productivity, expressive syntax.
- **Doctrine ORM**:
  Data Mapper style, rich domain modeling, stronger separation of concerns.

3. **Benefits**

- Faster development for CRUD-heavy features.
- Cleaner and more readable persistence code for common scenarios.
- Easier relation traversal and model-centric workflows.
- Convention-based scaffolding and ecosystem integrations.

4. **Trade-offs / drawbacks**

- Abstraction overhead and potential performance cost.
- Hidden/implicit queries (N+1 problem).
- Complex SQL/reporting often still requires manual SQL.
- ORM-specific patterns can increase learning curve and lock-in.

5. **When ORM works best**

- Business applications with frequent entity lifecycle operations.
- Teams that value productivity and maintainable model-centric code.

6. **When to prefer raw SQL/query builders**

- Performance-critical hot paths.
- Complex analytical/report queries.
- DB-vendor-specific features and fine-grained SQL control.

7. **Practical strategy**

- Use ORM by default for common domain operations.
- Profile and optimize bottlenecks.
- Mix ORM with optimized SQL where needed (hybrid approach).
- Be explicit with eager/lazy loading to avoid query explosions.

ORM is a productivity multiplier in PHP, but good engineering requires understanding where abstraction helps and where lower-level SQL control is better.

</details>

<details>
<summary>43. What is connection pooling and why is it important?</summary>

#### PHP

Connection pooling is a technique where database connections are reused from a managed pool instead of being created and closed for every operation.

1. **Why connections are expensive**

- Opening DB connections involves network handshake, authentication, and server resource allocation.
- Frequent reconnects increase latency and CPU load on both app and DB.

2. **What pooling does**

- Maintains a reusable set of open connections.
- Assigns an existing connection to incoming work.
- Returns it to pool after use for reuse by next requests/jobs.

3. **Why it is important**

- Reduces request latency.
- Improves throughput under load.
- Lowers DB connection churn and overhead.
- Stabilizes behavior for high-concurrency systems.

4. **PHP context nuance**

- In classic PHP-FPM request model, each worker process has isolated lifecycle, so pooling is less straightforward than in long-lived runtimes.
- Common practical approaches:
  persistent connections (`PDO::ATTR_PERSISTENT` with caution),
  external poolers/proxies (for example, PgBouncer for PostgreSQL),
  long-running workers (RoadRunner/Swoole/queue consumers) where reuse is more direct.

5. **Trade-offs / risks**

- Stale/broken connections must be detected and recycled.
- Poor pool sizing can cause contention or DB overload.
- Persistent connections can hold server resources longer than expected.

6. **Best practices**

- Set sensible pool/connection limits aligned with DB capacity.
- Use connection health checks/timeouts.
- Monitor connection count, wait time, and error rates.
- Keep queries efficient; pooling is not a fix for slow SQL.

Connection pooling is a key scalability technique for database-heavy PHP systems, especially under sustained concurrent traffic.

</details>

<details>
<summary>44. How do you structure a scalable PHP application?</summary>

#### PHP

A scalable PHP application is structured around clear boundaries, predictable architecture, and operational readiness for growth in traffic, team size, and feature complexity.

1. **Use layered/module boundaries**

- Split by responsibilities and business domains, not only by technical folders.
- Typical layers:
  `Domain`, `Application/UseCases`, `Infrastructure`, `Interface/HTTP`.

2. **Keep business logic framework-agnostic**

- Put core rules in domain/use-case layer.
- Keep controllers thin.
- Depend on interfaces; keep DB/framework adapters in infrastructure layer.

3. **Design for stateless horizontal scale**

- Avoid local mutable state in app instances.
- Store shared state in external systems:
  DB, Redis, object storage, queues.
- Make sessions/cache ready for multi-node deployments.

4. **Data and persistence strategy**

- Use repositories/services for persistence boundaries.
- Apply indexing and query optimization early.
- Introduce caching (application/query/HTTP) where justified.
- Use read/write separation and partitioning only when needed.

5. **Async and background processing**

- Move non-critical/slow tasks to queues (emails, exports, notifications, webhooks).
- Keep request path fast and deterministic.

6. **Operational scalability**

- Containerize workloads (Docker/K8s/managed platforms).
- Use health checks, structured logging, metrics, tracing.
- Add rate limiting, timeouts, retries, circuit breakers.
- Build CI/CD with safe rollout and rollback strategy.

7. **Codebase scalability for teams**

- Enforce coding standards and static analysis.
- Maintain modular package boundaries.
- Use integration and contract tests around critical paths.
- Document architecture decisions (ADRs) and service contracts.

8. **Practical evolution path**

- Start with modular monolith and strong boundaries.
- Extract services only when clear scaling/team constraints justify it.

Scalability in PHP is primarily an architecture + operations discipline, not a single framework choice.

</details>

<details>
<summary>45. How do you handle configuration (env variables)?</summary>

#### PHP

In modern PHP applications, configuration should be externalized from code and provided through environment variables, following 12-factor principles.

1. **Core principle**

- Keep config out of source code.
- Treat environment as the source of deploy-specific settings:
  DB credentials, API URLs, cache hosts, feature flags, etc.

2. **Typical setup**

- Development: `.env` file (loaded by framework/bootstrap).
- Production: real environment variables from platform/orchestrator (not `.env` in repo).

3. **How values are consumed**

- Read env once in config bootstrap.
- Map to typed config structure/object.
- Inject config into services via DI.

4. **Good practices**

- Separate config by environment (`dev`, `staging`, `prod`) using env values.
- Provide defaults only for non-sensitive local development values.
- Validate required config at startup and fail fast if missing/invalid.
- Keep config keys consistent and documented.

5. **What not to do**

- Do not hardcode credentials in code.
- Do not commit production secrets to repository.
- Do not call `getenv()` randomly across domain logic.
- Do not mix business logic with config loading logic.

6. **Practical pattern**

Use central config files that pull from env, for example:
- `config/database.php`
- `config/cache.php`
- `config/app.php`

Then inject resolved config into dependent services.

7. **Security note**

Environment variables are better than hardcoded secrets, but still sensitive:
limit access, avoid logging full values, and combine with dedicated secret managers for critical credentials.

Handling configuration via env variables keeps PHP apps portable, secure, and consistent across environments.

</details>

<details>
<summary>46. How do you manage secrets (Vault, AWS Secrets Manager)?</summary>

#### PHP

Secrets management is the practice of securely storing, rotating, and accessing sensitive values (API keys, DB passwords, tokens, certificates) outside application code.

1. **Why dedicated secret managers are needed**

- Prevent secrets from leaking into repository/history.
- Centralize access control and auditing.
- Enable safe rotation without redeploying code.
- Reduce operational risk versus plain `.env` files.

2. **Common tools**

- **HashiCorp Vault**: dynamic secrets, leases, policy-based access, strong audit capabilities.
- **AWS Secrets Manager**: managed secret storage/rotation integrated with IAM and AWS services.
- (Also common: cloud-native parameter stores or KMS-backed solutions.)

3. **Recommended secret flow**

1. App identity is established (IAM role, workload identity, Vault auth method).
2. App fetches required secrets at startup (or on demand with cache).
3. Secrets are kept in memory only as needed.
4. Rotation events are handled without hardcoded values.

4. **Best practices**

- Never commit secrets to git (including sample files with real values).
- Use least-privilege access policies per service/environment.
- Rotate secrets regularly and on incident triggers.
- Log access metadata, never secret values.
- Separate secrets by environment (`dev/staging/prod`) and service scope.
- Use short-lived credentials when possible (dynamic DB creds/tokens).

5. **PHP integration pattern**

- Fetch secrets in bootstrap/infrastructure layer.
- Map them into typed config objects.
- Inject config/secrets into dependent services via DI.
- Add fallback and retry strategy for secret manager outages.

6. **Operational considerations**

- Cache secrets with TTL to reduce latency and API limits.
- Plan bootstrap behavior when secret backend is temporarily unavailable.
- Test rotation procedure in staging before production rollout.

Using Vault/AWS Secrets Manager turns secret handling from ad-hoc environment variables into a controlled security process suitable for production PHP systems.

</details>

<details>
<summary>47. What is 12-factor app in context of PHP?</summary>

#### PHP

12-factor app is a set of cloud-native engineering principles for building portable, scalable, and maintainable services. In PHP, these principles help move from “server-coupled apps” to modern deployable services.

1. **Codebase**

- One codebase tracked in version control.
- Many deploys (dev/staging/prod) from the same codebase.

2. **Dependencies**

- Declare dependencies explicitly in `composer.json`.
- Avoid relying on globally installed system packages.

3. **Config**

- Store config in environment variables, not in code.
- Keep secrets and environment-specific values outside repository.

4. **Backing services**

- Treat DB, cache, queue, object storage as attached resources.
- Access them via config/URLs, so they can be swapped per environment.

5. **Build, release, run separation**

- Build artifact once.
- Promote same artifact through environments.
- Keep runtime config separate from build.

6. **Processes**

- Run app as stateless processes.
- Store persistent state in external services (DB/Redis/S3/etc.).

7. **Port binding and concurrency**

- Expose services through HTTP/runtime entrypoints.
- Scale out via process/container replication, not vertical-only tuning.

8. **Disposability and parity**

- Fast startup/shutdown for safe deploys and autoscaling.
- Keep dev/staging/prod environments as similar as possible.

9. **Logs and admin tasks**

- Treat logs as event streams (stdout/aggregators).
- Run admin/migration tasks as one-off processes using same codebase.

10. **PHP-specific practical implications**

- Use Composer + env config + externalized state.
- Container-friendly runtime (PHP-FPM/CLI workers).
- Queue workers for background tasks.
- CI/CD pipeline with immutable artifacts.

Applying 12-factor principles in PHP improves deployment reliability, operational scalability, and long-term maintainability.

</details>

<details>
<summary>48. What is containerization (Docker) in PHP apps?</summary>

#### PHP

Containerization packages a PHP application with its runtime dependencies into a portable image, so it runs consistently across local, CI, staging, and production environments.

1. **What Docker gives PHP apps**

- Reproducible runtime (PHP version, extensions, system libs).
- Environment parity between developer machines and production.
- Easier deployment, rollback, and scaling.
- Isolation between services (app, DB, cache, queue, worker).

2. **Typical containerized PHP stack**

- PHP-FPM container (application runtime)
- Nginx/Apache container (web server)
- Separate containers for DB/Redis/queue workers/cron jobs

3. **Basic Dockerfile pattern**

```dockerfile
FROM php:8.4-fpm-alpine

RUN docker-php-ext-install pdo pdo_mysql opcache
WORKDIR /var/www/html

COPY . .
RUN php -v
```

4. **Why it matters for scalability**

- Horizontal scaling becomes simpler (replicate containers).
- Immutable image-based deploys reduce drift/config mismatch.
- Works naturally with orchestration platforms (Kubernetes, ECS, Nomad).

5. **Best practices**

- Use small base images and multi-stage builds.
- Pin image/tag versions for reproducibility.
- Keep images stateless; store persistent data externally.
- Inject config/secrets via env/secret managers, not baked into image.
- Run health checks and expose structured logs to stdout/stderr.

6. **Common pitfalls**

- Running everything in one container (web + DB + queue) for production.
- Writing persistent app data to container filesystem.
- Large images with unnecessary build tools in runtime layer.

Containerization is a core practice for modern PHP operations because it standardizes runtime behavior and improves deployability at scale.

</details>

<details>
<summary>49. What is OPcache and how does it improve performance?</summary>

#### PHP

OPcache is a built-in PHP bytecode cache that stores compiled script bytecode in shared memory, so PHP does not need to parse and compile the same files on every request.

1. **What problem OPcache solves**

- Without OPcache, each request repeatedly does:
  read PHP file -> parse -> compile to opcodes -> execute.
- This repeated compilation adds CPU overhead and latency.

2. **How OPcache improves performance**

- Compiled opcodes are cached in memory and reused across requests.
- Reduces CPU usage and request time.
- Increases throughput under load.
- Improves startup performance for frameworks with many files.

3. **Typical production setup**

- Enable OPcache in PHP runtime (`opcache.enable=1`).
- Tune memory and file count limits:
  `opcache.memory_consumption`, `opcache.max_accelerated_files`.
- Disable timestamp validation for immutable release artifacts:
  `opcache.validate_timestamps=0` (with deploy-triggered cache reset).

4. **Common useful settings**

- `opcache.enable`
- `opcache.memory_consumption`
- `opcache.max_accelerated_files`
- `opcache.interned_strings_buffer`
- `opcache.validate_timestamps`
- `opcache.revalidate_freq`

5. **Deployment considerations**

- When code changes, cached bytecode must refresh.
- In immutable/container deploys, restarting PHP workers is usually enough.
- In mutable deploys, use controlled invalidation/restart strategy.

6. **Best practices**

- Always use OPcache in production.
- Monitor cache hit rate, memory usage, and restarts.
- Size cache according to codebase growth.
- Combine OPcache with application/database caching for full performance gains.

OPcache is one of the highest-impact, low-effort performance features for PHP production environments.

</details>

<details>
<summary>50. What is JIT in PHP and when is it useful?</summary>

#### PHP

JIT (Just-In-Time compilation) in PHP is an engine optimization that compiles selected Zend opcodes into native machine code at runtime.

1. **What JIT does**

- Normal PHP flow: script -> opcodes -> interpreter execution.
- With JIT: hot code paths can be compiled to native code and executed faster.

2. **Where JIT can help**

- CPU-intensive workloads:
  heavy math, loops, data processing, computational algorithms.
- Long-running CLI workers and specialized compute tasks.

3. **Where JIT often gives little benefit**

- Typical web apps dominated by I/O:
  database queries, network calls, cache access, template rendering.
- In many CRUD/API workloads, OPcache and query optimization matter more than JIT.

4. **Relation to OPcache**

- JIT is built on top of OPcache infrastructure.
- OPcache generally gives the biggest baseline gain for most apps.
- JIT is an additional optimization layer for CPU-bound code.

5. **Practical guidance**

- Enable and benchmark before/after on your real workload.
- Do not assume global speedups for all request types.
- Prioritize bottleneck fixes first:
  slow SQL, N+1 queries, excessive network calls, inefficient caching.

6. **Rule of thumb**

- For classic web backends: JIT impact is usually modest.
- For compute-heavy PHP workloads: JIT can provide meaningful improvements.

JIT is a useful optimization tool, but its value depends heavily on workload profile.

</details>

<details>
<summary>51. What is lazy loading and where is it used?</summary>

#### PHP

Lazy loading is a technique where data or objects are loaded only when they are actually needed, instead of loading everything upfront.

1. **Core idea**

- Delay expensive initialization until first access.
- Reduce initial memory usage and startup time.
- Pay cost only for paths that are actually used.

2. **Where lazy loading is used in PHP**

- ORM relations (Doctrine/Eloquent relation proxies).
- Service initialization in DI containers (deferred services).
- Large configuration/resources loaded on demand.
- Stream/file processing where chunks are loaded progressively.

3. **Typical ORM example**

- `User` entity is loaded.
- `User->orders` is not fetched immediately.
- First access to orders triggers SQL query.

4. **Benefits**

- Faster initial response for many use cases.
- Lower memory footprint when not all data is required.
- Better scalability for complex object graphs.

5. **Trade-offs and risks**

- Hidden queries can cause N+1 performance problems.
- Access patterns become less explicit.
- Lazy loading in tight loops can explode DB round-trips.

6. **Best practices**

- Use eager loading when you know related data is needed.
- Profile query count and latency.
- Keep lazy boundaries explicit in repository/query layer.
- Avoid lazy-loading inside serialization/output loops.

7. **Rule of thumb**

- Use lazy loading for optional or rarely-used dependencies/data.
- Use eager loading for predictable, frequently-accessed related data.

Lazy loading is powerful for performance optimization, but only when paired with visibility into query behavior and deliberate loading strategy.

</details>

<details>
<summary>52. What are common PHP performance bottlenecks?</summary>

#### PHP

Most PHP performance issues are not caused by the language itself, but by inefficient I/O, query patterns, and architecture decisions.

1. **Database bottlenecks (most common)**

- N+1 queries in ORM usage.
- Missing indexes or poor query plans.
- Over-fetching data (`SELECT *` when not needed).
- Long transactions and lock contention.

2. **Network and external I/O**

- Slow third-party APIs without timeouts/retries.
- Too many synchronous outbound calls in request path.
- Lack of circuit breakers/fallbacks.

3. **Application-level inefficiencies**

- Heavy business logic executed on every request.
- Recomputing expensive results instead of caching.
- Excessive serialization/deserialization or large payload processing.

4. **Autoload/bootstrap overhead**

- Large framework bootstraps for trivial endpoints.
- Too many loaded classes/config providers.
- Misconfigured OPcache.

5. **Filesystem and logging overhead**

- Frequent disk writes in request path.
- Blocking/verbose logging without async processing.
- Slow storage volumes in containers/VMs.

6. **Memory pressure**

- Large in-memory collections and unbounded arrays.
- Inefficient loops over huge datasets.
- Long-lived workers retaining references unintentionally.

7. **Missing/ineffective caching**

- No caching for read-heavy data.
- Wrong cache invalidation strategy causing stale/frequent misses.
- Cache stampede under load.

8. **How to address systematically**

- Profile before optimizing.
- Prioritize hottest endpoints/queries first.
- Add query optimization + caching + async offloading.
- Monitor p95/p99 latency, DB time, cache hit ratio, and error rates.

In PHP systems, the fastest wins usually come from query tuning, caching strategy, and reducing synchronous I/O in the request path.

</details>

<details>
<summary>53. How do you profile a PHP application?</summary>

#### PHP

Profiling is the process of measuring where execution time, CPU, memory, and I/O are actually spent, so optimization is based on evidence instead of guesses.

1. **What to measure first**

- Request latency (p50/p95/p99)
- Database time and query count
- External API call duration
- Memory usage and peak usage
- Hot functions/code paths

2. **Common PHP profiling tools**

- **Blackfire** - production-friendly profiling and performance recommendations.
- **Xdebug (profiler mode)** - detailed traces/callgrind for local analysis.
- **Tideways/XHProf family** - function-level profiling with low overhead options.
- **APM tools** (Datadog/New Relic/etc.) for distributed request visibility.

3. **Practical profiling workflow**

1. Reproduce slow endpoint/job with realistic data.
2. Capture profile trace.
3. Identify top contributors (DB, external I/O, CPU-heavy functions).
4. Optimize one bottleneck at a time.
5. Re-profile and compare metrics.

4. **What usually appears as hotspots**

- N+1 ORM queries
- Missing indexes / expensive SQL scans
- Repeated serialization and large payload processing
- Synchronous network calls in request path
- Excessive framework/bootstrap overhead

5. **Memory profiling focus**

- Large arrays/collections loaded at once
- Long-lived references in workers
- Unnecessary object graphs and duplicated data

6. **Best practices**

- Profile in environments close to production behavior.
- Benchmark before and after every optimization.
- Track regressions in CI/CD with performance budgets for critical endpoints.
- Combine code profiling with DB profiling (`EXPLAIN`, slow query logs).

Profiling turns performance tuning into a measurable engineering process and is the most reliable way to improve PHP application speed safely.

</details>

<details>
<summary>54. How does caching work (Redis, Memcached)?</summary>

#### PHP

Caching stores precomputed or frequently requested data in fast storage (usually memory) to avoid repeated expensive operations like DB queries or heavy computations.

1. **How caching works (basic flow)**

1. App receives request for data.
2. Check cache by key.
3. If hit: return cached value quickly.
4. If miss: load from source (DB/API), store in cache with TTL, return value.

2. **Common cache backends**

- **Redis**:
  in-memory data store with rich data structures, persistence options, pub/sub, distributed features.
- **Memcached**:
  simple distributed in-memory key-value cache, focused on high-speed ephemeral caching.

3. **Typical PHP cache use cases**

- Query result caching
- Session storage
- Response/fragment caching
- Rate limiting counters
- Locks and idempotency keys
- Computed/config reference data

4. **Important cache design concepts**

- **Key strategy**: predictable namespacing and versioning (`user:42:v2`).
- **TTL**: choose expiration based on data volatility.
- **Invalidation**: explicit invalidation on writes when freshness matters.
- **Consistency model**: accept eventual consistency where appropriate.

5. **Common pitfalls**

- Cache stampede (many concurrent misses).
- Stale data due to weak invalidation strategy.
- Oversized values and poor key design.
- Treating cache as source of truth.

6. **Best practices**

- Cache only expensive/high-frequency reads.
- Use short, sensible TTLs and jitter to reduce synchronized expiry.
- Add stampede protection (locks, request coalescing, stale-while-revalidate).
- Monitor hit rate, latency, eviction, and memory usage.
- Keep DB as source of truth; cache is acceleration layer.

Redis/Memcached caching is one of the most effective ways to reduce latency and database load in PHP production systems.

</details>

<details>
<summary>55. What is asynchronous processing in PHP?</summary>

#### PHP

Asynchronous processing means moving slow or non-critical tasks out of the synchronous HTTP request flow, so users get fast responses while background work is executed separately.

1. **Why async is needed**

- Request-response cycles should stay short.
- Some operations are expensive:
  emails, file processing, report generation, external API calls.
- Doing all of that inline increases latency and failure impact.

2. **How it works in PHP systems**

1. Main app receives request.
2. Critical state is saved quickly.
3. Background job/event is pushed to queue.
4. Worker process consumes and executes task asynchronously.

3. **Typical async workloads**

- Email/SMS/push notifications
- Media processing (images/video/PDF)
- Data imports/exports
- Webhook delivery/retries
- Search index updates
- Analytics/event processing

4. **Benefits**

- Lower user-facing latency.
- Better resilience (retries, dead-letter queues).
- Improved throughput by decoupling heavy jobs.
- Cleaner separation of online vs offline work.

5. **Trade-offs**

- Added operational complexity (queues/workers/monitoring).
- Eventual consistency between write and side effects.
- Need for idempotency and retry-safe handlers.

6. **Best practices**

- Keep job payloads minimal (IDs, not full objects).
- Make handlers idempotent.
- Configure retry/backoff and dead-letter handling.
- Monitor queue depth, worker lag, and failure rate.
- Define which tasks are sync-critical vs async-deferred.

In PHP architecture, asynchronous processing is a key technique for scaling user experience and reliability under real production load.

</details>

<details>
<summary>56. What are queues (RabbitMQ, Kafka, Redis queues)?</summary>

#### PHP

Queues are messaging mechanisms used to decouple producers and consumers, enabling asynchronous processing, buffering, and reliable background execution.

1. **Core queue concept**

- Producer publishes a message/job.
- Broker stores it temporarily.
- Consumer/worker processes it later.
- This removes heavy work from synchronous request flow.

2. **Why queues are important**

- Smooth traffic spikes (buffering).
- Improve response time (offload background tasks).
- Increase reliability with retries and dead-letter handling.
- Decouple services and components.

3. **Common queue technologies in PHP**

- **RabbitMQ**:
  traditional message broker, strong routing patterns, acknowledgements, retries.
- **Kafka**:
  distributed event log, high-throughput stream processing, replayable messages.
- **Redis-based queues** (for example, Laravel queues):
  simple and fast for many app-level background jobs.

4. **Typical PHP queue use cases**

- Email/SMS/push dispatch
- Webhook delivery
- File/image/video processing
- Search indexing
- Report generation
- Integration/event fan-out

5. **Reliability concepts**

- **Ack/Nack**: confirm success or request retry.
- **Retry policy**: exponential backoff, max attempts.
- **Dead-letter queue (DLQ)**: isolate poison/failing messages.
- **Idempotency**: safe reprocessing without duplicate side effects.

6. **Best practices**

- Keep message payloads small (prefer IDs over big objects).
- Version message schemas.
- Make consumers idempotent and observable (logs/metrics/tracing).
- Monitor queue depth, processing lag, failure rate, retry rate.
- Set clear SLAs for processing latency.

Queues are a foundational building block for scalable and resilient PHP systems with asynchronous workloads.

</details>

<details>
<summary>57. What is event-driven architecture in PHP?</summary>

#### PHP

Event-driven architecture (EDA) is a style where system components communicate by publishing and reacting to events instead of direct synchronous calls.

1. **Core concept**

- A producer emits an event (for example, `OrderPlaced`).
- Interested consumers subscribe and handle it independently.
- Publisher does not need to know which consumers exist.

2. **Why EDA is useful**

- Decouples modules/services.
- Improves extensibility (new consumers can be added without changing publisher).
- Supports async processing and better scalability.
- Makes side effects explicit as domain/integration events.

3. **Typical PHP use cases**

- Order created -> send email, reserve stock, publish analytics.
- User registered -> welcome sequence, CRM sync, audit log.
- Payment succeeded -> invoice generation, notifications, fulfillment.

4. **Event types**

- **Domain events**: business-significant facts inside domain boundary.
- **Integration events**: events published for other services/systems.

5. **Delivery options in PHP ecosystem**

- In-process event bus/dispatcher (framework-level events).
- Queue/broker-backed delivery (RabbitMQ/Kafka/Redis streams/queues) for async and cross-service distribution.

6. **Key design concerns**

- Idempotent handlers (events may be delivered more than once).
- Ordering guarantees (depends on transport/topic/partition strategy).
- Retry and dead-letter policy for failures.
- Schema/version evolution for event payloads.

7. **Best practices**

- Use immutable, versioned event payloads.
- Keep handlers focused and independent.
- Treat events as facts (past tense naming: `UserRegistered`).
- Add observability: correlation IDs, tracing, processing lag metrics.

EDA in PHP helps build modular, scalable systems where workflows can evolve without tight coupling between components.

</details>

<details>
<summary>58. What are WebSockets and when to use them?</summary>

#### PHP

WebSockets are a protocol that creates a persistent, bidirectional connection between client and server, enabling real-time data exchange without repeated HTTP polling.

1. **How WebSockets differ from HTTP**

- HTTP: request/response, usually short-lived and client-initiated.
- WebSocket: one long-lived connection where both sides can push messages anytime.

2. **When WebSockets are useful**

- Real-time chat and messaging.
- Live dashboards/monitoring updates.
- Collaborative editing and presence indicators.
- Trading/market feeds, gaming events, notifications.

3. **Why not use WebSockets everywhere**

- Adds operational complexity (connection state, scaling, routing).
- Not needed for simple CRUD pages with infrequent updates.
- For some cases, SSE or short polling can be simpler and sufficient.

4. **PHP architecture considerations**

- Traditional PHP-FPM request model is not ideal for long-lived connections.
- Common approaches:
  dedicated WebSocket servers (Ratchet/Swoole/RoadRunner),
  separate real-time service + PHP backend integration via Redis/message broker.

5. **Scaling concerns**

- Connection fan-out and broadcast efficiency.
- Sticky sessions vs shared pub/sub backplane.
- Horizontal scaling with Redis/Kafka/NATS-like messaging layers.

6. **Security and reliability**

- Authenticate WebSocket handshake/session.
- Validate message schema and enforce authorization per channel/topic.
- Apply rate limits and abuse protection.
- Handle reconnects, heartbeats, and backpressure.

7. **Rule of thumb**

- Use WebSockets when low-latency server push is a core product requirement.
- Prefer simpler HTTP-based approaches when near-real-time is enough.

WebSockets are a powerful real-time tool in PHP ecosystems when paired with the right runtime and scaling model.

</details>

<details>
<summary>59. How do you build REST APIs in PHP?</summary>

#### PHP

Building REST APIs in PHP means exposing resources over HTTP using clear routes, standard methods, predictable status codes, and consistent JSON contracts.

1. **Core REST principles**

- Resource-oriented endpoints (`/users`, `/orders/{id}`).
- Proper HTTP methods:
  `GET`, `POST`, `PUT/PATCH`, `DELETE`.
- Stateless requests.
- Consistent representation format (usually JSON).

2. **Typical API layers in PHP**

- Route/controller layer (HTTP input/output).
- Validation/auth/middleware layer.
- Service/use-case layer (business logic).
- Repository/data layer (persistence).

3. **Design essentials**

- Versioning strategy (`/api/v1/...` or header-based).
- Standard response envelope and error format.
- Pagination/filtering/sorting conventions.
- Idempotency for relevant write operations.

4. **HTTP correctness**

- Return meaningful status codes (`200`, `201`, `204`, `400`, `401`, `403`, `404`, `422`, `500`).
- Set `Content-Type: application/json`.
- Use caching headers where appropriate.

5. **Security baseline**

- Authentication (token/JWT/session depending on context).
- Authorization checks per resource/action.
- Input validation and output encoding.
- Rate limiting and abuse protection.
- CSRF protection for cookie-based APIs.

6. **Operational quality**

- Structured logging + request correlation IDs.
- Centralized exception handling.
- OpenAPI/Swagger documentation.
- Contract/integration tests for critical endpoints.

7. **Example endpoint shape**

- `POST /api/v1/orders`
- Validate payload -> run use case -> return `201 Created` with resource body/location.

8. **Practical guideline**

- Keep controllers thin.
- Keep business logic out of HTTP layer.
- Make API contracts explicit and stable.

A good PHP REST API is not only about routes, but about consistent contracts, secure behavior, and operational reliability.

</details>

<details>
<summary>60. What is GraphQL and how is it used in PHP?</summary>

#### PHP

GraphQL is an API query language and runtime where clients request exactly the fields they need from a typed schema, instead of consuming fixed REST payloads.

1. **Core GraphQL concepts**

- **Schema**: strongly typed contract (types, fields, arguments).
- **Queries**: read operations.
- **Mutations**: write operations.
- **Resolvers**: PHP functions/methods that fetch/compute field data.

2. **Why teams use GraphQL**

- Avoid over-fetching/under-fetching common in REST.
- Single endpoint for flexible data retrieval.
- Better frontend velocity for complex UI data needs.
- Strong introspection and tooling support.

3. **How it is used in PHP**

- Define GraphQL schema in code/SDL.
- Implement resolvers that call services/repositories.
- Execute query against schema and return JSON response.
- Integrate auth, validation, complexity limits, and caching in execution layer.

4. **Typical PHP stack options**

- `webonyx/graphql-php` (core GraphQL implementation)
- Framework integrations/adapters for Laravel/Symfony ecosystems

5. **Trade-offs**

- More complexity than basic REST for simple APIs.
- Requires strict query depth/complexity controls to avoid expensive queries.
- Caching strategy can be harder than REST endpoint caching.
- Schema governance/versioning discipline is essential.

6. **Best practices**

- Keep resolvers thin; delegate to application services.
- Use DataLoader pattern to avoid N+1 backend calls.
- Enforce auth per field/resource where needed.
- Limit query depth/complexity and monitor heavy operations.
- Publish schema docs and treat schema changes as contracts.

GraphQL in PHP is most effective for data-rich products with complex client needs, provided the team manages query complexity and schema governance carefully.

</details>

<details>
<summary>61. What is API authentication (JWT, OAuth)?</summary>

#### PHP

API authentication verifies who is calling your API and under what permissions. Two common approaches are JWT-based token auth and OAuth 2.0 / OpenID Connect flows.

1. **JWT-based authentication**

- After successful login, server issues signed token (JWT).
- Client sends token on each request (usually `Authorization: Bearer ...`).
- API validates signature, expiry, and claims.

Typical JWT claims:
- `sub` (subject/user id)
- `exp` (expiration)
- `iss`/`aud` (issuer/audience)
- optional roles/scopes

2. **OAuth 2.0 (authorization framework)**

- Designed for delegated access and third-party authorization.
- Access is granted via scopes and token lifetimes.
- Common flows: Authorization Code (+ PKCE), Client Credentials.

3. **OpenID Connect (OIDC)**

- Identity layer on top of OAuth 2.0.
- Adds ID token and standardized user identity claims.

4. **JWT vs OAuth (practical distinction)**

- JWT is token format/mechanism.
- OAuth is authorization protocol.
- OAuth tokens may be JWT or opaque.

5. **Security best practices**

- Use HTTPS only.
- Keep access tokens short-lived; rotate refresh tokens safely.
- Validate signature, issuer, audience, expiry on every request.
- Store tokens securely on client side (avoid insecure storage patterns).
- Implement revocation/introspection strategy where needed.

6. **PHP implementation guidance**

- Use battle-tested libraries for JWT/OAuth/OIDC validation.
- Centralize authentication middleware.
- Separate authentication (who) from authorization (what allowed).
- Represent permissions as roles/scopes/policies checked at resource level.

Strong API authentication in PHP is about protocol correctness, token lifecycle hygiene, and strict validation on every protected endpoint.

</details>

<details>
<summary>62. What is rate limiting and API security?</summary>

#### PHP

Rate limiting is a control mechanism that restricts how many requests a client can make in a given time window. It is a core part of broader API security.

1. **Why rate limiting is needed**

- Prevent abuse and brute-force attacks.
- Protect backend resources from overload.
- Ensure fair usage across clients/tenants.
- Reduce impact of buggy or malicious integrations.

2. **Common rate limiting strategies**

- Fixed window (simple counters per interval).
- Sliding window (more accurate distribution).
- Token bucket / leaky bucket (burst-friendly with sustained limits).

3. **Where limits are applied**

- Per IP address
- Per API key/client id
- Per user/account/tenant
- Per endpoint sensitivity (stricter for auth endpoints)

4. **Typical implementation in PHP stacks**

- Middleware-level checks using Redis/in-memory counters.
- Reverse proxy/API gateway enforcement (Nginx, cloud API gateway).
- Return `429 Too Many Requests` with retry headers.

5. **API security baseline (beyond rate limits)**

- Strong authentication (JWT/OAuth/OIDC).
- Authorization checks per resource/action.
- Input validation and output encoding.
- HTTPS everywhere + secure headers.
- Request size/time limits and timeout control.
- Audit logging, anomaly detection, and alerting.

6. **Best practices**

- Use layered controls: gateway + app middleware.
- Apply different quotas by plan/trust level.
- Add burst handling and graceful degradation.
- Protect login/token endpoints with stricter rules and lockouts.
- Monitor limit hits, blocked requests, and attack patterns.

Rate limiting is one pillar of API security; real protection comes from combining it with authentication, authorization, validation, and observability.

</details>

<details>
<summary>63. What is testing pyramid in PHP?</summary>

#### PHP

Testing pyramid is a test strategy model that recommends many fast low-level tests and fewer slow high-level tests to balance confidence, speed, and maintenance cost.

1. **Pyramid layers**

- **Base (largest): Unit tests**
  fast, isolated tests for functions/classes/business rules.
- **Middle: Integration tests**
  verify collaboration between modules (DB, cache, queue, external adapters).
- **Top (smallest): End-to-end/API/UI tests**
  validate full user flows across the whole system.

2. **Why this model works**

- Unit tests are cheap and run quickly in large numbers.
- Integration tests catch boundary and wiring issues.
- E2E tests provide realistic confidence but are slower and more brittle.

3. **PHP-specific mapping**

- Unit: PHPUnit/Pest with mocks/stubs.
- Integration: real DB containers, repositories, HTTP clients in controlled env.
- E2E/API: request-level tests against running app/service.

4. **Common anti-patterns**

- “Ice cream cone”: too many UI/E2E tests, too few unit tests.
- Over-mocking everything, losing integration confidence.
- No contract tests for critical external integrations.

5. **Practical recommendations**

- Keep majority of tests at unit level.
- Add focused integration tests around critical boundaries.
- Keep E2E suite small, stable, and business-critical.
- Run fast suites on each commit; heavier suites on main/pre-release gates.

6. **Outcome**

A healthy pyramid gives fast feedback to developers and strong release confidence without excessive CI time or flaky test maintenance.

</details>

<details>
<summary>64. What is unit testing (PHPUnit / Pest)?</summary>

#### PHP

Unit testing verifies the behavior of the smallest testable pieces of code (functions, methods, classes) in isolation from external systems.

1. **What unit tests should cover**

- Business rules and calculations.
- Edge cases and input validation.
- Error/exception behavior.
- Deterministic logic branches.

2. **Isolation principle**

- Unit tests should not depend on real DB, network, filesystem, or queue services.
- External dependencies are replaced with test doubles (mocks/stubs/fakes).

3. **PHP tools**

- **PHPUnit**: classic and widely adopted testing framework.
- **Pest**: expressive syntax built on top of PHPUnit ecosystem.

4. **Simple example (PHPUnit style)**

```php
final class PriceCalculatorTest extends TestCase
{
    public function test_applies_discount(): void
    {
        $calc = new PriceCalculator();
        self::assertSame(90, $calc->applyDiscount(100, 10));
    }
}
```

5. **Why unit tests matter**

- Fast feedback during development.
- Safer refactoring.
- Better documentation of expected behavior.
- Early regression detection.

6. **Best practices**

- Keep tests small, focused, and deterministic.
- Use clear arrange-act-assert structure.
- Name tests by expected behavior.
- Avoid over-mocking internal logic.
- Run unit tests on every commit in CI.

Unit testing with PHPUnit/Pest is the foundation of reliable PHP delivery because it provides fast and precise confidence in core logic.

</details>

<details>
<summary>65. What is integration testing?</summary>

#### PHP

Integration testing verifies that multiple components work correctly together (for example, application logic + database + cache + external adapters), while still staying narrower than full end-to-end tests.

1. **What integration tests focus on**

- Module boundaries and collaboration.
- Data persistence/retrieval correctness.
- Infrastructure adapter behavior.
- Configuration and wiring correctness.

2. **How it differs from unit tests**

- Unit tests isolate one component and mock dependencies.
- Integration tests use real or close-to-real dependencies to validate interactions.

3. **Typical PHP integration scenarios**

- Repository with real test DB/container.
- HTTP client adapter against sandbox/mock server.
- Queue publishing/consuming flow in controlled environment.
- Framework route + middleware + controller + service interaction.

4. **Why integration tests matter**

- Catch issues mocks cannot reveal (SQL schema mismatch, serialization bugs, config mistakes).
- Increase confidence in critical boundaries.
- Reduce production surprises from infrastructure coupling.

5. **Best practices**

- Run against dedicated test infrastructure (isolated DB/cache).
- Control data setup/teardown deterministically.
- Keep scope focused: one integration concern per test.
- Avoid unnecessary network dependency when contract stubs are enough.
- Include integration suite in CI for critical paths.

6. **Trade-off**

- Slower and heavier than unit tests, so they should be fewer and targeted.

Integration tests are the bridge between fast unit confidence and full system confidence in PHP delivery pipelines.

</details>

<details>
<summary>66. What is mocking and why is it needed?</summary>

#### PHP

Mocking is a testing technique where real dependencies are replaced with controlled test doubles to isolate the unit under test and verify interactions.

1. **Why mocking is needed**

- Isolate business logic from external systems (DB, HTTP, queue, filesystem).
- Make tests fast and deterministic.
- Simulate rare/error scenarios that are hard to reproduce with real services.
- Verify collaboration contracts (method called with expected arguments).

2. **Common test double types**

- **Stub**: returns predefined values.
- **Mock**: verifies expected interactions/calls.
- **Fake**: lightweight working implementation (for example, in-memory repository).
- **Spy**: records calls for later assertions.

3. **PHP example concept**

Test `OrderService` by mocking `PaymentGatewayInterface` and `OrderRepositoryInterface`, then assert:
- service returns expected result
- gateway called once with correct amount
- repository save called with expected entity state

4. **Where mocking is appropriate**

- Unit tests of domain/application services.
- Error-path testing for external dependencies.
- Contract verification at module boundaries.

5. **Where mocking is not enough**

- Integration behavior with real DB/network protocols.
- Framework wiring/configuration issues.
- Performance characteristics and transaction semantics.

6. **Best practices**

- Mock only external boundaries, not internal pure logic.
- Keep expectations focused on observable behavior.
- Prefer interfaces for mockable dependencies.
- Combine unit + integration tests (mocking is not a full strategy alone).

Mocking is essential for fast, isolated PHP unit tests, but it should be balanced with integration tests for real-system confidence.

</details>

<details>
<summary>67. What is code coverage?</summary>

#### PHP

Code coverage is a metric that shows which parts of source code were executed by automated tests.

1. **What coverage measures**

- **Line coverage**: executed lines.
- **Branch/condition coverage**: executed decision branches.
- **Function/method coverage**: executed callable units.

2. **Why it is useful**

- Highlights untested areas.
- Helps prioritize where tests are missing.
- Supports regression risk assessment during refactoring.

3. **What coverage does NOT guarantee**

- High coverage does not automatically mean high test quality.
- Tests may execute code without asserting correct behavior.
- Critical edge cases can still be missed despite good percentages.

4. **PHP tooling**

- PHPUnit/Pest can generate coverage reports.
- Typically relies on Xdebug or PCOV drivers.
- Reports can be produced in text, HTML, or CI formats.

5. **Practical usage in teams**

- Track trends over time rather than chasing one absolute number.
- Set sensible minimum thresholds for critical modules.
- Use coverage deltas in PR checks to prevent test regressions.

6. **Best practices**

- Focus first on testing critical business logic and risky paths.
- Pair coverage with mutation testing/static analysis when possible.
- Review assertion quality, not only executed lines.
- Keep flaky or low-value tests out of coverage gaming.

Code coverage is a useful signal for test completeness, but it should be interpreted with test quality and risk context, not as a standalone target.

</details>

<details>
<summary>68. What is static analysis (PHPStan, Psalm)?</summary>

#### PHP

Static analysis checks PHP code without executing it to detect type issues, potential bugs, dead code, and architecture violations early.

1. **What static analysis finds**

- Type mismatches and impossible types.
- Nullability and undefined variable/property/method access issues.
- Incorrect return types and unsafe casts.
- Unreachable/dead code and some API misuse patterns.

2. **Main tools**

- **PHPStan**: widely adopted, strictness levels, strong ecosystem integration.
- **Psalm**: advanced type system, powerful inference, taint analysis options.

3. **Why it is valuable**

- Finds defects before runtime and before tests may cover them.
- Improves refactoring safety in large codebases.
- Encourages stronger typing and clearer contracts.
- Reduces production incidents caused by basic type/flow mistakes.

4. **How teams use it**

- Run in CI on every PR.
- Start with moderate strictness and increase gradually.
- Maintain baseline for legacy issues while preventing new ones.

5. **Best practices**

- Add type hints/return types consistently.
- Use generics annotations where needed (collections, repositories).
- Fix root-cause typing problems instead of suppressing warnings.
- Keep analysis config versioned and reviewed like code.

6. **Static analysis vs tests**

- Static analysis does not replace tests.
- It complements unit/integration tests by proving structural/type correctness across paths tests might miss.

Static analysis with PHPStan/Psalm is a high-leverage quality gate for modern PHP projects, especially during continuous refactoring.

</details>

<details>
<summary>69. What is Rector and how is it used for refactoring?</summary>

#### PHP

Rector is an automated refactoring tool for PHP that transforms source code using predefined and custom rules, helping upgrade and modernize codebases safely at scale.

1. **What Rector does**

- Applies AST-based code transformations.
- Upgrades syntax/features across PHP versions.
- Refactors framework/library usage patterns.
- Automates repetitive mechanical changes.

2. **Typical use cases**

- Upgrade from older PHP versions to newer standards.
- Migrate deprecated APIs to current alternatives.
- Enforce modern language constructs (typed properties, constructor promotion, etc.).
- Large-scale codebase cleanup before strict static analysis adoption.

3. **How it is used in practice**

1. Configure `rector.php` with rule sets.
2. Run Rector on selected paths.
3. Review generated diff.
4. Run tests/static analysis.
5. Commit incremental, safe batches.

4. **Why teams use Rector**

- Speeds up modernization work dramatically.
- Reduces human error in repetitive refactors.
- Keeps refactoring consistent across modules.

5. **Best practices**

- Run Rector on focused scopes, not whole legacy codebase at once.
- Keep changes small and reviewable.
- Always validate with tests + PHPStan/Psalm after transformation.
- Pin Rector version in tooling for reproducibility.
- Combine automated refactoring with manual architectural review.

6. **Important limitation**

- Rector handles mechanical transformations well, but cannot replace architectural judgment or domain-specific redesign decisions.

Rector is most effective as part of a refactoring pipeline with static analysis and tests, not as a standalone “one-click migration” tool.

</details>

<details>
<summary>70. What is coding standard enforcement (PHP-CS-Fixer)?</summary>

#### PHP

Coding standard enforcement is the practice of automatically checking and fixing code style rules so the codebase remains consistent, readable, and review-friendly.

1. **Why coding standards matter**

- Improves readability across teams.
- Reduces style noise in pull requests.
- Makes code reviews focus on logic, not formatting.
- Keeps long-lived codebases coherent.

2. **What PHP-CS-Fixer does**

- Scans PHP files against configured style rules.
- Automatically rewrites code formatting/style issues.
- Supports standard rule sets (for example, PSR-12) plus custom rules.

3. **Typical workflow**

- Configure rules in `.php-cs-fixer.php`.
- Run checker in CI to prevent drift.
- Run fixer locally/pre-commit to auto-format changed files.

4. **Common rules categories**

- Imports ordering and unused imports removal.
- Spacing/indentation/braces style.
- Array/function syntax normalization.
- Strict typing and modern syntax preference rules.

5. **Best practices**

- Agree on one project-wide standard early.
- Auto-fix in developer workflow (pre-commit/hooks/editor integration).
- Keep CI as enforcement gate (`--dry-run` mode).
- Apply large reformatting separately from feature changes to keep diffs clear.

6. **Related tools**

- PHP-CS-Fixer (auto-fix formatting/style).
- PHP_CodeSniffer (rule checking and coding standard analysis).
- Combine style tools with PHPStan/Psalm for quality beyond formatting.

Coding standard enforcement with tools like PHP-CS-Fixer is a low-cost way to improve maintainability and team velocity in PHP projects.

</details>

<details>
<summary>71. What is CI/CD pipeline for PHP applications?</summary>

#### PHP

CI/CD pipeline is an automated workflow that builds, tests, verifies, and deploys PHP applications consistently from commit to production.

1. **CI (Continuous Integration) goals**

- Validate every change quickly.
- Catch bugs early via automated checks.
- Keep main branch always releasable.

2. **Typical CI stages for PHP**

1. Install dependencies (`composer install`).
2. Static checks (PHPStan/Psalm, coding standards).
3. Unit/integration tests (PHPUnit/Pest).
4. Build/package artifacts (Docker image or deploy bundle).

3. **CD (Continuous Delivery/Deployment) goals**

- Deliver validated artifacts safely to environments.
- Automate rollout steps and minimize manual errors.
- Support quick rollback on incidents.

4. **Typical CD stages**

- Deploy to staging.
- Run smoke/health checks.
- Promote same artifact to production.
- Monitor post-deploy metrics and logs.

5. **PHP-specific best practices**

- Use lockfile-based reproducible installs.
- Build immutable artifacts once and reuse across environments.
- Run DB migrations with controlled strategy.
- Keep secrets/config outside artifact.
- Use zero-downtime rollout patterns (blue-green/canary/rolling).

6. **Quality gates**

- Required test pass status.
- Static analysis threshold.
- Security checks (dependency audit/SAST).
- Optional performance smoke checks for critical endpoints.

7. **Outcome**

A solid CI/CD pipeline improves release frequency, reliability, and team confidence while reducing production risk in PHP delivery.

</details>

<details>
<summary>72. How do you deploy PHP applications?</summary>

#### PHP

Deploying PHP applications means delivering a tested artifact to production with predictable runtime configuration, minimal downtime, and rollback safety.

1. **Common deployment targets**

- Traditional VM/bare metal with Nginx/Apache + PHP-FPM.
- Container platforms (Docker, Kubernetes, ECS).
- Platform services (PaaS/serverless variants).

2. **Recommended deployment flow**

1. Build immutable artifact (image/package) in CI.
2. Run tests/static checks/security scans.
3. Deploy artifact to staging.
4. Execute smoke checks and health checks.
5. Promote same artifact to production.

3. **Runtime essentials**

- Environment-based config and secrets (not hardcoded).
- Correct PHP extensions and OPcache settings.
- DB/cache/queue connectivity verified at startup.
- Structured logging and monitoring enabled.

4. **Database migration strategy**

- Apply backward-compatible migrations before switching traffic.
- Use expand-and-contract approach for risky schema changes.
- Keep migration scripts versioned and repeatable.

5. **Zero/low-downtime techniques**

- Blue-green, rolling, or canary deployments.
- Graceful worker reloads (PHP-FPM/process manager).
- Health-check-based traffic switching via load balancer.

6. **Rollback strategy**

- Fast rollback to previous artifact/version.
- Controlled DB rollback or forward-fix plan.
- Post-deploy monitoring window with alerting.

7. **Best practices**

- Never deploy directly from local machine.
- Keep deploy process automated and auditable.
- Use infrastructure as code where possible.
- Separate build-time and runtime concerns clearly.

Good PHP deployment is an engineering system: reproducible artifacts, safe rollout mechanics, observability, and reliable rollback.

</details>

<details>
<summary>73. What is blue-green deployment?</summary>

#### PHP

Blue-green deployment is a release strategy where two identical production environments are maintained: one active (serving traffic) and one idle (candidate for next release).

1. **How it works**

- **Blue**: current live environment.
- **Green**: new version deployed and validated in parallel.
- After checks pass, traffic is switched from Blue to Green.
- Old environment remains available for quick rollback.

2. **Why teams use it**

- Minimizes deployment downtime.
- Reduces release risk with near-instant rollback.
- Enables realistic pre-switch verification on production-like stack.

3. **Typical rollout flow**

1. Deploy new PHP release to idle environment.
2. Run health checks/smoke tests/migrations strategy.
3. Switch load balancer/router to new environment.
4. Monitor error rates/latency.
5. Keep previous environment temporarily for rollback.

4. **Key considerations for PHP apps**

- Session strategy must support environment switch (shared Redis/session store).
- Static assets/versioning should be compatible across both environments.
- DB changes must be backward-compatible during transition window.
- Queue workers and cron jobs must avoid duplicate side effects.

5. **Advantages**

- Fast rollback path.
- Safer deployments for high-traffic systems.
- Clear separation of “current” vs “candidate” release.

6. **Trade-offs**

- Higher infrastructure cost (two environments).
- More operational complexity around data/schema compatibility.

Blue-green is a strong deployment pattern for PHP production systems where uptime and rollback speed are critical.

</details>

<details>
<summary>74. What is rollback strategy?</summary>

#### PHP

Rollback strategy is a predefined plan for quickly restoring a stable previous version when a deployment causes incidents (errors, regressions, performance drops, data issues).

1. **Why rollback strategy is critical**

- Reduces incident duration and customer impact.
- Prevents ad-hoc emergency actions during outages.
- Increases confidence in frequent releases.

2. **What should be rollback-ready**

- Application artifact/image version.
- Infrastructure/config version.
- Feature flags/toggles state.
- Database migration compatibility plan.

3. **Common rollback approaches**

- **Artifact rollback**: redeploy previous known-good build.
- **Traffic rollback**: switch back to previous environment (blue-green/canary revert).
- **Feature rollback**: disable problematic feature flag without full redeploy.

4. **Database rollback reality**

- DB rollback is often hardest part.
- Prefer backward-compatible migrations:
  expand first, contract later.
- Use forward-fix when true schema rollback is risky.

5. **Operational checklist**

- Define rollback trigger thresholds (error rate, latency, failed checks).
- Keep previous release immediately deployable.
- Automate rollback steps in pipeline/runbooks.
- Verify health after rollback and continue monitoring.

6. **Best practices**

- Rehearse rollback in staging regularly.
- Keep releases small to reduce blast radius.
- Couple rollout and rollback with observability (logs/metrics/traces).
- Document ownership and incident decision flow.

A strong rollback strategy is a core reliability mechanism for PHP production delivery, especially in high-frequency deployment environments.

</details>

<details>
<summary>75. What is serverless PHP (Laravel Vapor, Bref)?</summary>

#### PHP

Serverless PHP is an execution model where your PHP code runs on managed cloud functions/platforms without managing traditional servers directly.

1. **Core idea**

- You deploy code/functions, not VM fleets.
- Cloud provider handles provisioning, scaling, and much of operations.
- Billing is typically based on execution time and requests.

2. **Common PHP serverless options**

- **Laravel Vapor**:
  Laravel-focused platform on AWS (Lambda, managed integrations).
- **Bref**:
  open-source runtime/tooling to run PHP on AWS Lambda (framework-agnostic support).

3. **Why teams use serverless PHP**

- Fast horizontal auto-scaling.
- Lower ops burden (patching/provisioning reduced).
- Cost efficiency for spiky or low baseline traffic.
- Faster time-to-production for API/backoffice workloads.

4. **Architecture implications**

- Stateless function execution.
- Externalized state (DB, Redis, object storage, queues).
- Event-driven triggers (HTTP, queues, cron, object events).
- Cold starts and execution limits must be considered.

5. **Best use cases**

- APIs with variable traffic.
- Background jobs/events.
- Scheduled tasks and lightweight automation.
- MVPs and teams optimizing for speed of delivery.

6. **Trade-offs**

- Platform/runtime constraints and timeouts.
- Vendor lock-in risk.
- Cold-start latency impact on some endpoints.
- Debugging/observability can require extra setup.

7. **Best practices**

- Keep functions small and focused.
- Optimize bootstrap time and dependency footprint.
- Use async queues for long-running work.
- Configure robust logging/metrics/tracing from day one.
- Design idempotent handlers and retry-safe workflows.

Serverless PHP with Vapor/Bref is a strong option for scalable, low-ops architectures when workload characteristics match the serverless model.

</details>

<details>
<summary>76. What are microservices vs monolith in PHP?</summary>

#### PHP

Monolith and microservices are architectural styles for structuring systems. In PHP, both can work well when chosen based on team size, domain complexity, and operational maturity.

1. **Monolith (single deployable app)**

- One codebase/deployable unit containing multiple business capabilities.
- Shared runtime and usually shared database.

**Pros**
- Simpler development, testing, and deployment.
- Lower operational overhead.
- Easier local debugging and transactions across modules.

**Cons**
- Can become hard to evolve if boundaries are weak.
- Large deployments may increase release risk.
- Scaling is often coarse-grained (whole app).

2. **Microservices (multiple independently deployable services)**

- System split into small services aligned to business domains.
- Each service owns its logic and often its datastore.

**Pros**
- Independent scaling/deployment per service.
- Clear ownership boundaries.
- Technology/runtime flexibility per service.

**Cons**
- Higher complexity (networking, observability, auth, retries, data consistency).
- Harder local development and cross-service debugging.
- Significant DevOps/platform maturity required.

3. **PHP-specific practical reality**

- Many teams succeed with a modular monolith first.
- Microservices become worthwhile when clear bounded contexts and team scaling justify operational cost.

4. **Decision guideline**

- Choose **monolith/modular monolith** when:
  product is early-stage, team is small/medium, velocity matters most.
- Choose **microservices** when:
  domains are clearly separable, scaling needs differ strongly, and platform capabilities are mature.

5. **Common mistake**

- Starting with microservices too early creates accidental complexity without business payoff.

In PHP ecosystems, the pragmatic path is usually: well-structured monolith first, then selective extraction to services when objective constraints demand it.

</details>

<details>
<summary>77. What is modular monolith architecture?</summary>

#### PHP

A modular monolith is a single deployable application structured as clearly separated internal modules with explicit boundaries and contracts.

1. **Core idea**

- One application/runtime/deployment unit.
- Multiple business modules (bounded contexts) inside it.
- Strong internal boundaries to reduce coupling.

2. **How it differs**

- Vs classic monolith:
  modular monolith enforces strict module boundaries and dependency rules.
- Vs microservices:
  keeps single deployable unit and avoids distributed system complexity.

3. **Typical PHP module structure**

- `Modules/Orders/...`
- `Modules/Billing/...`
- `Modules/Users/...`

Each module contains own:
- domain logic
- application/use-case services
- infrastructure adapters
- HTTP/API handlers (or mapped interfaces)

4. **Why teams choose it**

- Faster development than microservices.
- Easier local debugging and transactions.
- Lower operational overhead.
- Good path for domain-driven organization and future service extraction.

5. **Boundary enforcement practices**

- Communicate between modules via interfaces/events, not direct internals.
- Avoid shared mutable “god” utilities across modules.
- Use static analysis/tests to enforce dependency direction.
- Keep database ownership clear (even if physically shared).

6. **When it is a good fit**

- Product and team are growing, but microservices complexity is premature.
- Need strong domain separation with simple deployment model.

7. **Evolution path**

- Start modular monolith.
- Extract selected modules into services only when scaling/team/ownership pressure is real and measurable.

Modular monolith is often the most pragmatic architecture for PHP teams that want clean boundaries today without distributed system overhead too early.

</details>

<details>
<summary>78. What are common PHP vulnerabilities in real projects?</summary>

#### PHP

Most real PHP security incidents come from unsafe input handling, weak auth/session controls, and dependency/configuration issues rather than the language itself.

1. **Injection vulnerabilities**

- SQL Injection from unsafe query construction.
- Command Injection when passing untrusted input to shell/system calls.
- Header/LDAP/NoSQL-style injections in integration layers.

2. **Cross-site vulnerabilities**

- XSS (stored/reflected/DOM) due to missing contextual output escaping.
- CSRF in cookie-auth flows without token and SameSite protections.

3. **Authentication and authorization flaws**

- Weak password handling or missing MFA for critical roles.
- Broken access control (IDOR/BOLA): user accesses other users' resources by changing IDs.
- Missing server-side authorization checks on sensitive endpoints.

4. **Session and token issues**

- Insecure cookie flags (`Secure`, `HttpOnly`, `SameSite` absent).
- Session fixation/hijacking due to poor ID rotation.
- Leaked or long-lived API tokens without revocation strategy.

5. **File handling risks**

- Unsafe file uploads (no type/content validation, executable uploads).
- Path traversal (`../`) due to unchecked file paths.
- Insecure deserialization or unsafe parsing of untrusted files.

6. **Configuration and dependency risks**

- Debug mode enabled in production.
- Exposed secrets in repo/logs/environment dumps.
- Outdated dependencies with known CVEs.
- Misconfigured CORS/CSP/security headers.

7. **How to mitigate systematically**

- Strict input validation + output encoding by context.
- Prepared statements and safe query layers.
- Centralized authz policies and deny-by-default checks.
- Secure session/token lifecycle management.
- Dependency scanning/patching and hardened production config.
- Regular security testing (SAST/DAST), logging, and incident playbooks.

Security in PHP projects is primarily a discipline of secure design, safe defaults, and continuous verification across code, runtime, and operations.

</details>

<details>
<summary>79. How do you detect memory leaks in PHP?</summary>

#### PHP

In PHP, "memory leaks" are often not classic permanent leaks from script-level code, but memory growth caused by long-running processes, retained references, large in-memory buffers, extension-level leaks, or allocator fragmentation.

1. **First identify where leak-like behavior appears**

- FPM/request model: memory should return after request ends; growth usually indicates worker-level issues or oversized requests.
- Long-running workers (queue consumers, daemons, Swoole/RoadRunner): retained state between jobs is a common source.
- CLI batch scripts: unbounded arrays/caches can simulate leaks.

2. **Instrument memory inside code**

- Use `memory_get_usage(true)` and `memory_get_peak_usage(true)` around major pipeline stages.
- Log memory per iteration/job to detect monotonic growth trend.
- Add counters for processed items so you can correlate memory with workload size.

3. **Use runtime/process-level diagnostics**

- Watch worker RSS over time via `ps`, `top`, container metrics, or APM.
- Compare PHP-level usage vs OS-level memory to spot allocator/fragmentation behavior.
- In FPM, monitor pool worker memory and restart patterns.

4. **Use profilers and specialized tools**

- Xdebug/Blackfire/Tideways for allocation hotspots and heavy call paths.
- Valgrind/ASan for C-extension or native-level leaks (debug builds, slower but precise).
- Framework debug toolbars/profilers for request memory snapshots.

5. **Common root causes to check**

- Static/global arrays accumulating data across jobs.
- Event listeners/closures capturing large objects unintentionally.
- ORM identity maps or query results retained too long.
- Large strings/JSON payload copies during transformations.
- Circular references plus delayed GC in long loops.

6. **Mitigation patterns after detection**

- Process data in chunks/streams instead of full in-memory collections.
- Explicitly `unset()` large variables and occasionally call `gc_collect_cycles()` in long loops.
- Recreate worker process after N jobs/time (`--max-jobs`, supervisor restarts).
- Configure sane memory limits and fail-fast behavior.
- Keep dependencies/extensions updated when native leaks are fixed upstream.

The practical approach is: measure trend, isolate hotspot, confirm with profiling, and enforce lifecycle boundaries for long-running processes.

</details>

<details>
<summary>80. How do you optimize memory usage?</summary>

#### PHP

Memory optimization in PHP is mostly about controlling data lifetime, reducing unnecessary copies, and using streaming/chunked processing instead of loading everything at once.

1. **Process data incrementally**

- Prefer generators (`yield`) for large datasets instead of building huge arrays.
- Read files/streams line-by-line or in chunks.
- Paginate DB reads (`LIMIT/OFFSET` or cursor/chunk APIs) for batch jobs.

2. **Avoid unnecessary copies**

- Minimize string concatenation in tight loops; use buffering strategies.
- Avoid repeated `array_merge` on large arrays inside loops.
- Be careful with transformations that duplicate big structures.

3. **Release memory early in long-running scripts**

- `unset()` large temporary variables after use.
- Break work into bounded iterations; clear per-iteration state.
- For cyclic references in long loops, occasionally call `gc_collect_cycles()`.

4. **Choose efficient data access patterns**

- Select only needed columns in SQL, not `SELECT *`.
- Hydrate lightweight DTOs/arrays when full ORM models are unnecessary.
- Use lazy-loading carefully; avoid N+1 queries and excessive object graphs.

5. **Use runtime limits and worker lifecycle controls**

- Set reasonable `memory_limit` to fail fast instead of degrading the host.
- For queue workers, restart after N jobs/time to avoid long-term memory drift.
- Monitor memory trend with `memory_get_usage(true)` and OS metrics.

6. **Cache smartly, not blindly**

- Cache only high-value, expensive computations.
- Store compact cache payloads; compress when useful.
- Use TTLs/invalidation to prevent unbounded cache growth.

7. **Profile before and after**

- Use Xdebug/Blackfire/Tideways/APM to find real hotspots.
- Optimize measured bottlenecks first; avoid premature micro-optimizations.

In practice, the biggest gains come from streaming/chunking, controlling object lifetimes, and preventing large transient allocations.

</details>

<details>
<summary>81. How would you reverse a string without built-in functions?</summary>

#### PHP

The core idea is to iterate from the end of the string to the beginning and build a new string character by character.

```php
<?php
function reverseString(string $s): string
{
    $result = '';
    $length = strlen($s);

    for ($i = $length - 1; $i >= 0; $i--) {
        $result .= $s[$i];
    }

    return $result;
}
```

Time complexity is `O(n)`, and extra space is `O(n)` for the reversed output.

Notes for interviews:

- This byte-based version works for ASCII.
- For UTF-8/multibyte strings, byte indexing can break characters, so a multibyte-safe approach is needed.

</details>

<details>
<summary>82. How would you remove duplicates from an array?</summary>

#### PHP

The standard approach is to track seen values in a hash map and keep only the first occurrence.

```php
<?php
function removeDuplicates(array $input): array
{
    $seen = [];
    $result = [];

    foreach ($input as $value) {
        $key = is_scalar($value) || $value === null
            ? (string) $value . ':' . gettype($value)
            : serialize($value);

        if (!isset($seen[$key])) {
            $seen[$key] = true;
            $result[] = $value;
        }
    }

    return $result;
}
```

Why this version is interview-friendly:

- Keeps insertion order.
- Works in linear time on average: `O(n)`.
- Handles scalars, `null`, and complex values via `serialize`.

If the question allows built-ins, `array_unique()` is shorter, but manual hash-set logic better demonstrates fundamentals.

</details>

<details>
<summary>83. How would you find the second largest number?</summary>

#### PHP

A robust one-pass solution keeps track of the largest and second largest distinct values while scanning the array.

```php
<?php
function secondLargest(array $numbers): ?int
{
    $max = null;
    $second = null;

    foreach ($numbers as $n) {
        if (!is_int($n)) {
            continue;
        }

        if ($max === null || $n > $max) {
            if ($max !== $n) {
                $second = $max;
            }
            $max = $n;
            continue;
        }

        if ($n !== $max && ($second === null || $n > $second)) {
            $second = $n;
        }
    }

    return $second;
}
```

Behavior:

- Returns `null` if there is no second distinct maximum (e.g., `[5]`, `[7, 7]`).
- Time complexity: `O(n)`.
- Space complexity: `O(1)`.

</details>

<details>
<summary>84. How would you check if a string is a palindrome?</summary>

#### PHP

A palindrome reads the same forward and backward. Efficiently, compare characters from both ends moving toward the center.

```php
<?php
function isPalindrome(string $s): bool
{
    $left = 0;
    $right = strlen($s) - 1;

    while ($left < $right) {
        if ($s[$left] !== $s[$right]) {
            return false;
        }
        $left++;
        $right--;
    }

    return true;
}
```

Complexity:

- Time: `O(n)`
- Space: `O(1)`

Interview notes:

- This is byte-based and fine for ASCII.
- For UTF-8, use a multibyte-safe approach before indexing characters.
- Clarify whether spaces, punctuation, and case should be ignored; if yes, normalize input first.

</details>

<details>
<summary>85. How would you check if a number is prime?</summary>

#### PHP

A number `n` is prime if it has exactly two positive divisors: `1` and `n`.  
Efficient check: test divisibility only up to `sqrt(n)`.

```php
<?php
function isPrime(int $n): bool
{
    if ($n < 2) {
        return false;
    }

    if ($n === 2) {
        return true;
    }

    if ($n % 2 === 0) {
        return false;
    }

    $limit = (int) sqrt($n);
    for ($i = 3; $i <= $limit; $i += 2) {
        if ($n % $i === 0) {
            return false;
        }
    }

    return true;
}
```

Complexity:

- Time: `O(sqrt(n))`
- Space: `O(1)`

This is the standard interview solution: correct, fast enough, and easy to reason about.

</details>

<details>
<summary>86. How would you implement factorial using recursion?</summary>

#### PHP

Recursive factorial uses the definition `n! = n * (n - 1)!` with a base case `0! = 1` (and `1! = 1`).

```php
<?php
function factorial(int $n): int
{
    if ($n < 0) {
        throw new InvalidArgumentException('Factorial is undefined for negative numbers.');
    }

    if ($n === 0 || $n === 1) {
        return 1;
    }

    return $n * factorial($n - 1);
}
```

Complexity:

- Time: `O(n)`
- Space: `O(n)` due to recursion stack.

Interview note: iterative version uses `O(1)` stack space and is safer for very large `n`.

</details>

<details>
<summary>87. How would you implement sorting manually?</summary>

#### PHP

For interviews, a clear manual example is Bubble Sort: repeatedly swap adjacent elements if they are in the wrong order.

```php
<?php
function bubbleSort(array $arr): array
{
    $n = count($arr);

    for ($i = 0; $i < $n - 1; $i++) {
        $swapped = false;

        for ($j = 0; $j < $n - 1 - $i; $j++) {
            if ($arr[$j] > $arr[$j + 1]) {
                $tmp = $arr[$j];
                $arr[$j] = $arr[$j + 1];
                $arr[$j + 1] = $tmp;
                $swapped = true;
            }
        }

        if (!$swapped) {
            break;
        }
    }

    return $arr;
}
```

Complexity:

- Worst/average time: `O(n^2)`
- Best case (already sorted with early break): `O(n)`
- Space: `O(1)` extra (ignoring output copy semantics)

If asked for a more efficient algorithm, explain Merge Sort (`O(n log n)`) or Quick Sort average (`O(n log n)`).

</details>

<details>
<summary>88. How would you generate Fibonacci sequence?</summary>

#### PHP

The most practical approach is iterative: start with `0, 1` and keep appending the sum of the previous two numbers.

```php
<?php
function fibonacciSequence(int $count): array
{
    if ($count <= 0) {
        return [];
    }

    if ($count === 1) {
        return [0];
    }

    $result = [0, 1];

    for ($i = 2; $i < $count; $i++) {
        $result[] = $result[$i - 1] + $result[$i - 2];
    }

    return $result;
}
```

Complexity:

- Time: `O(n)`
- Space: `O(n)` for storing the sequence

Interview note:

- Recursive Fibonacci without memoization is exponential and usually not acceptable for performance-sensitive answers.
- If only the n-th value is needed, space can be reduced to `O(1)` by storing just two previous numbers.

</details>

<details>
<summary>89. How would you find the most frequent element?</summary>

#### PHP

Use a frequency map (hash table): count occurrences of each value, then return the key with the maximum count.

```php
<?php
function mostFrequentElement(array $items): mixed
{
    if ($items === []) {
        return null;
    }

    $freq = [];
    $bestKey = null;
    $bestCount = 0;

    foreach ($items as $item) {
        $key = is_scalar($item) || $item === null
            ? (string) $item . ':' . gettype($item)
            : serialize($item);

        if (!isset($freq[$key])) {
            $freq[$key] = ['value' => $item, 'count' => 0];
        }

        $freq[$key]['count']++;

        if ($freq[$key]['count'] > $bestCount) {
            $bestCount = $freq[$key]['count'];
            $bestKey = $key;
        }
    }

    return $bestKey !== null ? $freq[$bestKey]['value'] : null;
}
```

Complexity:

- Time: `O(n)`
- Space: `O(k)`, where `k` is number of distinct elements

Tie behavior: this implementation returns the first element that reaches the highest frequency.

</details>

<details>
<summary>90. How would you design a high-load PHP system?</summary>

#### PHP

For high-load PHP systems, the core principle is to make the application stateless, move heavy work out of request path, and scale horizontally behind reliable infrastructure.

1. **Architecture baseline**

- Stateless PHP app instances behind a load balancer.
- Nginx/Envoy + PHP-FPM (or RoadRunner/Swoole when justified).
- Separate data, cache, queue, and object storage layers.

2. **Data strategy**

- Primary DB + read replicas; split read/write paths.
- Proper indexing, query optimization, and slow-query monitoring.
- Partitioning/sharding only when single-node scaling is exhausted.

3. **Caching layers**

- CDN/edge cache for static and cacheable dynamic responses.
- Redis/Memcached for application data and hot query results.
- Clear cache invalidation policy (TTL + event-based invalidation).

4. **Asynchronous processing**

- Offload expensive tasks to queues (emails, reports, media processing).
- Use idempotent workers with retries and dead-letter queues.
- Keep HTTP requests short and predictable.

5. **Reliability and resiliency**

- Timeouts, circuit breakers, bulkheads for external dependencies.
- Graceful degradation when non-critical services fail.
- Health checks, auto-restarts, and rolling deployments.

6. **Observability**

- Centralized logs with correlation IDs.
- Metrics: p95/p99 latency, error rate, queue lag, DB/cache saturation.
- Tracing for multi-service request paths.

7. **Operational practices**

- Capacity planning and load testing before peak events.
- Blue-green/canary releases to reduce risk.
- Security hardening and rate limiting at edge and app levels.

A scalable PHP design is mostly an infrastructure and architecture discipline: stateless app tier, efficient data access, aggressive caching, and async background execution.

</details>

<details>
<summary>91. How would you scale PHP horizontally?</summary>

#### PHP

Horizontal scaling in PHP means adding more identical app nodes and making sure any request can be served by any node without relying on local state.

1. **Make application tier stateless**

- Store sessions in Redis/DB, not on local disk.
- Move uploaded files to shared/object storage (e.g., S3-compatible).
- Keep node-local caches as optional, not a source of truth.

2. **Put nodes behind a load balancer**

- Use L4/L7 load balancer (Nginx, HAProxy, cloud LB).
- Enable health checks and automatic unhealthy-node removal.
- Sticky sessions are a temporary workaround; prefer truly stateless design.

3. **Scale read-heavy dependencies**

- Add DB read replicas and route read traffic appropriately.
- Add distributed cache (Redis/Memcached) to offload primary DB.
- Use CDN for static assets and cacheable responses.

4. **Control background workloads**

- Use queue-based workers for heavy jobs.
- Scale workers independently from HTTP app nodes.
- Make jobs idempotent and retry-safe.

5. **Standardize runtime with containers/images**

- Immutable images for consistent deployments.
- Autoscaling policies based on CPU, memory, and latency signals.
- Centralized config/secrets management.

6. **Observability and scaling signals**

- Track p95/p99 latency, saturation, error rate, queue lag.
- Monitor DB connection pool pressure and cache hit ratio.
- Use these metrics to trigger autoscaling and capacity planning.

In practice, PHP horizontal scaling is straightforward when state is externalized and infrastructure handles distribution, health, and elasticity.

</details>

<details>
<summary>92. How would you handle millions of users?</summary>

#### PHP

Handling millions of users is a system design task, not a single PHP trick. The solution is layered scaling across edge, app, data, and operations.

1. **Traffic distribution and edge**

- Global CDN for static assets and cacheable API responses.
- Load balancers with autoscaled stateless PHP app nodes.
- Rate limiting and bot protection at edge.

2. **Application architecture**

- Split monolith bottlenecks into bounded services when needed.
- Keep synchronous request path minimal; move heavy tasks to queues.
- Use idempotency keys for critical write operations.

3. **Data layer at scale**

- Primary DB for writes, multiple read replicas for read traffic.
- Aggressive indexing and query tuning; avoid ORM anti-patterns.
- Partitioning/sharding for very large datasets and hot tenants.

4. **Caching strategy**

- Multi-layer cache: CDN -> Redis/Memcached -> DB.
- Cache hot objects, computed views, and expensive queries.
- Strong invalidation rules to prevent stale critical data.

5. **Asynchronous and event-driven processing**

- Queue workers for emails, notifications, media, analytics pipelines.
- Retry with backoff, dead-letter queues, and idempotent handlers.
- Stream events for downstream consumers instead of blocking requests.

6. **Reliability and resilience**

- Graceful degradation for non-essential features under pressure.
- Timeout budgets and circuit breakers for dependencies.
- Multi-AZ deployment and tested failover procedures.

7. **Observability and capacity discipline**

- SLOs for latency/error; track p95/p99 and saturation.
- Continuous load/stress testing before major launches.
- Capacity forecasting from real usage patterns.

At "millions" scale, success comes from predictable architecture, controlled data growth, and strong operational practices more than language-level optimizations.

</details>

<details>
<summary>93. How would you design caching strategy?</summary>

#### PHP

A good caching strategy starts from access patterns and consistency requirements, not from technology choice alone.

1. **Define what to cache**

- Expensive DB query results.
- Aggregated/computed API responses.
- Session and authorization context (when safe).
- Static/config/reference data with low change frequency.

2. **Use multi-layer caching**

- Edge/CDN cache for static assets and cacheable HTTP responses.
- Application cache (Redis/Memcached) for hot objects and query results.
- In-process/opcache optimizations for code and immutable config.

3. **Choose proper cache patterns**

- Cache-aside for read-heavy data (most common).
- Write-through/write-behind for specific consistency/performance cases.
- Read-through if cache provider supports transparent loading.

4. **Design keys and TTLs carefully**

- Namespaced keys: `entity:{id}:v{version}`.
- Different TTLs by data volatility and business criticality.
- Add jitter to TTL to reduce thundering herd.

5. **Handle invalidation explicitly**

- Event-driven invalidation after writes.
- Versioned keys for easy logical invalidation.
- Tag-based invalidation when supported.

6. **Protect against cache failures**

- Fallback path if cache is down (degraded but functional).
- Request coalescing/locking to prevent stampede.
- Warm-up for critical keys after deploy/restart.

7. **Measure and tune continuously**

- Monitor hit ratio, latency, eviction rate, memory pressure.
- Track stale-read incidents and cache-miss cost.
- Optimize based on real production traces.

Strong caching strategy is a balance: maximize hit rate and latency gains while preserving correctness and predictable invalidation behavior.

</details>

<details>
<summary>94. How do modern PHP frameworks (Laravel, Symfony) differ internally?</summary>

#### PHP

Laravel and Symfony share many foundations (HTTP request lifecycle, DI, middleware/event concepts), but differ in architecture philosophy, defaults, and extension model.

1. **Core philosophy**

- Symfony: component-first, explicit configuration, high composability.
- Laravel: integrated developer experience, convention-heavy defaults, faster delivery out of the box.

2. **Dependency Injection and container**

- Symfony has a compiled DI container with strong compile-time validation and optimization.
- Laravel uses a highly dynamic service container with runtime resolution and auto-wiring patterns tailored for developer ergonomics.

3. **Configuration model**

- Symfony: configuration-centric (`yaml/xml/php`), environment-specific bundles, explicit wiring.
- Laravel: convention + service providers + facades; many features enabled with minimal config.

4. **HTTP pipeline internals**

- Symfony request flow is centered on `HttpKernel` and event dispatcher listeners.
- Laravel request flow is middleware pipeline oriented with expressive route/controller integration.

5. **ORM/data layer defaults**

- Symfony commonly uses Doctrine ORM (Data Mapper pattern, explicit unit-of-work behavior).
- Laravel ships with Eloquent (Active Record pattern, rapid CRUD ergonomics).

6. **Ecosystem structure**

- Symfony components are widely reused standalone across PHP ecosystem.
- Laravel ecosystem is tightly integrated (queues, jobs, scheduler, Horizon, Nova-like tooling patterns).

7. **Performance and production profile**

- Both can be production-grade at scale.
- Symfony often emphasizes predictability and explicit control in large enterprise systems.
- Laravel emphasizes speed of implementation and cohesive developer workflow.

In short: Symfony optimizes for explicit architecture and component composition; Laravel optimizes for integrated productivity and fast feature delivery.

</details>

<details>
<summary>95. How does routing work in frameworks?</summary>

#### PHP

Routing maps an incoming HTTP request to a specific handler (controller/action/closure) using method, path pattern, host, and optional constraints.

1. **Route definition phase**

- Framework loads route table at boot (from files/attributes/annotations).
- Each route stores method(s), path pattern, handler, middleware, and metadata.
- Many frameworks precompile/caches route definitions for faster lookup.

2. **Request matching phase**

- Router receives normalized request path + method.
- It tries to match static routes first, then dynamic parameterized routes.
- Constraints (regex, host, scheme, locale) are validated.

3. **Parameter extraction**

- Dynamic segments like `/users/{id}` are extracted from path.
- Values are cast/validated (explicitly or via framework binding rules).
- Optional defaults are applied for missing optional parameters.

4. **Middleware and guards**

- Before handler execution, route/group/global middleware chain runs.
- Typical checks: auth, rate limiting, CSRF, permissions, tenant resolution.
- Middleware can short-circuit and return response early.

5. **Controller dispatch**

- Container resolves controller dependencies.
- Route params + injected services are passed to action method.
- Action returns response object/data for serialization.

6. **Reverse routing**

- Framework can generate URLs from route names + params.
- This avoids hardcoded URLs and improves refactor safety.

7. **Performance considerations**

- Route cache/precompilation in production.
- Prefer specific/static routes over overly broad wildcard patterns.
- Keep middleware chain minimal for hot endpoints.

Internally, routing is essentially an indexed pattern-matching and dispatch pipeline wrapped with middleware and dependency injection.

</details>

<details>
<summary>96. How does middleware pipeline work internally?</summary>

#### PHP

Middleware pipeline is a chain-of-responsibility: each middleware receives the request and a "next" callable, then either passes control forward or returns a response immediately.

1. **Pipeline construction**

- Framework collects global, group, and route-specific middleware.
- Middleware order is resolved (priority rules may apply).
- A final destination handler (controller/action) is set as the last step.

2. **Execution model**

- Middleware signature is conceptually: `handle(Request $request, Closure $next): Response`.
- Middleware can do pre-processing, then call `$next($request)`.
- After next returns, middleware can do post-processing on response.

3. **Short-circuit behavior**

- Middleware may return a response without calling `$next`.
- Typical cases: auth failure, CSRF failure, rate-limit exceeded, maintenance mode.
- This prevents downstream middleware/controller execution.

4. **Nested call stack**

- The chain is often built by wrapping closures from last to first.
- Execution "goes down" request path, then "unwinds" response path.
- This enables cross-cutting concerns like logging, timing, header injection.

5. **Error and exception handling**

- Exception middleware/handler can catch and normalize errors.
- Some frameworks place error handling outside the middleware stack as top-level kernel logic.
- Consistent error mapping keeps API responses predictable.

6. **Common middleware responsibilities**

- Authentication/authorization checks.
- Request validation/sanitization.
- Rate limiting and anti-abuse controls.
- Tracing, logging, metrics, correlation IDs.
- CORS/security headers and response transformation.

7. **Performance considerations**

- Keep the chain minimal on hot routes.
- Put cheap reject-fast checks early.
- Avoid heavy synchronous I/O in generic middleware.

Internally, middleware is just an ordered callable composition that centralizes cross-cutting concerns around request/response flow.

</details>

<details>
<summary>97. How does dependency resolution work under the hood?</summary>

#### PHP

Dependency resolution in modern PHP frameworks is performed by a DI container that builds objects based on bindings and constructor metadata, usually via reflection and cached definitions.

1. **Container bindings**

- Interfaces/abstracts are mapped to concrete implementations.
- Bindings can be singleton, scoped, or transient.
- Factories/closures may define custom construction logic.

2. **Resolution request**

- Framework asks container for a type (controller, service, middleware, etc.).
- Container checks if instance already exists (for singleton/scoped lifetimes).
- If not, it starts building the object graph.

3. **Constructor introspection**

- Container inspects constructor parameters (reflection or compiled metadata).
- For class-typed params, it recursively resolves dependencies.
- For scalars/config values, it uses explicit parameters, env/config bindings, or default values.

4. **Recursive object graph build**

- Dependencies are resolved depth-first.
- Circular dependency detection prevents infinite recursion.
- Optional dependencies can be nullable/defaulted if not bound.

5. **Lifecycle and caching**

- Singletons are cached after first creation.
- Scoped instances are cached per request/job scope.
- Some containers compile metadata for faster production resolution.

6. **Method/action injection**

- Beyond constructors, frameworks may inject dependencies into controller actions, command handlers, and middleware methods.
- Route params and container services are merged during dispatch.

7. **Failure modes**

- Unbound interface/abstract.
- Ambiguous or non-instantiable dependency chain.
- Scalar constructor params without defaults/bindings.
- Circular dependencies between services.

Under the hood, DI resolution is deterministic graph construction with lifecycle rules, reflection/metadata, and caching for performance.

</details>

<details>
<summary>98. What are best practices for modern PHP development in 2026?</summary>

#### PHP

Modern PHP best practices in 2026 focus on strict engineering discipline: strong typing, automated quality gates, secure defaults, and observable production systems.

1. **Use current language features intentionally**

- `declare(strict_types=1);` in application code.
- Typed properties, return types, enums, readonly/value-object patterns.
- Prefer explicit contracts over dynamic magic where possible.

2. **Architecture and code organization**

- Modular boundaries (domain/application/infrastructure or equivalent).
- Clear separation of business logic from framework glue code.
- Dependency inversion with interfaces for testability.

3. **Quality automation**

- CI with static analysis (PHPStan/Psalm) at high strictness.
- Consistent coding style via PHP-CS-Fixer/Pint.
- Unit + integration + contract tests with realistic fixtures.

4. **Performance and runtime efficiency**

- PHP 8.3/8.4+ with OPcache and tuned FPM/process manager settings.
- Profile first (Blackfire/XHProf/APM), then optimize hotspots.
- Use caching/queues to keep synchronous request path lean.

5. **Security by default**

- Prepared statements, contextual output escaping, CSRF protection.
- Secrets management outside repo; key rotation and least privilege.
- Dependency vulnerability scanning in CI.

6. **Operational maturity**

- Structured logs, metrics, tracing, correlation IDs.
- SLO-driven monitoring with alert fatigue control.
- Safe releases: canary/blue-green and rollback procedures.

7. **Dependency and ecosystem hygiene**

- Keep Composer dependencies current with controlled upgrade cadence.
- Pin and audit critical packages.
- Avoid unnecessary framework coupling in core domain code.

8. **Team conventions**

- ADRs for major decisions and clear code review standards.
- Backward compatibility rules for public/internal APIs.
- Documentation close to code for onboarding and incident response.

The strongest PHP teams in 2026 treat codebase health as a product: typed, tested, observable, and continuously improved.

</details>

<details>
<summary>99. What tools are essential for modern PHP developer?</summary>

#### PHP

An effective modern PHP toolkit covers coding, quality, debugging, delivery, and operations.

1. **Core language and package management**

- PHP 8.3/8.4+ runtime.
- Composer for dependencies and autoloading.
- Local environment tooling: Docker/DDEV/Lando or native reproducible setup.

2. **Code quality and static analysis**

- PHPStan or Psalm for static analysis.
- PHP-CS-Fixer or Pint for coding standards.
- PHP_CodeSniffer where custom standards are needed.

3. **Testing stack**

- PHPUnit or Pest for unit/integration tests.
- Mocking/test doubles libraries as needed.
- Coverage reporting integrated into CI.

4. **Debugging and profiling**

- Xdebug for step debugging.
- Blackfire/Tideways/XHProf/APM profiler for performance bottlenecks.
- Structured logging tools and centralized log viewer.

5. **Framework and DX tooling**

- Laravel Artisan or Symfony Console tooling.
- Framework-specific debug/profiler utilities.
- API tools: Postman/Insomnia + OpenAPI validation.

6. **Data and infrastructure tools**

- Redis and DB CLI tools (`redis-cli`, `psql`, `mysql`) for diagnostics.
- Queue/worker monitoring dashboards.
- Migration and schema management tooling.

7. **CI/CD and automation**

- GitHub Actions/GitLab CI or equivalent.
- Automated lint, static analysis, test, security scan gates.
- Deployment automation with rollback capability.

8. **Security and dependency hygiene**

- `composer audit` and/or SCA scanners.
- Secret scanning and pre-commit hooks.
- SAST/DAST where risk profile requires it.

9. **Observability and operations**

- Metrics, tracing, and alerting stack (Prometheus/Grafana/APM).
- Error tracking (Sentry/Bugsnag).
- Log correlation with request IDs.

The essential set is the one that enforces fast feedback loops: code quality checks, reliable tests, safe delivery, and production visibility.

</details>

<details>
<summary>100. How do you keep PHP codebase maintainable long-term?</summary>

#### PHP

Long-term maintainability is achieved by combining technical standards, architectural discipline, and continuous operational feedback.

1. **Keep architecture explicit**

- Enforce clear module boundaries and ownership.
- Separate domain logic from framework/infrastructure details.
- Minimize hidden coupling and global state.

2. **Prioritize readability over cleverness**

- Small focused classes/functions with clear naming.
- Consistent conventions across the codebase.
- Prefer explicit behavior over magic abstractions.

3. **Treat type safety seriously**

- `strict_types=1` where feasible.
- Strong typing for params/returns/properties.
- Static analysis (PHPStan/Psalm) as mandatory CI gate.

4. **Build a resilient test portfolio**

- Fast unit tests for core logic.
- Integration tests for DB/external boundaries.
- Contract tests for APIs/events shared with other services.

5. **Control dependencies and upgrades**

- Regular dependency update cadence instead of rare big-bang upgrades.
- Changelogs and deprecation tracking for framework/runtime changes.
- Remove unused packages and dead abstractions proactively.

6. **Design for safe change**

- Backward compatibility rules for public APIs.
- Feature flags for risky rollouts.
- Migrations and data changes with rollback/repair plans.

7. **Institutionalize code quality process**

- Code review checklist (correctness, security, performance, readability).
- Automated formatting/linting to reduce review noise.
- ADRs for major decisions to preserve context over time.

8. **Operational feedback loop**

- Production observability: logs, metrics, tracing, error tracking.
- Post-incident reviews feeding concrete code/process improvements.
- SLO-based prioritization to keep reliability visible.

9. **Protect team continuity**

- Up-to-date docs for setup, architecture, and runbooks.
- Onboarding guides and shared engineering standards.
- Reduce "single expert" risk via knowledge sharing and rotation.

A maintainable PHP codebase is not static; it is continuously curated through standards, automation, and deliberate simplification.

</details>
