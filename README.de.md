**Read in other languages: [English 🇺🇸](README.en.md),
[Polska 🇵🇱](README.pl.md), [German 🇩🇪](README.de.md), [French 🇫🇷](README.fr.md),
[Spanish 🇪🇸](README.es.md), [Українська 🇺🇦](README.md).**

<h1>
  Laravel <img src="./assets/laravel.svg" width="40" height="40" alt="Laravel logo"/>
</h1>

<h2>Die beliebtesten Laravel-Interviewfragen und Antworten</h2>

<details>
<summary>1. Was ist Laravel und warum wird es verwendet?</summary>

#### Laravel

Laravel ist ein modernes PHP-Webframework mit Fokus auf Entwicklerproduktivität, saubere Architektur und wartbaren Code.

1. **Was Laravel ist**

- Ein Open-Source-Framework, das auf Symfony-Komponenten aufbaut.
- Meinungsstark genug für gute Standards, aber flexibel für individuelle Architektur.

2. **Warum es verwendet wird**

- Beschleunigt die Entwicklung durch integriertes Routing, Validierung, Authentifizierung, Queues, Mail, Events und Caching.
- Fördert sauberen Code durch Service Container, Middleware, Eloquent ORM und Test-Tools.
- Bietet First-Party-Werkzeuge (`Artisan`, Migrationen, Scheduler, Horizon, Telescope) für produktionsreife Anwendungen.

3. **Typische Einsatzfälle**

- REST-APIs und Backend-Services.
- Serverseitig gerenderte Webanwendungen.
- Admin-Panels, SaaS-Produkte und Marktplatz-Plattformen.
- Hintergrundverarbeitung von Jobs und Integrationen mit Drittanbieterdiensten.

Kurz gesagt: Laravel wird eingesetzt, um sichere, skalierbare und wartbare PHP-Anwendungen schneller und mit weniger Boilerplate zu entwickeln.

</details>

<details>
<summary>180. Was ist Composer-Autoloading und wie funktioniert PSR-4?</summary>

#### PHP

Composer-Autoloading lädt Klassen automatisch, ohne manuelle `require/include`-Aufrufe. PSR-4 definiert dabei den Standard für die Zuordnung von Namespaces zu Verzeichnissen.

1. **Composer-Autoloading**

- Composer erzeugt einen Autoloader aus der Projekt-/Paketkonfiguration.
- Klassen werden bei Bedarf dynamisch geladen.

2. **PSR-4-Prinzip**

- Ein Namespace-Präfix wird einem Basisverzeichnis zugeordnet.
- Namespace-Segmente entsprechen Unterordnern.
- Der Klassenname entspricht dem Dateinamen.

3. **Beispiel**

- `App\\` -> `app/`
- `App\\Services\\BillingService` -> `app/Services/BillingService.php`

Composer + PSR-4 bilden die Grundlage für strukturierte, wartbare PHP/Laravel-Codebasen.

</details>

<details>
<summary>129. Wie verbessern Factories das Testen?</summary>

#### Laravel

Factories beschleunigen Test-Setup und erhöhen die Lesbarkeit.

1. Weniger Boilerplate für Testdaten.
2. Szenarien über States klar ausdrückbar.
3. Beziehungen zwischen Modellen schnell aufbaubar.

Sie helfen, Tests auf Verhalten statt auf Setup-Code zu fokussieren.

</details>

<details>
<summary>130. Wie testet man APIs in Laravel?</summary>

#### Laravel

API-Tests erfolgen mit HTTP-Helpers und klaren Assertions.

1. `getJson`, `postJson`, `putJson`, `deleteJson`.
2. Statuscodes und JSON-Struktur prüfen.
3. Auth/Permissions und Datenbank-Side-Effects validieren.

Gute API-Tests decken sowohl Happy Path als auch Fehlerpfade ab.

</details>

<details>
<summary>131. Wie fake’t man Queues, Events, Notifications und Mail in Tests?</summary>

#### Laravel

Laravel bietet eingebaute Fakes für schnelle, deterministische Tests.

1. `Queue::fake()` + `assertPushed(...)`
2. `Event::fake()` + `assertDispatched(...)`
3. `Notification::fake()` + `assertSentTo(...)`
4. `Mail::fake()` + `assertSent(...)`

So testest du Orchestrierung, ohne reale Side-Effects auszuführen.

</details>

<details>
<summary>132. Was ist Pest PHP und warum ist es in Laravel beliebt?</summary>

#### Laravel

Pest ist ein Test-Framework auf PHPUnit-Basis mit prägnanter Syntax.

1. Weniger Boilerplate, bessere Lesbarkeit.
2. Starke Laravel-Integration.
3. Volle Nutzung des PHPUnit-Ökosystems.

Pest ist beliebt, weil es Tests schneller und angenehmer macht.

</details>

<details>
<summary>133. Was ist Mocking in Laravel-Tests?</summary>

#### Laravel

Mocking ersetzt reale Abhängigkeiten durch kontrollierte Test Doubles.

1. Isoliert die Unit unter Test.
2. Simuliert Fehlerpfade.
3. Prüft Interaktionsverträge zwischen Komponenten.

Mocking ergänzt Unit-Tests und sollte mit Integrations-/Feature-Tests kombiniert werden.

</details>

<details>
<summary>91. Wie funktioniert Concurrency in Queues?</summary>

#### Laravel

Queue-Concurrency entsteht, wenn mehrere Worker parallel Jobs ausführen.

1. Mehr Worker-Prozesse erhöhen den Durchsatz.
2. Priorisierte Queues (`high`, `default`, `low`) helfen bei Laststeuerung.
3. Korrektheit braucht idempotente Jobs und sauberes State-Handling.

Concurrency verbessert Performance, erfordert aber saubere Nebenläufigkeitsstrategie.

</details>

<details>
<summary>92. Was ist Idempotenz bei Queue-Jobs?</summary>

#### Laravel

Idempotenz bedeutet: Mehrfache Ausführung eines Jobs führt zum gleichen Endergebnis wie eine einmalige Ausführung.

1. Wichtig wegen Retries und möglicher Doppel-Dispatches.
2. Umsetzung über Idempotency Keys, Zustandsprüfungen und DB-Constraints.
3. Besonders relevant bei Zahlungen, E-Mails, externen APIs.

Idempotenz ist essenziell für zuverlässige asynchrone Verarbeitung.

</details>

<details>
<summary>93. Wie funktioniert Caching in Laravel?</summary>

#### Laravel

Laravel speichert häufig benötigte oder teure Ergebnisse im Cache, um wiederholte Berechnungen/Queries zu vermeiden.

1. Typisches Muster: `remember()` (Cache-aside).
2. Unterstützt verschiedene Backends wie Redis/Memcached/Datei/DB.
3. Reduziert Latenz und Datenbanklast deutlich.

Caching ist ein zentraler Performance-Hebel in Laravel-Anwendungen.

</details>

<details>
<summary>94. Welche Cache-Treiber sind verfügbar?</summary>

#### Laravel

Gängige Cache-Treiber in Laravel:

1. `array`
2. `file`
3. `database`
4. `redis`
5. `memcached`
6. `dynamodb` (bei entsprechender Konfiguration)
7. `null`

Für produktive High-Load-Umgebungen werden typischerweise Redis oder Memcached genutzt.

</details>

<details>
<summary>95. Welche Caching-Strategien würdest du in einer High-Load-Laravel-Anwendung einsetzen?</summary>

#### Laravel

1. Cache-aside (`remember`) für teure Reads.
2. Gezielte Invalidation statt globalem Flush.
3. Schutz vor Cache-Stampede (Locks/Jitter).
4. Mehrstufiges Caching (App + CDN/HTTP, wo sinnvoll).
5. Monitoring von Hit-Rate, Latenz und Speicherverbrauch.

Bei High-Load sind Invalidation-Strategie und Observability genauso wichtig wie Cache-Geschwindigkeit.

</details>

<details>
<summary>96. Was sind Cache Tags?</summary>

#### Laravel

Cache Tags gruppieren Cache-Einträge logisch, damit zusammengehörige Keys gemeinsam invalidiert werden können.

1. Erlaubt präzises Löschen statt Full-Flush.
2. Nützlich für tenant-/domänenspezifische Gruppen.
3. Unterstützt nur bestimmte Treiber (typisch Redis/Memcached).

Cache Tags verbessern die Wartbarkeit von Cache-Invalidierung.

</details>

<details>
<summary>97. Wie leert und wärmt man den Cache auf?</summary>

#### Laravel

1. **Leeren**

```bash
php artisan cache:clear
php artisan config:clear
php artisan route:clear
php artisan view:clear
```

2. **Build/Optimize**

```bash
php artisan config:cache
php artisan route:cache
php artisan view:cache
```

3. **Warm-up**

- Nach Deploy gezielt Hot Keys vorladen, um Cold-Start-Latenz zu vermeiden.

</details>

<details>
<summary>89. Was ist Laravel Horizon?</summary>

#### Laravel

Laravel Horizon ist ein Monitoring- und Management-Dashboard für Redis-basierte Queues.

1. **Was Horizon zeigt**

- Durchsatz, Laufzeiten, Wartezeiten und Fehler.
- Status von Workern/Supervisors.

2. **Wofür es nützlich ist**

- Schnelle Diagnose von Queue-Engpässen.
- Bessere Betriebsübersicht für asynchrone Workloads.
- Feineres Tuning von Queue-Performance.

3. **Typischer Einsatz**

- Production-Observability für Redis-Queues.

Horizon ist der Standard für Queue-Operations im Laravel-Redis-Umfeld.

</details>

<details>
<summary>88. Was ist Laravel Reverb und warum ist es in modernem Laravel wichtig?</summary>

#### Laravel

Laravel Reverb ist Laravels First-Party-WebSocket-Server für Realtime-Broadcasting.

1. **Was Reverb bietet**

- Native WebSocket-Infrastruktur im Laravel-Ökosystem.
- Direkte Integration mit Broadcasting, Channel-Auth und Echo.

2. **Warum es wichtig ist**

- Weniger Abhängigkeit von externen Realtime-Diensten.
- Bessere Konsistenz zwischen lokaler Entwicklung und Produktion.
- Mehr Kontrolle über Skalierung und Betrieb.

3. **Typische Anwendungsfälle**

- Realtime-Benachrichtigungen.
- Live-Collaboration.
- Event-getriebene Dashboards.

Reverb ist ein zentraler Baustein für moderne Realtime-Architekturen mit Laravel.

</details>

<details>
<summary>87. Wie funktioniert Laravel Echo?</summary>

#### Laravel

Laravel Echo ist eine JavaScript-Client-Bibliothek, die Broadcast-Channels abonniert und Laravel-Events im Frontend verarbeitet.

1. **Rolle im Realtime-Stack**

- Komfortable API für WebSocket-Subscriptions.
- Saubere Integration mit Laravel-Channel- und Event-Konventionen.

2. **Ablauf**

- Echo wird mit Broadcaster-Konfiguration initialisiert.
- Client tritt Channels bei (`channel`, `private`, `presence`).
- Event-Callbacks aktualisieren die UI in Echtzeit.

3. **Beispiel**

```js
Echo.private(`orders.${orderId}`)
  .listen('OrderShipped', (payload) => {
    // UI aktualisieren
  });
```

Echo ist die Standard-Bridge zwischen Laravel Broadcasting und dem Browser.

</details>

<details>
<summary>86. Was ist Laravel Broadcasting?</summary>

#### Laravel

Laravel Broadcasting ist die Echtzeit-Schicht von Laravel, um serverseitige Events über WebSockets (oder kompatible Treiber) an Clients auszuliefern.

1. **Wofür es genutzt wird**

- Live-Benachrichtigungen.
- Chat und Presence-Status.
- Realtime-Dashboards.

2. **Kernkonzepte**

- Channel-Typen: `public`, `private`, `presence`.
- Autorisierung für private/presence Channels.
- Broadcastbare Event-Klassen.

3. **Ablauf**

- Backend dispatcht ein Event.
- Broadcast-Treiber sendet es an die Realtime-Infrastruktur.
- Frontend (meist Laravel Echo) empfängt und aktualisiert die UI.

Broadcasting ermöglicht reaktive UX ohne starkes Polling.

</details>

<details>
<summary>85. Was ist eventgetriebene Architektur in Laravel?</summary>

#### Laravel

Eventgetriebene Architektur (EDA) organisiert Anwendungsvorgänge rund um Events und entkoppelte Reaktionen durch Listener.

1. **Prinzip**

- Wichtige fachliche Ereignisse werden als Events veröffentlicht.
- Unabhängige Listener reagieren darauf.

2. **Vorteile**

- Geringere Kopplung zwischen Modulen.
- Leichtere Erweiterbarkeit.
- Gute Skalierbarkeit mit queued Listenern.

3. **Typischer Ablauf**

- Kernaktion passiert (z. B. `OrderPaid`).
- Mehrere Listener erledigen Folgeaktionen (Mail, Analytics, Integrationen).

EDA hilft, Laravel-Systeme modular und langfristig wartbar zu gestalten.

</details>

<details>
<summary>81. Was ist Job-Batching?</summary>

#### Laravel

Job-Batching fasst viele Jobs zu einer logisch zusammengehörigen Einheit zusammen, die als Batch überwacht und gesteuert werden kann.

1. **Was es ermöglicht**

- Mehrere Jobs gesammelt dispatchen.
- Fortschritt, Erfolg und Fehler batchweise verfolgen.
- Callbacks wie `then`, `catch`, `finally` nutzen.

2. **Typische Anwendungsfälle**

- Große Importe/Exporte.
- Reindexing-Operationen.
- Fan-out-Prozesse mit Gesamtstatus.

3. **Vorteile**

- Bessere Observability und Steuerung.
- Klarere Orchestrierung komplexer Multi-Job-Abläufe.

Batching ist ideal, wenn viele parallele Jobs zu einem Business-Prozess gehören.

</details>

<details>
<summary>79. Was ist der Unterschied zwischen den Queue-Treibern sync, database, Redis und SQS?</summary>

#### Laravel

Diese Treiber unterscheiden sich in Ausführungsmodell, Performance und Betriebsaufwand.

1. **`sync`**

- Führt Jobs sofort im aktuellen Request aus.
- Keine asynchrone Entkopplung.

2. **`database`**

- Speichert Jobs in einer DB-Tabelle.
- Einfach einzurichten, aber bei hoher Last begrenzter.

3. **`redis`**

- Schneller In-Memory-Treiber.
- Sehr gut für hohe Durchsätze.

4. **`sqs`**

- Managed Queue-Service von AWS.
- Hohe Skalierbarkeit und Zuverlässigkeit für verteilte Systeme.

5. **Faustregel**

- Klein/Einfach: `database`
- Hohe Last: `redis`
- AWS-native verteilte Architektur: `sqs`
- Lokale/synchrone Ausführung: `sync`

</details>

<details>
<summary>78. Welche Queue-Treiber stehen in Laravel zur Verfügung?</summary>

#### Laravel

Laravel unterstützt mehrere Queue-Backends über konfigurierbare Treiber.

1. **Gängige Treiber**

- `sync`
- `database`
- `redis`
- `sqs`
- `null`

2. **Kurzprofil**

- `sync`: sofortige Ausführung im aktuellen Prozess.
- `database`: persistiert Jobs in Tabellen.
- `redis`: schneller In-Memory-Queue-Treiber.
- `sqs`: skalierbarer Managed-Cloud-Queue-Service.

3. **Konfiguration**

- In `config/queue.php` und über Environment-Variablen.

Die Wahl des Treibers hängt von Lastprofil, Betriebsmodell und Infrastruktur ab.

</details>

<details>
<summary>77. Was sind Jobs und Queue-Worker?</summary>

#### Laravel

Jobs und Worker bilden das Kernmodell für asynchrone Verarbeitung in Laravel.

1. **Jobs**

- Kapseln eine konkrete Aufgabe (typisch in `app/Jobs`).
- Werden für sofortige oder verzögerte Ausführung dispatcht.
- Implementieren für Queue-Verarbeitung häufig `ShouldQueue`.

2. **Queue-Worker**

- Laufende Prozesse, die Jobs aus der Queue abarbeiten.
- Werden z. B. mit `php artisan queue:work` gestartet.

3. **Ablauf**

- Job wird dispatcht.
- Payload landet im Queue-Backend.
- Worker liest den Job und führt `handle()` aus.

In Production werden Worker üblicherweise durch Supervisor/systemd verwaltet.

</details>

<details>
<summary>76. Erkläre das Queue-System in Laravel.</summary>

#### Laravel

Das Laravel-Queue-System verlagert zeitintensive Aufgaben aus dem HTTP-Request in asynchrone Hintergrundverarbeitung.

1. **Warum Queues**

- Schnellere Antwortzeiten für Nutzer.
- Bessere Skalierbarkeit.
- Zuverlässige Ausführung mit Retry-Mechanismen.

2. **Ablauf**

- Anwendung dispatcht einen Job in ein Queue-Backend.
- Worker konsumiert den Job und führt ihn aus.
- Fehlgeschlagene Jobs können gespeichert und erneut ausgeführt werden.

3. **Typische Queue-Tasks**

- E-Mails, Benachrichtigungen, Reports.
- Externe API-Integrationen.
- Datei-/Medienverarbeitung.

Queues sind zentral für performante und robuste Laravel-Anwendungen.

</details>

<details>
<summary>75. Was sind verschlüsselte Cookies und signierte Cookies?</summary>

#### Laravel

Verschlüsselte und signierte Cookies schützen beide vor Manipulation, aber nur verschlüsselte Cookies schützen zusätzlich den Inhalt vor Einsicht.

1. **Verschlüsselte Cookies**

- Wert wird verschlüsselt und integritätsgeschützt.
- Client kann den Originalinhalt nicht lesen.

2. **Signierte Cookies**

- Wert kann lesbar bleiben, ist aber signiert.
- Manipulation wird erkannt, Inhalt jedoch nicht verborgen.

3. **Laravel-Praxis**

- Im typischen Laravel-Webstack werden App-Cookies standardmäßig verschlüsselt.

4. **Sicherheitsattribute**

- Immer `Secure`, `HttpOnly` und passende `SameSite`-Einstellung nutzen.

In der Praxis sind verschlüsselte Cookies meist die sicherere Standardwahl.

</details>

<details>
<summary>74. Wie funktionieren signierte URLs in Laravel?</summary>

#### Laravel

Signierte URLs enthalten eine kryptografische Signatur, die nachweist, dass die URL von deiner Anwendung stammt und nicht manipuliert wurde.

1. **Was geschützt wird**

- Integrität von Pfad und Query-Parametern.
- Optional ein Ablaufzeitpunkt für temporäre Links.

2. **Signierte URL erzeugen**

```php
$url = URL::signedRoute('unsubscribe', ['user' => $user->id]);
$temporary = URL::temporarySignedRoute('download', now()->addMinutes(30), ['file' => $fileId]);
```

3. **Signatur prüfen**

- Über Middleware `signed` oder Request-Validierung.

```php
Route::get('/unsubscribe/{user}', UnsubscribeController::class)
    ->name('unsubscribe')
    ->middleware('signed');
```

4. **Typische Anwendungsfälle**

- Abmeldelinks.
- E-Mail-Verifizierungsaktionen.
- Zeitlich begrenzte Download-/Aktionslinks.

Signierte URLs sind ein einfacher, wirksamer Schutz für öffentliche Aktionslinks.

</details>

<details>
<summary>73. Welche Security Best Practices sollte jede Laravel-Anwendung befolgen?</summary>

#### Laravel

Sicherheit in Laravel ist ein mehrschichtiger Ansatz aus Code-, Infrastruktur- und Betriebsdisziplin.

1. **Auth & Access Control**

- Geschützte Routen absichern.
- Gates/Policies konsequent einsetzen.

2. **Input/Output-Sicherheit**

- Eingaben validieren.
- Ausgaben standardmäßig escapen.
- Keine unsichere raw SQL-Konkatenation.

3. **Session/Cookie-Härtung**

- `HttpOnly`, `Secure`, `SameSite` korrekt setzen.
- Session bei Login/Logout regenerieren.

4. **Secrets & Konfiguration**

- `.env` schützen.
- Credentials nicht in Git committen.
- Schlüssel regelmäßig rotieren.

5. **Transport & Header**

- HTTPS erzwingen.
- Sicherheitsheader (z. B. CSP, HSTS) setzen.

6. **Patch-Management**

- Laravel/PHP/Dependencies aktuell halten.

7. **Missbrauchsschutz**

- Rate Limiting für sensible Endpunkte.
- Logging/Monitoring für verdächtige Aktivitäten.

Sicherheit ist kein einzelnes Feature, sondern ein kontinuierlicher Prozess.

</details>

<details>
<summary>72. Wie werden Passwörter in Laravel gehasht?</summary>

#### Laravel

Laravel hasht Passwörter mit One-Way-Hashing über die `Hash`-Facade (nicht mit reversibler Verschlüsselung).

1. **Standardansatz**

- Verwendung moderner Algorithmen (typisch `bcrypt` oder `argon2id`, je nach Konfiguration).
- In der Datenbank wird nur der Hash gespeichert.

2. **Hash erzeugen**

```php
$hash = Hash::make($password);
```

3. **Passwort prüfen**

```php
if (Hash::check($plainPassword, $user->password)) {
    // valid
}
```

4. **Rehashing**

- `Hash::needsRehash()` hilft beim schrittweisen Upgrade von Hash-Parametern.

5. **Best Practices**

- Keine Klartextpasswörter speichern oder loggen.
- Starke Passwortregeln und Rate Limits für Login-Endpunkte.

</details>

<details>
<summary>71. Wie funktioniert Verschlüsselung in Laravel?</summary>

#### Laravel

Laravel stellt symmetrische Verschlüsselung über die `Crypt`-Facade bereit und nutzt dabei den Anwendungsschlüssel.

1. **Wie es funktioniert**

- Es wird der App-Key aus der Konfiguration verwendet.
- Daten werden verschlüsselt und mit Integritätsschutz versehen.
- Entschlüsselung ist nur mit dem passenden Schlüssel möglich.

2. **Typische Nutzung**

```php
$encrypted = Crypt::encryptString('secret-value');
$plain = Crypt::decryptString($encrypted);
```

3. **Wofür geeignet**

- Reversibel zu schützende sensible Daten.
- Bestimmte Framework-internen Anwendungsfälle (z. B. verschlüsselte Cookies).

4. **Wichtige Praxis**

- `APP_KEY` geheim halten.
- Schlüsselrotation geplant durchführen.
- Passwörter nicht verschlüsseln, sondern hashen.

</details>

<details>
<summary>69. Wie schützt Laravel vor CSRF-Angriffen?</summary>

#### Laravel

Laravel schützt vor CSRF, indem für zustandsändernde Web-Requests ein gültiges CSRF-Token verlangt wird.

1. **Funktionsweise**

- Pro Session wird ein Token erzeugt und serverseitig gespeichert.
- Formulare enthalten das Token via `@csrf`.
- Middleware validiert Token bei POST/PUT/PATCH/DELETE.

2. **Beispiel**

```blade
<form method="POST" action="/profile">
    @csrf
    <!-- fields -->
</form>
```

3. **Wichtig**

- Besonders relevant für Cookie-/Session-basierte Browser-Requests.
- Für stateless Bearer-Token-APIs meist nicht das primäre Schutzmittel.

CSRF-Protection ist ein zentraler Sicherheitslayer im Laravel-Webstack.

</details>

<details>
<summary>68. Wie schützt Laravel vor SQL Injection?</summary>

#### Laravel

Laravel schützt standardmäßig vor SQL Injection durch Parameter-Bindings und sichere Query-Abstraktionen.

1. **Prepared Statements / Bindings**

- Eloquent und Query Builder binden Werte als Parameter statt SQL-Strings zu konkatenieren.

2. **Sichere Beispiele**

```php
User::where('email', $email)->first();
DB::table('orders')->where('status', $status)->get();
```

3. **Risikoquellen**

- Unsichere String-Konkatenation in raw SQL.

```php
DB::select("SELECT * FROM users WHERE email = '$input'"); // riskant
```

4. **Sicheres raw SQL**

```php
DB::select('SELECT * FROM users WHERE email = ?', [$input]);
```

Mit korrekter Nutzung von Bindings ist Laravel sehr robust gegen SQL Injection.

</details>

<details>
<summary>67. Wann würdest du Sanctum statt Passport wählen?</summary>

#### Laravel

Sanctum ist die richtige Wahl, wenn du einfache First-Party-Authentifizierung ohne vollständigen OAuth2-Overhead brauchst.

1. **Typische Sanctum-Szenarien**

- SPA + Laravel Backend mit Session/Cookie-Auth.
- Mobile/Internal Clients mit Personal Access Tokens.
- APIs ohne Delegation an externe Drittanbieter-Clients.

2. **Warum Sanctum**

- Schnellere Implementierung.
- Geringere operative Komplexität.
- Weniger moving parts beim Token-Management.

3. **Wann Passport nötig ist**

- Bei expliziten OAuth2-Delegationsanforderungen.
- Wenn standardisierte Third-Party-Authorization-Flows benötigt werden.

Faustregel: standardmäßig Sanctum, Passport nur bei klaren OAuth2-Anforderungen.

</details>

<details>
<summary>66. Vergleiche Laravel Sanctum und Laravel Passport.</summary>

#### Laravel

Sanctum und Passport bieten beide API-Authentifizierung, zielen aber auf unterschiedliche Komplexitätsstufen.

1. **Sanctum**

- Leichtgewichtige Token-Auth + SPA-Session-Auth.
- Personal Access Tokens, einfache Abilities.
- Schnell eingerichtet, geringe OAuth-Komplexität.

2. **Passport**

- Vollwertiger OAuth2-Server.
- Unterstützt komplexe OAuth-Grant-Flows, Scopes, Refresh Tokens.
- Geeignet für Third-Party-/Delegation-Szenarien.

3. **Praxis**

- Sanctum: meist beste Wahl für First-Party-Apps.
- Passport: wenn echte OAuth2-Anforderungen bestehen.

</details>

<details>
<summary>64. Wie funktionieren die Blade-Direktiven @can und @cannot?</summary>

#### Laravel

`@can` und `@cannot` sind Blade-Direktiven für bedingtes Rendering anhand von Autorisierungsregeln.

1. **`@can`**

- Rendert Inhalte, wenn der User die Fähigkeit hat.

```blade
@can('update', $post)
    <a href="{{ route('posts.edit', $post) }}">Edit</a>
@endcan
```

2. **`@cannot`**

- Rendert Inhalte, wenn die Fähigkeit fehlt.

```blade
@cannot('delete', $post)
    <span>You cannot delete this post.</span>
@endcannot
```

3. **Bewertung**

- Nutzt intern Gates/Policies im Kontext des aktuellen Users.

So bleibt die UI mit den Backend-Berechtigungen konsistent.

</details>

<details>
<summary>65. Was ist Multi-Authentication und wie setzt man sie um?</summary>

#### Laravel

Multi-Authentication bedeutet, mehrere Guards/Benutzertypen in einer Anwendung zu unterstützen (z. B. `web`, `admin`, `api`).

1. **Typische Fälle**

- Getrennte Bereiche für Admins und Kunden.
- Unterschiedliche Zugriffsmodelle je Kanal.

2. **Umsetzung**

- Mehrere Guards/Provider konfigurieren.
- Guard-spezifische Middleware einsetzen (`auth:admin`, `auth:web`, `auth:sanctum`).
- Optional getrennte Login-Flows pro Guard.

3. **Beispiel**

```php
Route::middleware('auth:admin')->group(function () {
    Route::get('/admin/dashboard', AdminDashboardController::class);
});
```

Multi-Auth sorgt für klare Trennung von Identitäten und Berechtigungen.

</details>

<details>
<summary>45. Was sind Lazy Collections?</summary>

#### Laravel

Lazy Collections verarbeiten Daten als Stream (generatorbasiert), statt alles gleichzeitig in den Speicher zu laden.

1. **Hauptvorteil**

- Sehr speichereffizient bei großen Datenmengen.

2. **Wie sie arbeiten**

- Elemente werden einzeln erzeugt und verarbeitet.
- Transformationen laufen lazy während der Iteration.

3. **Typische Quellen**

- `lazy()` bei Queries.
- `cursor()` in Eloquent/Query Builder.
- Eigene Generatoren in `LazyCollection`.

4. **Wann nutzen**

- Große Importe/Exporte.
- Migrationen und Batch-Verarbeitung.
- Hintergrundjobs mit vielen Datensätzen.

Lazy Collections sind ideal, wenn Speicherverbrauch wichtiger ist als zufälliger Direktzugriff.

</details>

<details>
<summary>44. Was ist der Unterschied zwischen Arrays und Collections?</summary>

#### Laravel

Arrays sind native PHP-Datenstrukturen, Collections dagegen objektorientierte Wrapper mit einer fluent API für Transformationen.

1. **Arrays**

- Sehr schnell und nativ.
- Direkter Sprachsyntax-Zugriff.
- Weniger eingebaute High-Level-Transformationen.

2. **Collections**

- `Illuminate\Support\Collection` mit chainbaren Methoden.
- Typische Methoden: `map`, `filter`, `reduce`, `sortBy`, `groupBy`.
- Bessere Lesbarkeit bei komplexen Datenflüssen.

3. **Beispiel**

```php
$names = collect($users)
    ->filter(fn ($u) => $u->is_active)
    ->pluck('name')
    ->values();
```

4. **Faustregel**

- Arrays für einfache Low-Level-Fälle.
- Collections für ausdrucksstarke, wartbare Transformationen.

</details>

<details>
<summary>42. Was sind Attribute-Objekte im modernen Laravel?</summary>

#### Laravel

`Attribute`-Objekte sind der moderne Weg, Accessor- und Mutator-Logik für ein Feld zentral in einer Methode zu definieren.

1. **Grundidee**

- Eine Methode liefert `Attribute::make(get: ..., set: ...)`.
- Lese-/Schreibtransformationen bleiben an einem Ort.

2. **Beispiel**

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

3. **Vorteile**

- Klarer als alte `getXxxAttribute`/`setXxxAttribute`-Methoden.
- Besser wartbar und testbar.

Attribute-Objekte sind der empfohlene Standard für moderne Accessor/Mutator-Implementierungen.

</details>

<details>
<summary>41. Was sind Casts in Eloquent?</summary>

#### Laravel

Casts definieren, wie Eloquent Attribute zwischen Rohwerten aus der Datenbank und PHP-Typen konvertiert.

1. **Zweck**

- Automatische Typumwandlung beim Lesen und Schreiben.
- Konsistentes und besser typisiertes Modellverhalten.

2. **Häufige Cast-Typen**

- `integer`, `float`, `decimal:2`, `boolean`
- `datetime`, `immutable_datetime`
- `array`, `json`, `object`, `collection`
- `encrypted`, `hashed`

3. **Beispiel**

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

Casts reduzieren Boilerplate und verhindern viele typische Typfehler.

</details>

<details>
<summary>40. Was sind Accessors und Mutators?</summary>

#### Laravel

Accessors und Mutators steuern, wie Modellattribute beim Lesen und Schreiben transformiert werden.

1. **Accessor**

- Transformiert einen Wert beim Auslesen.

2. **Mutator**

- Transformiert einen Wert vor dem Speichern.

3. **Moderner Stil mit `Attribute`**

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

4. **Unterschied zu Casts**

- Casts: allgemeine Typumwandlungen.
- Accessors/Mutators: individuelle, domänenspezifische Transformationen.

Sie sorgen für konsistente und zentrale Attributlogik im Modell.

</details>

<details>
<summary>39. Was sind Query Scopes?</summary>

#### Laravel

Query Scopes sind Modellmethoden, die wiederverwendbare Query-Logik kapseln.

1. **Muster**

- Methode beginnt mit `scope`.
- Aufruf erfolgt ohne `scope`-Präfix.

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

2. **Vorteile**

- Weniger Duplikation.
- Bessere Lesbarkeit.
- Einheitliche Filterlogik.

Scopes sind ein Kernwerkzeug für saubere Eloquent-Abfragen.

</details>

<details>
<summary>38. Was sind globale Scopes und lokale Scopes?</summary>

#### Laravel

Scopes sind wiederverwendbare Query-Einschränkungen in Eloquent.

1. **Globale Scopes**

- Werden automatisch auf alle Queries eines Modells angewendet.
- Geeignet für systemweite Regeln (z. B. Tenant-Filter, aktive Datensätze).

2. **Lokale Scopes**

- Werden explizit im Query-Chain aufgerufen.
- Kapseln wiederkehrende Filterlogik.

```php
public function scopePublished(Builder $query): Builder
{
    return $query->whereNotNull('published_at');
}

$posts = Post::published()->get();
```

3. **Praxisregel**

- Global Scope für Default-Regeln.
- Local Scope für optionale, use-case-spezifische Filter.

Scopes verbessern Lesbarkeit und vermeiden duplizierte Bedingungen.

</details>

<details>
<summary>37. Was ist Lazy Eager Loading?</summary>

#### Laravel

Lazy Eager Loading lädt Beziehungen erst nach dem Abruf der Hauptmodelle, aber weiterhin gesammelt statt pro Datensatz.

1. **Wann sinnvoll**

- Wenn erst später im Ablauf klar wird, welche Beziehungen benötigt werden.

2. **Methoden**

- `load()` lädt gezielt Beziehungen nach.
- `loadMissing()` lädt nur nicht bereits geladene Beziehungen.

```php
$posts = Post::latest()->take(50)->get();
$posts->load('author', 'comments');
```

3. **Abgrenzung**

- `with()` = vor dem Query.
- `load()` = nach dem Query.

Lazy Eager Loading verbindet Flexibilität mit Performance.

</details>

<details>
<summary>36. Was ist das N+1-Query-Problem und wie löst man es?</summary>

#### Laravel

Das N+1-Problem entsteht, wenn ein Query eine Liste lädt und danach pro Eintrag zusätzliche Queries für Beziehungen ausführt.

1. **Typischer Fall**

- 1 Query für 100 Posts.
- Danach 100 weitere Queries für `$post->author`.

2. **Warum problematisch**

- Hohe Query-Anzahl.
- Mehr Latenz und höhere Datenbanklast.

3. **Lösung in Laravel**

- Eager Loading per `with()` verwenden.

```php
$posts = Post::with('author')->get();
```

- Bei bereits geladenen Modellen `load()` oder `loadMissing()` nutzen.

N+1-Beseitigung ist eine der wirksamsten Eloquent-Optimierungen.

</details>

<details>
<summary>35. Was ist Eager Loading?</summary>

#### Laravel

Eager Loading bedeutet, dass verknüpfte Modelle vorab gemeinsam mit dem Hauptquery geladen werden, statt später pro Eintrag einzeln.

1. **Warum wichtig**

- Reduziert die Anzahl der Datenbankabfragen.
- Verhindert N+1-Probleme.
- Verbessert Performance und Skalierbarkeit.

2. **Typisches Beispiel**

```php
$posts = Post::with(['author', 'comments'])->latest()->get();
```

3. **Varianten**

- Verschachteltes Laden (`with('comments.user')`).
- Eingeschränktes Eager Loading via Closure.
- Standardbeziehungen per `$with` im Modell.

Eager Loading ist eine zentrale Performance-Praxis bei Eloquent.

</details>

<details>
<summary>2. Was sind die wichtigsten Vorteile von Laravel im Vergleich zu anderen PHP-Frameworks?</summary>

#### Laravel

Die wichtigsten Vorteile von Laravel liegen in der starken Developer Experience, den umfangreichen integrierten Funktionen und dem großen Ökosystem.

1. **Developer Experience**

- Konsistente und ausdrucksstarke API-Gestaltung über die Framework-Komponenten hinweg.
- Hervorragende Dokumentation und einfacher Einstieg.
- Schnelles Scaffolding und effiziente CLI-Workflows über `Artisan`.

2. **Batteries Included**

- Erstklassige Unterstützung für Routing, Validierung, Authentifizierung, Queues, Events, Benachrichtigungen, Caching und Scheduling.
- ORM (Eloquent) und Schema-Migrationen sind standardmäßig enthalten.

3. **Architektur und Wartbarkeit**

- Service Container und Dependency Injection sind tief integriert.
- Middleware und Service Provider machen Querschnittsaspekte explizit.
- Starke Testunterstützung durch PHPUnit/Pest-Integration.

4. **Starkes Ökosystem**

- Offizielle Tools: Forge, Vapor, Horizon, Telescope, Octane, Sanctum, Passport, Cashier.
- Reifes Community-Ökosystem und langfristige Stabilität.

5. **Betriebliche Produktivität**

- Reibungslose CI/CD- und Deployment-Workflows.
- Sehr gute Unterstützung für Queues, Caching, Redis und Monitoring.

Laravel wird häufig gewählt, wenn Teams Business-Funktionen schnell liefern wollen, ohne Codequalität und langfristige Wartbarkeit zu opfern.

</details>

<details>
<summary>3. Wie folgt Laravel der MVC-Architektur?</summary>

#### Laravel

Laravel folgt dem MVC-Prinzip (Model-View-Controller), indem Domänen-/Datenlogik, Request-Verarbeitung und Darstellung klar getrennt werden.

1. **Model (M)**

- In der Regel Eloquent-Modelle in `app/Models`.
- Repräsentieren Domänenentitäten und Datenbankdatensätze.
- Enthalten Beziehungen, Scopes, Casts und domänenspezifisches Verhalten.

2. **View (V)**

- Blade-Templates in `resources/views`.
- Verantwortlich ausschließlich für die Darstellung.
- Erhalten vorbereitete Daten von Controllern oder View-Models.

3. **Controller (C)**

- Klassen in `app/Http/Controllers`.
- Verarbeiten HTTP-Requests, koordinieren Validierung/Services und liefern Responses zurück.
- Sollten schlank bleiben: Orchestrierung statt schwerer Business-Logik.

4. **Request-Flow im MVC-Kontext**

- Eine Route ordnet die URL einer Controller-Action zu.
- Der Controller nutzt Modelle/Services zur Ausführung des Use Cases.
- Der Controller gibt eine View (HTML) oder eine JSON-Response (API) zurück.

Laravel unterstützt zusätzlich Service-Klassen, Actions, Repositories und Domänenschichten über MVC hinaus für größere Anwendungen.

</details>

<details>
<summary>4. Beschreibe den Request-Lifecycle in einer Laravel-Anwendung.</summary>

#### Laravel

Der Request-Lifecycle in Laravel beschreibt, wie ein eingehender HTTP-Request in eine Response umgewandelt wird.

1. **Einstiegspunkt**

- Der Webserver leitet Requests an `public/index.php`.
- Composer-Autoloader und das Laravel-Bootstrapping werden geladen.

2. **Start des HTTP-Kernels**

- Der Service Container wird initialisiert.
- Globale und routebezogene Middleware-Stacks werden vorbereitet.

3. **Service Provider**

- Provider werden registriert und gebootet.
- Kernservices und Bindings der Anwendung stehen bereit.

4. **Routing-Phase**

- Der Router matched HTTP-Methode + URI auf eine Route.
- Die Middleware-Pipeline der Route wird ausgeführt.

5. **Ausführung von Controller/Handler**

- Eine Controller-Action, Closure oder invokable Klasse wird ausgeführt.
- Abhängigkeiten werden automatisch aus dem Container aufgelöst.
- Validierung, Autorisierung, Business-Logik und Datenzugriff finden statt.

6. **Response-Erzeugung**

- Der Handler gibt `Response`, `JsonResponse`, View, Redirect oder serialisierbare Daten zurück.
- Laravel normalisiert das Ergebnis zu einem HTTP-Response-Objekt.

7. **Terminierungsphase**

- Die Response wird an den Client gesendet.
- Terminierbare Middleware und Post-Response-Hooks laufen.

Dieser Lifecycle sorgt in Laravel für ein vorhersehbares Ausführungsmodell und klare Erweiterungspunkte.

</details>

<details>
<summary>5. Was ist der Laravel Service Container?</summary>

#### Laravel

Der Laravel Service Container ist ein IoC-Container (Inversion of Control), der für Objekterzeugung und Abhängigkeitsverwaltung zuständig ist.

1. **Kernaufgabe**

- Zentrale Stelle, an der Klassen/Interfaces an konkrete Implementierungen gebunden werden.
- Löst Konstruktorabhängigkeiten automatisch per Reflection auf.

2. **Warum das wichtig ist**

- Reduziert manuelles Verdrahten von Objekten.
- Ermöglicht Dependency Inversion (Abhängigkeit von Interfaces statt von konkreten Klassen).
- Verbessert Testbarkeit durch austauschbare Implementierungen (z. B. Fakes/Mocks).

3. **Wo er genutzt wird**

- In Controllern, Middleware, Jobs, Listenern, Commands und Service-Klassen.
- In Framework-Interna sowie in benutzerdefinierter Anwendungsarchitektur.

4. **Häufige APIs**

- `bind()` für transiente Bindings.
- `singleton()` für eine geteilte Instanz.
- `make()` / `app()` zum Auflösen von Services.

5. **Praktischer Effekt**

- Klarere Konstruktoren, geringere Kopplung, besseres modulares Design.

In Laravel ist der Service Container eine der zentralen Grundlagen für skalierbare Architektur.

</details>

<details>
<summary>6. Erkläre den Unterschied zwischen Binding, Singleton-Binding und Resolving im Service Container.</summary>

#### Laravel

Diese Begriffe beschreiben unterschiedliche Schritte im Lebenszyklus des Laravel-Containers.

1. **Binding (`bind`)**

- Registriert, wie der Container einen Typ erstellen soll.
- Erstellt **bei jedem Resolve eine neue Instanz** (transienter Lebenszyklus).

```php
$this->app->bind(PaymentGateway::class, StripeGateway::class);
```

2. **Singleton-Binding (`singleton`)**

- Registriert einen Typ als **geteilte Instanz**.
- Beim ersten Resolve wird die Instanz erstellt, danach immer dieselbe zurückgegeben.

```php
$this->app->singleton(CacheClient::class, fn () => new CacheClient());
```

3. **Resolving (`make` / Auto-Injection)**

- Der Vorgang, eine Instanz aus dem Container anzufordern.
- Kann explizit (`app()->make(...)`) oder implizit per Constructor Injection erfolgen.

```php
$gateway = app()->make(PaymentGateway::class);
```

4. **Faustregel**

- `bind` für zustandslose/leichte Services.
- `singleton` für geteilte/schwere Infrastruktur-Clients.
- Bevorzugt automatische Auflösung per Dependency Injection in frameworkverwalteten Klassen.

</details>

<details>
<summary>7. Was ist Contextual Binding und wann verwendet man es?</summary>

#### Laravel

Mit Contextual Binding kann man für dasselbe Interface unterschiedliche Implementierungen bereitstellen – abhängig davon, welche Klasse gerade aufgelöst wird.

1. **Welches Problem es löst**

- Mehrere Konsumenten benötigen denselben Vertrag, aber unterschiedliches Verhalten.

2. **Beispielszenario**

- `PhotoController` soll `S3Filesystem` verwenden.
- `ReportController` soll `LocalFilesystem` verwenden.
- Beide hängen von `FilesystemInterface` ab.

3. **Container-API**

```php
$this->app->when(PhotoController::class)
    ->needs(FilesystemInterface::class)
    ->give(S3Filesystem::class);

$this->app->when(ReportController::class)
    ->needs(FilesystemInterface::class)
    ->give(LocalFilesystem::class);
```

4. **Wann einsetzen**

- Multi-Tenant- oder Multi-Region-Integrationen.
- Unterschiedliche Adapter für unterschiedliche Use Cases.
- Wenn ein globales Binding nicht ausreicht.

Contextual Binding ist sinnvoll, wenn Verhalten je nach Konsumentenkontext variieren muss.

</details>

<details>
<summary>8. Was sind Service Provider und wozu dienen sie?</summary>

#### Laravel

Service Provider sind der zentrale Bootstrap-Mechanismus in Laravel zum Registrieren und Konfigurieren von Services.

1. **Hauptzweck**

- Registrieren von Container-Bindings.
- Konfigurieren von Paket-/Anwendungsservices beim Start.

2. **Was typischerweise hinein gehört**

- Interface-zu-Implementierung-Bindings.
- Singleton-Registrierungen für Infrastrukturservices.
- Event/Listener-Registrierungen (oder in separaten Providern).
- Paket-Bootstrapping und Konfigurationsverdrahtung.

3. **Typische Beispiele**

- `AppServiceProvider`
- `RouteServiceProvider`
- Paket-Provider

4. **Warum das wichtig ist**

- Schafft eine vorhersehbare Startschicht.
- Hält Bootstrap-Logik aus Controllern/Modellen heraus.
- Verbessert Modularität und Wartbarkeit in größeren Anwendungen.

Service Provider sind praktisch die Composition Root einer Laravel-Anwendung.

</details>

<details>
<summary>9. Was ist der Unterschied zwischen Registering und Booting in einem Service Provider?</summary>

#### Laravel

In einem Service Provider laufen `register()` und `boot()` in unterschiedlichen Phasen und haben unterschiedliche Aufgaben.

1. **`register()`**

- Dient zum Registrieren von Bindings im Container.
- Sollte keine Seiteneffekte haben und nicht davon abhängen, dass andere Provider bereits gebootet sind.

```php
public function register(): void
{
    $this->app->singleton(PaymentGateway::class, StripeGateway::class);
}
```

2. **`boot()`**

- Läuft, nachdem alle Provider registriert wurden.
- Für Integrationslogik mit bereits verfügbaren Services: Routen, View Composers, Observer, Events, Macros.

```php
public function boot(): void
{
    Schema::defaultStringLength(191);
}
```

3. **Faustregel**

- `register()` = Abhängigkeiten deklarieren.
- `boot()` = Framework-Integrationslogik ausführen.

</details>

<details>
<summary>10. Was sind Laravel Contracts?</summary>

#### Laravel

Laravel Contracts sind vom Framework definierte PHP-Interfaces, die die Fähigkeiten zentraler Services unabhängig von ihrer konkreten Implementierung beschreiben.

1. **Was sie sind**

- Interfaces unter `Illuminate\Contracts\...`.
- Beispiele: `Cache\Repository`, `Queue\Queue`, `Auth\Guard`, `Mail\Mailer`.

2. **Warum sie wichtig sind**

- Entkoppeln deinen Code von konkreten Framework-Klassen.
- Unterstützen Dependency Inversion und erleichtern Tests.
- Erlauben den Austausch von Implementierungen mit minimalen Änderungen.

3. **Wie sie verwendet werden**

- Contract im Konstruktor oder in Methoden type-hinten.
- Der Service Container löst die passende Implementierung auf.

```php
use Illuminate\Contracts\Cache\Repository as Cache;

final class UserService
{
    public function __construct(private Cache $cache) {}
}
```

Laravel Contracts sind ein zentraler Baustein für sauberen, austauschbaren und testbaren Laravel-Code.

</details>

<details>
<summary>11. Was ist der Unterschied zwischen einem Contract und einer Facade?</summary>

#### Laravel

Contracts und Facades beziehen sich beide auf Laravel-Services, lösen aber unterschiedliche Aufgaben.

1. **Contract**

- Ein PHP-Interface (meist unter `Illuminate\Contracts\...`).
- Definiert Verhalten/Fähigkeiten ohne Implementierungsdetails.
- Dient sauberer Architektur und Dependency Inversion.

2. **Facade**

- Ein statisch wirkender Proxy auf einen Service aus dem Container.
- Bietet eine kurze, bequeme Aufrufsyntax.
- Beispiel: `Cache::get('key')`, `Log::info('...')`.

3. **Kernunterschied**

- Contract = Abstraktionsgrenze (Design-Zeit).
- Facade = Komfort-Zugriffsschicht (Nutzungsstil).

4. **Testauswirkung**

- Contracts lassen sich über DI leicht mocken.
- Facades können ebenfalls gemockt werden (`Facade::shouldReceive()`), bleiben aber statisch anmutend.

Kurz: Der Contract definiert, *was* ein Service kann; die Facade vereinfacht, *wie* man ihn aufruft.

</details>

<details>
<summary>12. Erkläre den Unterschied zwischen Facades und Helper-Funktionen in Laravel.</summary>

#### Laravel

Sowohl Facades als auch Helper bieten kurze Syntax, unterscheiden sich aber in Struktur, Transparenz und Teststil.

1. **Facades**

- Klassenbasierte, statisch wirkende Proxys (`Cache::`, `DB::`, `Bus::`).
- Auf Services im Container gemappt.
- Unterstützen Facade-Mocking/Faking.

2. **Helper-Funktionen**

- Globale Funktionen wie `app()`, `route()`, `config()`, `request()`, `response()`.
- Sehr kurz und praktisch in Views/Controllern.

3. **Praktische Einordnung**

- Facades sind expliziter über Klassennamen.
- Helper sind minimalistischer und direkt.

4. **Architekturhinweis**

- In Core-Business-Code ist Constructor DI meist die sauberste Wahl.
- In Framework-Glue-Code sind Facades/Helper beide vertretbar.

</details>

<details>
<summary>13. Wie funktioniert Dependency Injection in Laravel?</summary>

#### Laravel

Dependency Injection in Laravel wird durch den Service Container unterstützt, der Abhängigkeiten automatisch auflöst.

1. Konstruktor-Injection per Type-Hint.
2. Methoden-Injection in Controllern/Jobs/Listenern.
3. Interfaces werden über Bindings auf konkrete Klassen gemappt.

DI reduziert Kopplung und verbessert Testbarkeit.

</details>

<details>
<summary>14. Wie nutzt Laravel IoC (Inversion of Control)?</summary>

#### Laravel

Laravel übergibt Objekterstellung und Verdrahtung an den Container statt Abhängigkeiten direkt im Code zu instanziieren.

1. Klassen deklarieren Abstraktionen.
2. Der Container liefert Implementierungen.
3. Ergebnis: austauschbare Komponenten, bessere Tests, klarere Architektur.

</details>

<details>
<summary>15. Was ist Middleware in Laravel?</summary>

#### Laravel

Middleware sind Filter in der HTTP-Pipeline, die Requests/Responses vor oder nach der Controller-Logik verarbeiten.

Typische Aufgaben:

1. Authentifizierung/Autorisierung
2. CSRF-Schutz
3. Rate Limiting
4. Logging, Security Headers, Lokalisierung

</details>

<details>
<summary>16. Wie registriert und weist man Middleware zu?</summary>

#### Laravel

Middleware wird in Laravel konfiguriert und dann über Alias, Gruppe oder Klassenname Routen zugewiesen.

1. Alias/Groups definieren.
2. Global Middleware für alle Requests.
3. Route-/Group-spezifische Middleware per `->middleware(...)`.

</details>

<details>
<summary>17. Wie funktioniert Middleware mit Parametern?</summary>

#### Laravel

Middleware kann Parameter aus der Route erhalten, z. B. `role:admin`.

1. Parameter werden in der Route angegeben.
2. `handle(...)` nimmt sie nach `$next` entgegen.
3. So bleibt Middleware wiederverwendbar und konfigurierbar.

</details>

<details>
<summary>18. Was sind Route Groups, Prefixes und Middleware Groups?</summary>

#### Laravel

Route Groups bündeln gemeinsame Route-Eigenschaften.

1. `prefix(...)` für gemeinsame URI-Präfixe.
2. `name(...)` für Namenspräfixe.
3. `middleware(...)` für gemeinsame Sicherheits-/Pipeline-Regeln.

Das reduziert Wiederholungen und hält Routen konsistent.

</details>

<details>
<summary>19. Was ist Route Model Binding?</summary>

#### Laravel

Route Model Binding wandelt Route-Parameter automatisch in Eloquent-Modelle um.

1. Type-Hint im Controller genügt meist.
2. Nicht gefundene Modelle führen automatisch zu 404.
3. Spart `findOrFail()`-Boilerplate.

</details>

<details>
<summary>20. Erkläre implizites vs. explizites Route Model Binding.</summary>

#### Laravel

1. **Implizit**: Laravel erkennt Binding über Parameternamen + Type-Hint.
2. **Explizit**: Mapping wird manuell über `Route::bind(...)` definiert.

Implizit ist Standard; explizit ist nützlich für Sonderlogik.

</details>

<details>
<summary>21. Was ist Rate Limiting in Laravel und wie funktioniert es?</summary>

#### Laravel

Rate Limiting begrenzt, wie viele Requests ein Client in einem Zeitraum senden darf, um APIs vor Missbrauch und Überlastung zu schützen.

1. **Was es macht**

- Beschränkt die Request-Frequenz pro Schlüssel (User-ID, IP, Token oder eigener Identifier).
- Bei Überschreitung wird `429 Too Many Requests` zurückgegeben.

2. **Wie Laravel es umsetzt**

- Benannte Limiter werden über `RateLimiter::for(...)` definiert.
- Anwendung über Middleware (typisch `throttle`).
- Zähler liegen im Cache-Backend (z. B. Redis/Memcached/DB-Cache).

3. **Typischer Einsatz**

- Öffentliche API-Endpunkte.
- Login/OTP/Passwort-Reset.
- Kostenintensive Endpunkte wie Suche/Export/Reports.

Rate Limiting ist ein zentraler Baustein für Stabilität und Sicherheit in Laravel-APIs.

</details>

<details>
<summary>22. Was sind Invokable Controller?</summary>

#### Laravel

Invokable Controller besitzen genau eine `__invoke()`-Methode und repräsentieren einen einzelnen Use Case.

Vorteile:

1. Klare Verantwortung
2. Schlanke Route-zu-Action-Zuordnung
3. Gute Testbarkeit

</details>

<details>
<summary>23. Was sind Single Action Controller?</summary>

#### Laravel

Single Action Controller sind praktisch Invokable Controller: ein Controller, eine Aktion.

Sie fördern:

1. Trennung von Verantwortlichkeiten
2. bessere Wartbarkeit
3. geringere Merge-Konflikte in Teams

</details>

<details>
<summary>24. Was ist der Unterschied zwischen Resource Controllern und API Resource Controllern?</summary>

#### Laravel

1. `Route::resource` erzeugt vollständige CRUD-Routen inkl. `create`/`edit` (für HTML-Formen).
2. `Route::apiResource` lässt `create`/`edit` weg und ist API-fokussiert.

`resource` passt zu servergerenderten Apps, `apiResource` zu JSON-APIs.

</details>

<details>
<summary>25. Wie erstellt man eigene Artisan-Kommandos?</summary>

#### Laravel

Eigene Artisan-Kommandos sind CLI-Klassen für Automatisierung, Wartung und wiederkehrende Backend-Prozesse.

1. **Kommando generieren**

```bash
php artisan make:command SyncInvoicesCommand
```

2. **Signature und Beschreibung definieren**

```php
protected $signature = 'billing:sync {--dry-run}';
protected $description = 'Sync invoices from billing provider';
```

3. **Logik in `handle()` implementieren**

```php
public function handle(): int
{
    // command logic
    return self::SUCCESS;
}
```

4. **Ausführen**

```bash
php artisan billing:sync --dry-run
```

5. **Optional planen**

- Über den Scheduler regelmäßig ausführen lassen.

Custom Commands sind ideal für wiederholbare, betriebsrelevante Aufgaben in Laravel.

</details>

<details>
<summary>26. Was sind Macros und wann sind sie sinnvoll?</summary>

#### Laravel

Macros erlauben es, Framework-Klassen zur Laufzeit um eigene Methoden zu erweitern, ohne den Framework-Code zu ändern.

1. **Typische macroable Ziele**

- `Collection`, `Str`, `ResponseFactory`, `Route` usw.

2. **Beispiel**

```php
use Illuminate\Support\Collection;

Collection::macro('toKeyValue', function (string $key, string $value) {
    return $this->mapWithKeys(fn ($item) => [$item[$key] => $item[$value]]);
});
```

3. **Wann sinnvoll**

- Wiederkehrende Hilfslogik im Codebestand.
- Domänenspezifische Shortcuts für Collections/Strings.
- Mehr Lesbarkeit bei häufigen Transformationen.

4. **Best Practices**

- Macros zentral (z. B. im Service Provider) registrieren.
- Namen klar wählen, um Kollisionen zu vermeiden.
- Für komplexe Logik lieber eigene Klassen verwenden.

Macros sind besonders nützlich für kleine, oft genutzte Erweiterungen.

</details>

<details>
<summary>27. Was sind Actions in der Laravel-Architektur und wann verwendet man sie?</summary>

#### Laravel

Actions sind fokussierte Klassen, die einen einzelnen Business-Use-Case kapseln.

1. **Was eine Action ist**

- Klassen wie `CreateOrderAction`, `PublishPostAction`, `RefundPaymentAction`.
- Meist mit einer Methode wie `handle()` oder `execute()`.

2. **Warum Actions nützlich sind**

- Business-Logik wird aus Controllern/Modellen ausgelagert.
- Wiederverwendbar in HTTP, Jobs, Listenern und Commands.
- Leicht testbar durch klare Ein-/Ausgabe.

3. **Typische Struktur**

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

Actions verbessern Modularität und machen Geschäftsabläufe explizit.

</details>

<details>
<summary>28. Erkläre das Repository Pattern und seine Vorteile.</summary>

#### Laravel

Das Repository Pattern abstrahiert den Datenzugriff über Interfaces, damit Business-Logik nicht direkt von ORM-/Query-Details abhängt.

1. **Grundidee**

- Contract definieren (z. B. `OrderRepository`).
- Konkrete Implementierung bereitstellen (z. B. `EloquentOrderRepository`).
- Repository in Services/Actions injizieren.

2. **Vorteile**

- Klare Trennung von Anwendungslogik und Persistenz.
- Einfacheres Testen mit Fakes/In-Memory-Repositories.
- Zentralisierung komplexer Query- und Caching-Logik.

3. **Trade-offs**

- Zusätzliche Abstraktion und mehr Boilerplate.
- Für sehr einfache CRUD-Module nicht immer notwendig.

Pragmatisch einsetzen: dort, wo es Kopplung und Komplexität wirklich reduziert.

</details>

<details>
<summary>29. Was sind Traits in PHP und wie werden sie in Laravel verwendet?</summary>

#### Laravel

Traits sind ein PHP-Mechanismus für horizontale Wiederverwendung von Verhalten ohne klassische Vererbung.

1. **Was Traits ermöglichen**

- Wiederverwendbare Methoden/Eigenschaften via `use`.
- Gemeinsames Verhalten für Klassen außerhalb einer gemeinsamen Vererbungslinie.

2. **Typische Laravel-Traits**

- `SoftDeletes`, `HasFactory`, `Notifiable`, `AuthorizesRequests`, `DispatchesJobs`, `ValidatesRequests`.

3. **Beispiel**

```php
use Illuminate\Database\Eloquent\SoftDeletes;

class Post extends Model
{
    use SoftDeletes;
}
```

4. **Best Practices**

- Traits klein und fokussiert halten.
- Für komplexe Domänenlogik eher Composition/Services nutzen.

Traits sind ein praktisches Mittel für gezielte Wiederverwendung in Laravel-Projekten.

</details>

<details>
<summary>30. Was sind die Unterschiede zwischen Laravel und Lumen, und ist Lumen im Jahr 2026 noch relevant?</summary>

#### Laravel

Laravel und Lumen haben gemeinsame Wurzeln, verfolgen aber unterschiedliche Ziele.

1. **Laravel** ist ein vollwertiges Framework mit großem Ökosystem.
2. **Lumen** ist ein schlankes Micro-Framework mit reduziertem Umfang.
3. Für neue Projekte wird in der Praxis meist Laravel bevorzugt.
4. Lumen bleibt vor allem für bestehende Legacy-Services relevant.

</details>

<details>
<summary>31. Was ist Eloquent ORM?</summary>

#### Laravel

Eloquent ORM ist Laravels Active-Record-Implementierung für den Datenbankzugriff über Modelle statt über rohes SQL.

1. Mapping von Modellen auf Tabellen.
2. Beziehungen, Scopes, Casts und Model-Events.
3. Ausdrucksstarke Query-Syntax.

Eloquent ist der Standard-Datenzugriff in vielen Laravel-Anwendungen.

</details>

<details>
<summary>32. Was sind Eloquent-Modelle?</summary>

#### Laravel

Eloquent-Modelle sind PHP-Klassen, die Tabellen repräsentieren und Datenverhalten kapseln.

1. Eine Modellinstanz entspricht typischerweise einer Tabellenzeile.
2. Modelle enthalten Attribute, Beziehungen, Casts und Scopes.
3. Sie zentralisieren Persistenzlogik und Domänenverhalten.

</details>

<details>
<summary>33. Erkläre One-to-One-, One-to-Many-, Many-to-Many- und polymorphe Beziehungen.</summary>

#### Laravel

Eloquent-Beziehungen definieren strukturelle Verknüpfungen zwischen Modellen.

1. **One-to-One**: ein Datensatz zu genau einem anderen.
2. **One-to-Many**: ein Parent zu vielen Children.
3. **Many-to-Many**: beide Seiten zu vielen Datensätzen (Pivot-Tabelle).
4. **Polymorph**: ein Child kann zu unterschiedlichen Parent-Typen gehören.

</details>

<details>
<summary>34. Was sind polymorphe Beziehungen und wann nutzt man sie?</summary>

#### Laravel

Polymorphe Beziehungen erlauben, dass ein Modell zu mehreren Modelltypen referenzieren kann (typisch über `*_type` und `*_id`).

1. Reduziert Tabellen-Duplikation bei ähnlichen Beziehungen.
2. Typische Fälle: Kommentare/Bilder/Aktivitäten für verschiedene Entitäten.
3. In Laravel über `morphTo`, `morphOne`, `morphMany` usw.

</details>

<details>
<summary>43. Was sind Eloquent Collections?</summary>

#### Laravel

Eloquent Collections sind spezialisierte Collection-Objekte, die von Eloquent-Abfragen zurückgegeben werden und Laravels Basis-`Collection` um modellbewusstes Verhalten erweitern.

1. **Was sie sind**

- Werden von Methoden wie `get()` und beim Laden von Beziehungen zurückgegeben.
- Enthalten Modellinstanzen, keine einfachen Arrays.

2. **Zusätzliche Fähigkeiten**

- Erben die umfangreiche Collection-API (`map`, `filter`, `groupBy`, `pluck` usw.).
- Bieten Eloquent-spezifische Helfer wie `load()`, `loadMissing()`, `modelKeys()`, `fresh()`.

3. **Beispiel**

```php
$users = User::where('is_active', true)->get(); // Eloquent Collection
$emails = $users->pluck('email');
```

4. **Warum nützlich**

- Ausdrucksstarke Transformationen nach der Abfrage.
- Komfortable Bulk-Operationen auf Modellmengen.

Eloquent Collections kombinieren ORM-Bewusstsein mit funktionalem Datenzugriff.

</details>

<details>
<summary>46. Wozu dient die Methode `cursor()`?</summary>

#### Laravel

`cursor()` gibt eine lazy Iterable von Ergebnissen zurück, sodass du Datensätze mit geringem Speicherverbrauch einzeln durchlaufen kannst.

1. **Warum verwenden**

- Verhindert, dass die gesamte Ergebnismenge in den RAM geladen wird.
- Ermöglicht effiziente Verarbeitung großer Tabellen.

2. **Beispiel**

```php
foreach (User::where('is_active', true)->cursor() as $user) {
    // user verarbeiten
}
```

3. **Eigenschaften**

- Generatorbasierte Iteration.
- Gut für Read/Process-Pipelines.
- Funktioniert gut mit Queues und langlaufenden Jobs.

4. **Wann weniger geeignet**

- Wenn du zufälligen Zugriff auf alle Ergebnisse gleichzeitig brauchst.
- Wenn du für alle Datensätze eine große eager-geladene Objektstruktur materialisieren musst.

`cursor()` ist ein zentrales Werkzeug für skalierbare Verarbeitung Datensatz für Datensatz.

</details>
