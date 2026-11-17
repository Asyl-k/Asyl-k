# Привет! Я Asyl 👋

Java Backend Developer. В этом портфолио собраны самостоятельные проекты, демонстрирующие практики, востребованные в production backend-разработке: транзакции, конкурентный доступ, идемпотентность, асинхронные события и автоматизированные проверки.

## Стек

`Java 21` · `Spring Boot 3` · `Spring Data JPA` · `PostgreSQL` · `Kafka` · `REST API` · `JUnit 5` · `Mockito` · `Maven` · `Docker` · `GitHub Actions`

## Проекты

| Проект | Что демонстрирует |
|---|---|
| [Auth Service](https://github.com/Asyl-k/auth-service) | Spring Security, JWT, BCrypt и stateless authentication |
| [API Gateway](https://github.com/Asyl-k/api-gateway) | Spring Cloud Gateway, маршрутизация и circuit breaker |
| [URL Shortener Service](https://github.com/Asyl-k/url-shortener-service) | Secure short codes, expiration, caching и click tracking |
| [Payment Ledger Service](https://github.com/Asyl-k/payment-ledger-service) | Переводы, идемпотентность, `BigDecimal`, блокировки счетов в стабильном порядке |
| [Inventory Service](https://github.com/Asyl-k/inventory-service) | Резервирование остатков и pessimistic locking против overselling |
| [Booking Service](https://github.com/Asyl-k/booking-service) | Проверка пересекающихся интервалов, границы временных слотов и отмена |
| [Order Service](https://github.com/Asyl-k/order-service) | Идемпотентное создание и конечный автомат состояний заказа |
| [Notification Service](https://github.com/Asyl-k/notification-service) | Kafka consumer, at-least-once delivery и дедупликация событий |
| [Task Manager API](https://github.com/Asyl-k/task-manager-api) | REST API, CRUD, валидация, OpenAPI, Docker Compose и CI |

## Практики

- Разделение HTTP, бизнес-логики и persistence-слоёв.
- Транзакционные границы, проверки инвариантов и обработка повторов.
- Unit-тесты бизнес-сценариев и CI на каждый репозиторий.

Это личные проекты для демонстрации архитектурных подходов и развития навыков; они не являются описанием коммерческого опыта.
