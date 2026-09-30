# Онлайн-платежи изнутри

Учебник для технических специалистов, которые приходят работать в индустрию онлайн-платежей. Книга идёт от общей карты местности к деталям: кто участвует, как проходит платёж, куда текут деньги, как платёжные компании зарабатывают, где прячутся риски, что требует закон и как всё это построить и эксплуатировать.

Как устроена книга: [PLAN.md](PLAN.md). Правила написания: [AGENTS.md](AGENTS.md).

Сквозные герои книги: покупательница Аня, интернет-магазин «Кофейня», PSP «Платёжка», эквайер «Банк Эквайр» и эмитент «Банк Север». Все вымышленные.

---

## Часть I. Карта местности

- [Глава 01. Как устроена индустрия онлайн-платежей](chapters/01-industry-overview.md)
- [Глава 02. Участники платёжной экосистемы](chapters/02-ecosystem-participants.md)

## Часть II. Карты и их окружение

- [Глава 03. Банковская карта: анатомия](chapters/03-bank-card-anatomy.md)
- [Глава 04. Карточные сети и схемы](chapters/04-card-networks.md)
- [Глава 05. Где и как используется карта: CP/CNP, MOTO, credentials on file, токены](chapters/05-card-contexts-and-tokens.md)

## Часть III. Путь платежа

- [Глава 06. Жизненный цикл карточного платежа](chapters/06-payment-lifecycle.md)
- [Глава 07. Состояния платежа, sync/async, webhooks, idempotency, retries](chapters/07-states-async-idempotency.md)
- [Глава 08. Аутентификация: 3-D Secure и SCA](chapters/08-3ds-and-sca.md)
- [Глава 09. Отказы и коды ответов](chapters/09-declines-and-response-codes.md)

## Часть IV. Платёжные методы за пределами карт

- [Глава 10. Банковские переводы, прямые дебеты и Open Banking](chapters/10-bank-based-methods.md)
- [Глава 11. Кошельки, BNPL, наличные и локальные методы](chapters/11-wallets-bnpl-local-methods.md)

## Часть V. Деньги

- [Глава 12. Что происходит с деньгами](chapters/12-flow-of-funds.md)
- [Глава 13. Ledger, двойная запись и reconciliation](chapters/13-ledger-and-reconciliation.md)
- [Глава 14. Валюты и FX](chapters/14-currencies-and-fx.md)
- [Глава 15. Комиссии и экономика платежей](chapters/15-fees-and-economics.md)

## Часть VI. Риск

- [Глава 16. Payment fraud: обнаружение и предотвращение](chapters/16-fraud.md)
- [Глава 17. Chargebacks и disputes](chapters/17-chargebacks-and-disputes.md)

## Часть VII. Право и безопасность

- [Глава 18. Регуляторика и compliance](chapters/18-regulation-and-compliance.md)
- [Глава 19. Безопасность платежей и PCI DSS](chapters/19-payment-security-pci.md)

## Часть VIII. Инженерия платёжной платформы

- [Глава 20. Архитектура платёжной платформы и доменная модель](chapters/20-platform-architecture.md)
- [Глава 21. Распределённые системы и деньги](chapters/21-distributed-systems-and-money.md)
- [Глава 22. Интеграции с банками, процессорами и схемами](chapters/22-integrations.md)
- [Глава 23. Надёжность платёжных систем](chapters/23-reliability.md)
- [Глава 24. Мониторинг и операционная работа](chapters/24-monitoring-and-operations.md)

## Часть IX. Бизнес-модели поверх платежей

- [Глава 25. Merchant-side: всё про продавца](chapters/25-merchant-domain.md)
- [Глава 26. Marketplace и split payments](chapters/26-marketplace-and-split-payments.md)
- [Глава 27. Международные платежи](chapters/27-cross-border-payments.md)

## Часть X. Справочник и сценарии

- [Глава 28. Глоссарий и идентификаторы](chapters/28-glossary.md)
- [Глава 29. Сквозные сценарии I: путь платежа, отказы, сбои интеграции](chapters/29-scenarios-part-1.md)
- [Глава 30. Сквозные сценарии II: деньги, диспуты и аварии](chapters/30-scenarios-part-2.md)

---

## Как читать

- **Новичку в индустрии** — подряд, части I–VI, затем сценарии (глава 29–30) как закрепление.
- **Инженеру, который строит платёжный бэкенд** — главы 02, 06, 07, затем часть VIII, затем 12–13.
- **Аналитику и продакту** — главы 01–02, 06, 09, 15–17, 24.
- **Перед собеседованием или онбордингом** — глава 28 (глоссарий) и сценарии 29–30.
