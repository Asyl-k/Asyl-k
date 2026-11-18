# Asyl — Java Backend Developer

Привет! Меня зовут Asyl, я Java backend-разработчик. Здесь собраны проекты, в которых я отрабатываю практики реального backend: транзакционные границы, конкурентный доступ, идемпотентность, ограничения на уровне базы данных, интеграционные тесты и CI.

**Стек:** Java 21 · Spring Boot 3 · Spring Data JPA · Spring Security · PostgreSQL · Flyway · JUnit 5 · Mockito · Testcontainers · Maven · Docker · GitHub Actions

## Проекты

### [Task Manager API](https://github.com/Asyl-k/task-manager-api)

[![CI](https://github.com/Asyl-k/task-manager-api/actions/workflows/ci.yml/badge.svg)](https://github.com/Asyl-k/task-manager-api/actions/workflows/ci.yml)

REST API для задач с JWT-аутентификацией, ролями и проверкой владельца. Пользователь видит и меняет только свои задачи, администратор — все. Есть фильтрация, пагинация, единый формат ошибок `ProblemDetail`, миграции Flyway и OpenAPI.

`Spring Security` `JWT` `PostgreSQL` `Flyway` `Testcontainers`

### [Payment Ledger Service](https://github.com/Asyl-k/payment-ledger-service)

[![CI](https://github.com/Asyl-k/payment-ledger-service/actions/workflows/ci.yml/badge.svg)](https://github.com/Asyl-k/payment-ledger-service/actions/workflows/ci.yml)

Платёжный ledger с двойной записью: каждый перевод создаёт пару `DEBIT`/`CREDIT`. Повторный запрос с тем же `Idempotency-Key` возвращает исходный перевод, а не двигает деньги ещё раз. Счета блокируются `SELECT ... FOR UPDATE` в порядке возрастания id, поэтому конкурентные переводы не теряют обновления и не приводят к дедлокам.

`Double-entry` `Idempotency` `Pessimistic locking` `PostgreSQL` `Flyway`

### [URL Shortener Service](https://github.com/Asyl-k/url-shortener-service)

[![CI](https://github.com/Asyl-k/url-shortener-service/actions/workflows/ci.yml/badge.svg)](https://github.com/Asyl-k/url-shortener-service/actions/workflows/ci.yml)

Сервис коротких ссылок с Base62-кодами, кастомными алиасами, сроком жизни и подсчётом переходов. Уникальность алиаса обеспечивает constraint в PostgreSQL, а не проверка «прочитать → вставить», поэтому гонка из 12 параллельных запросов даёт ровно одну ссылку. Горячие ссылки кэшируются в Caffeine, клики считаются атомарным `UPDATE`.

`Base62` `Caffeine` `PostgreSQL` `Flyway` `Atomic counters`

### [Booking Service](https://github.com/Asyl-k/booking-service)

[![CI](https://github.com/Asyl-k/booking-service/actions/workflows/ci.yml/badge.svg)](https://github.com/Asyl-k/booking-service/actions/workflows/ci.yml)

Бронирование ресурсов без двойных записей. Пересечение интервалов запрещает `EXCLUDE`-constraint с `btree_gist` и `tstzrange(..., '[)')`: соседние слоты разрешены, а любой реальный overlap отклоняется даже при одновременных запросах. Отмена освобождает слот, потому что constraint действует только на `CONFIRMED`-брони.

`PostgreSQL exclusion constraint` `btree_gist` `Concurrency` `Flyway`

## Как устроены проекты

- Каждый репозиторий запускается по README: `docker compose up --build` или локально с PostgreSQL.
- Схема управляется Flyway, Hibernate работает с `ddl-auto: validate` — расхождение сущностей и миграций ломает старт.
- API отдаёт DTO и ошибки в формате RFC 9457 `ProblemDetail` со стабильным полем `code`.
- Unit-тесты не требуют Docker; интеграционные тесты поднимают `postgres:17-alpine` через Testcontainers.
- CI на каждый push прогоняет тесты, собирает Docker-образ и делает smoke-тест запущенного стека.
- Docker-образ запускается от непривилегированного пользователя.

## Что посмотреть в коде

| Проект | С чего начать | Почему интересно |
|---|---|---|
| Task Manager API | `SecurityConfig`, `TaskService` | Проверка ownership и ролей на уровне сервиса, а не только контроллера |
| Payment Ledger Service | `TransferExecutor`, `TransferService` | Блокировки в стабильном порядке, replay идемпотентного запроса, двойная запись |
| URL Shortener Service | `ShortLinkService`, `V1__init.sql` | Retry для сгенерированных кодов и constraint против гонки кастомных алиасов |
| Booking Service | `V1__init.sql`, `BookingService` | Exclusion constraint как единственный надёжный арбитр пересечений |

## Архив

Ранние учебные проекты — [auth-service](https://github.com/Asyl-k/auth-service), [order-service](https://github.com/Asyl-k/order-service), [inventory-service](https://github.com/Asyl-k/inventory-service), [notification-service](https://github.com/Asyl-k/notification-service) и [api-gateway](https://github.com/Asyl-k/api-gateway) — переведены в архив и не поддерживаются. JWT-аутентификация теперь часть Task Manager API; остальные репозитории оставлены как история обучения.

---

# Asyl — Java Backend Developer (EN)

Hi! I am Asyl, a Java backend developer. This profile contains projects where I practise the things that matter in real backend work: transaction boundaries, concurrent access, idempotency, database-level constraints, integration tests and CI.

**Stack:** Java 21 · Spring Boot 3 · Spring Data JPA · Spring Security · PostgreSQL · Flyway · JUnit 5 · Mockito · Testcontainers · Maven · Docker · GitHub Actions

## Projects

### [Task Manager API](https://github.com/Asyl-k/task-manager-api)

[![CI](https://github.com/Asyl-k/task-manager-api/actions/workflows/ci.yml/badge.svg)](https://github.com/Asyl-k/task-manager-api/actions/workflows/ci.yml)

A task REST API with JWT authentication, roles and ownership checks. Users can only read and modify their own tasks, while admins can manage all of them. Includes filtering, pagination, RFC 9457 `ProblemDetail` errors, Flyway migrations and OpenAPI.

`Spring Security` `JWT` `PostgreSQL` `Flyway` `Testcontainers`

### [Payment Ledger Service](https://github.com/Asyl-k/payment-ledger-service)

[![CI](https://github.com/Asyl-k/payment-ledger-service/actions/workflows/ci.yml/badge.svg)](https://github.com/Asyl-k/payment-ledger-service/actions/workflows/ci.yml)

A payment ledger with double-entry bookkeeping: every transfer writes one `DEBIT` and one `CREDIT` entry. Retrying a request with the same `Idempotency-Key` returns the original transfer instead of moving money again. Accounts are locked with `SELECT ... FOR UPDATE` in ascending id order, so concurrent transfers neither lose updates nor deadlock.

`Double-entry` `Idempotency` `Pessimistic locking` `PostgreSQL` `Flyway`

### [URL Shortener Service](https://github.com/Asyl-k/url-shortener-service)

[![CI](https://github.com/Asyl-k/url-shortener-service/actions/workflows/ci.yml/badge.svg)](https://github.com/Asyl-k/url-shortener-service/actions/workflows/ci.yml)

A URL shortener with Base62 codes, custom aliases, expiration and click counting. Alias uniqueness is enforced by a PostgreSQL constraint rather than a check-then-insert sequence, so 12 concurrent requests produce exactly one link. Hot links are cached in Caffeine and clicks are counted with an atomic `UPDATE`.

`Base62` `Caffeine` `PostgreSQL` `Flyway` `Atomic counters`

### [Booking Service](https://github.com/Asyl-k/booking-service)

[![CI](https://github.com/Asyl-k/booking-service/actions/workflows/ci.yml/badge.svg)](https://github.com/Asyl-k/booking-service/actions/workflows/ci.yml)

Resource bookings without double booking. An `EXCLUDE` constraint with `btree_gist` and `tstzrange(..., '[)')` rejects overlapping intervals: adjacent slots are allowed, while any real overlap fails even under concurrent requests. Cancellation frees the slot because the constraint only covers `CONFIRMED` bookings.

`PostgreSQL exclusion constraint` `btree_gist` `Concurrency` `Flyway`

## How the projects are built

- Every repository starts from its README: `docker compose up --build` or locally with PostgreSQL.
- The schema is managed by Flyway and Hibernate runs with `ddl-auto: validate`, so entity/migration drift fails startup.
- The API exposes DTOs and RFC 9457 `ProblemDetail` errors with a stable `code` field.
- Unit tests need no Docker; integration tests start `postgres:17-alpine` through Testcontainers.
- CI runs on every push, executes the tests, builds the image and smoke-tests the running stack.
- The Docker image runs as a non-root user.

## Where to look in the code

| Project | Start here | Why it is interesting |
|---|---|---|
| Task Manager API | `SecurityConfig`, `TaskService` | Ownership and role checks in the service layer, not only in controllers |
| Payment Ledger Service | `TransferExecutor`, `TransferService` | Stable lock order, idempotent replay, double-entry writes |
| URL Shortener Service | `ShortLinkService`, `V1__init.sql` | Retry for generated codes and a constraint against custom-alias races |
| Booking Service | `V1__init.sql`, `BookingService` | An exclusion constraint as the only reliable arbiter of overlaps |

## Archive

Early learning projects — [auth-service](https://github.com/Asyl-k/auth-service), [order-service](https://github.com/Asyl-k/order-service), [inventory-service](https://github.com/Asyl-k/inventory-service), [notification-service](https://github.com/Asyl-k/notification-service) and [api-gateway](https://github.com/Asyl-k/api-gateway) — are archived and not maintained. JWT authentication now lives in Task Manager API; the other repositories are kept as a learning history.

---

Это личные проекты для демонстрации инженерных подходов, а не описание коммерческого опыта. / These are personal projects that demonstrate engineering practices, not a description of commercial experience.
