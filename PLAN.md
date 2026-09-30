# План книги «Онлайн-платежи изнутри»

Книга-учебник для технических специалистов (разработчики, архитекторы, QA, аналитики, SRE, продакты), которые приходят работать в индустрию онлайн-платежей. Цель — не набор разрозненных определений, а **целостная картина**: кто участвует, как идут деньги и данные, где рождаются комиссии, где прячутся риски, как это всё строится в коде и как ломается в продакшене.

Правила написания — в [AGENTS.md](AGENTS.md). Оглавление — в [README.md](README.md).

Номера в скобках «(№…)» — номера тем из исходного перечня заказчика. Каждая тема обязана быть раскрыта в указанной главе (либо отдельным разделом, либо осмысленно внутри раздела). Структура книги намеренно не повторяет исходный перечень.

Файлы глав лежат в `chapters/`. Порядок построен как история: сначала карта местности, потом путь платежа, потом деньги и экономика, потом риски и закон, потом как это строить, и в финале — сквозные сценарии, где всё сходится.

---

## Часть I. Карта местности

### Глава 01. Как устроена индустрия онлайн-платежей — `01-industry-overview.md`
Зачем вообще нужна платёжная индустрия, краткая история (наличные → карты → e-commerce → wallets → instant/open banking), масштаб и деньги в отрасли, почему платежи сложнее, чем «вызвать API банка». Обзор уровней: бизнес, технологии, деньги, право. Как читать книгу. (№1, №2 обзорно)

### Глава 02. Участники платёжной экосистемы — `02-ecosystem-participants.md`
Четырёхсторонняя (и более) модель. Cardholder, Merchant, Issuer, Acquirer, Payment Network/Scheme, Processor, Gateway, PSP, PayFac, Merchant of Record, Marketplace и платёжная инфраструктура. Чем отличаются gateway / processor / PSP / PayFac / MoR (одна большая сравнительная секция), кто что делает, кто несёт риск, кто получает деньги, кто владеет отношениями с клиентом. Типовые «стеки» реальных компаний. (№2–13, №280–288)

---

## Часть II. Карты и их окружение

### Глава 03. Банковская карта: анатомия — `03-bank-card-anatomy.md`
Как работает карта физически и логически: PAN, BIN/IIN, алгоритм Луна, expiration date, CVV/CVC (и почему его нельзя хранить), магнитная полоса/чип/EMV, credit vs debit vs prepaid, MCC. Кто что видит в номере карты. (№32, 33, 36–39, 289, 290)

### Глава 04. Карточные сети и схемы — `04-card-networks.md`
Visa, Mastercard, American Express, UnionPay, JCB, Discover, Мир, национальные схемы, «частные» (closed-loop) vs «открытые» (four-party) схемы. Правила схем, членство, сборы, сертификации. Региональные особенности. (№10, 34, 35, 288)

### Глава 05. Где и как используется карта: CP/CNP, MOTO, credentials on file, токены — `05-card-contexts-and-tokens.md`
Card Present vs Card Not Present, MOTO, card-on-file, stored credentials (CIT/MIT, recurring, unscheduled, installment), tokenized cards, network tokens (Visa Token Service, MDES), PSP-токены, виртуальные карты (single-use, B2B). (№40–46)

---

## Часть III. Путь платежа

### Глава 06. Жизненный цикл карточного платежа — `06-payment-lifecycle.md`
Полный путь от нажатия «Оплатить» до денег на счёте продавца. Authorization, Capture (single/multiple/partial), Clearing, Settlement, Void, Refund, Partial refund, Reversal. Сообщения и файлы на каждом шаге, тайминги, единая и двойная схемы (SMS/DMS). (№14–23, 15)

### Глава 07. Состояния платежа, sync/async, webhooks, idempotency, retries — `07-states-async-idempotency.md`
Payment state machine, синхронные и асинхронные потоки, webhooks (надёжность, порядок, дубликаты), idempotency key, стратегии retries (client/merchant/PSP), smart retries и cascading. (№26–30, 189 обзорно)

### Глава 08. Аутентификация: 3-D Secure и SCA — `08-3ds-and-sca.md`
Authentication vs Authorization, 3DS1 → 3DS2/EMV 3DS, frictionless vs challenge, участники (3DS Server, Directory Server, ACS), SCA и PSD2, exemptions (low value, TRA, trusted beneficiary, MIT, …), liability shift, 3DS как инструмент против fraud. (№47–54, 124, 170, 317)

### Глава 09. Отказы и коды ответов — `09-declines-and-response-codes.md`
Почему платёж отклоняют: issuer decline, scheme decline, acquirer/PSP decline, fraud decline, техническая ошибка. Response code, decline code, authorization code, reason code, soft vs hard decline, рекомендации по retry (Merchant Advice Codes), как показывать ошибки пользователю. (№55, 237, 294–297)

---

## Часть IV. Платёжные методы за пределами карт

### Глава 10. Банковские переводы, прямые дебеты и Open Banking — `10-bank-based-methods.md`
Bank transfer, SEPA (SCT, SCT Inst, SDD), ACH, Faster Payments, Pix/UPI (как примеры instant-систем), iDEAL и подобные bank-redirect методы, Open Banking (PIS/AIS), VRP. Особенности: push vs pull, возвраты, отзыв платежа, финальность. (№56–62)

### Глава 11. Кошельки, BNPL, наличные и локальные методы — `11-wallets-bnpl-local-methods.md`
Digital wallets (staged/pass-through), Apple Pay / Google Pay (как работают токены и криптограммы), BNPL (Klarna-подобные модели), cash-based (vouchers, OXXO-подобные), локальные методы и почему без них не выйти на рынок, APM как класс, интеграционные паттерны APM. (№63–68)

---

## Часть V. Деньги

### Глава 12. Что происходит с деньгами — `12-flow-of-funds.md`
Физический путь денег при платеже: счета, корреспондентские и сеттлмент-счета, net settlement между банками и схемами. Settlement of funds, merchant balance, available vs pending, payouts (расписание, rolling), rolling reserve, held funds, negative balance. (№69–72, 78–83)

### Глава 13. Ledger, двойная запись и reconciliation — `13-ledger-and-reconciliation.md`
Бухгалтерия для инженеров: double-entry, план счетов платёжной компании, transaction ledger, immutability, проводки для auth/capture/refund/chargeback/payout/fee, accounting в платёжной системе. Reconciliation: три уровня (внутренний, с провайдером, с банком), matching, типичные расхождения, автоматизация. (№31, 73–77)

### Глава 14. Валюты и FX — `14-currencies-and-fx.md`
Multi-currency payments, presentment vs settlement currency, exponent (minor units), FX rates и их источники, спреды/markup, DCC, хеджирование на уровне PSP, ошибки округления. (№84–86, 273–275)

### Глава 15. Комиссии и экономика платежей — `15-fees-and-economics.md`
Как зарабатывает платёжный сервис: interchange, scheme fee, acquirer/processor fee, markup, MDR, fixed vs percent, blended vs IC++, take rate, unit economics, cost per transaction, gross margin, revenue share, FX markup, стоимость chargeback и refund. Числовые примеры полного «разреза» одного платежа. (№88–108)

---

## Часть VI. Риск

### Глава 16. Payment fraud: обнаружение и предотвращение — `16-fraud.md`
Виды мошенничества (stolen cards, ATO, card testing, carding, friendly fraud, chargeback fraud), fraud prevention vs detection, scoring, rules engine, velocity, device fingerprinting, IP/geo, behavioral analysis, ML, false positives, trade-off fraud vs conversion, организация fraud-команды. (№109–126, 318, 319)

### Глава 17. Chargebacks и disputes — `17-chargebacks-and-disputes.md`
Что такое chargeback, lifecycle (first chargeback, representment, pre-arbitration, arbitration), reason codes, dispute management, evidence, chargeback ratio и программы схем, fraud chargebacks, refund vs chargeback, автоматизация disputes (Ethoca/Verifi-подобные сервисы, RDR). (№24, 25, 127–138, 313, 314)

---

## Часть VII. Право и безопасность

### Глава 18. Регуляторика и compliance — `18-regulation-and-compliance.md`
PSD2, PSD3/PSR, Open Banking regulation, SCA (кратко, ссылка на гл. 08), лицензирование (PI, EMI, банковская лицензия), KYC/KYB/UBO, AML, transaction monitoring, sanctions/OFAC, merchant onboarding и verification, GDPR и data retention, финансовые преступления. (№141–158, 159)

### Глава 19. Безопасность платежей и PCI DSS — `19-payment-security-pci.md`
PCI DSS (версии, уровни, SAQ, scope и способы его уменьшения), архитектура безопасности card data, шифрование at rest / in transit, токенизация, HSM, key management, secrets management, API security, webhook security (подписи, replay), fraudulent API requests. (№139, 160–174)

---

## Часть VIII. Инженерия платёжной платформы

### Глава 20. Архитектура платёжной платформы и доменная модель — `20-platform-architecture.md`
Payment platform целиком: слои, сервисы, Payment API, Payment Intent vs Payment Order vs Transaction, Payment Method, Customer, Merchant, мультитенантность, версионирование API, идентификаторы (Transaction ID, idempotency key). (№175–183, 301–303)

### Глава 21. Распределённые системы и деньги — `21-distributed-systems-and-money.md`
Event-driven architecture, очереди, event sourcing, распределённые транзакции (saga, outbox, 2PC-и почему нет), идемпотентность, exactly-once vs at-least-once, консистентность, race conditions, duplicate payments, failure handling, timeouts, retries, dead-letter queues, архитектура reconciliation. (№184–198)

### Глава 22. Интеграции с банками, процессорами и схемами — `22-integrations.md`
Интеграция с acquirer, processor, card networks, ISO 8583 (подробно: MTI, bitmap, DE), ISO 20022, REST/SOAP bank APIs, SFTP и batch, settlement/clearing files, transaction reports, file-based processing, абстракции коннекторов, маршрутизация. (№199–211)

### Глава 23. Надёжность платёжных систем — `23-reliability.md`
High availability, failover, DR, BCP, multi-region, circuit breakers, timeouts/retries (бюджет), graceful degradation, duplicate prevention, exactly-once financial processing, инциденты, incident management, reconciliation после инцидента. (№212–225)

### Глава 24. Мониторинг и операционная работа — `24-monitoring-and-operations.md`
Метрики (success/auth/decline/conversion/3DS challenge/fraud/chargeback/refund rate, latency, failure rate), issuer decline vs technical decline, observability, dashboards, alerting, operational reconciliation, on-call в платежах. (№226–241)

---

## Часть IX. Бизнес-модели поверх платежей

### Глава 25. Merchant-side: всё про продавца — `25-merchant-domain.md`
Merchant onboarding, merchant account, конфигурация, pricing, balance, payout, refund, disputes, risk, limits, reserves, statements, reporting, dashboard, multi-merchant архитектура. (№152, 153, 242–256)

### Глава 26. Marketplace и split payments — `26-marketplace-and-split-payments.md`
Marketplace/platform payments, split payments, multiple beneficiaries, sub-merchants, connected accounts, commission splitting, platform fee, seller payouts, escrow vs payment processing, marketplace reconciliation, регуляторные аспекты (когда вы уже не просто платформа). (№11, 257–268)

### Глава 27. Международные платежи — `27-cross-border-payments.md`
Domestic vs international, local acquiring vs cross-border acquiring, международный settlement, correspondent banking (SWIFT, nostro/vostro), международные платёжные методы, региональные регуляции, выбор стратегии выхода на рынок. (№87, 269–273, 276–279)

---

## Часть X. Справочник и сценарии

### Глава 28. Глоссарий и идентификаторы — `28-glossary.md`
Терминология «в одном месте» с живыми пояснениями и указанием, где в системе встречается каждый идентификатор: Acquirer, Issuer, Processor, Gateway, PSP, PayFac, Merchant, Cardholder, Scheme, BIN, MCC, ARN, RRN, STAN, Authorization code, Response/Decline/Reason code, Statement descriptor, MID, TID, Payment Intent, Transaction ID, Idempotency Key и др. (№280–303)

### Глава 29. Сквозные сценарии I: путь платежа, отказы, сбои интеграции — `29-scenarios-part-1.md`
Полный путь оплаты картой; успешный платёж; отказ банка; технический сбой; потерянный webhook; дублированный webhook; повторная оплата клиентом; auth без capture; refund; 3DS; fraud-блокировка и ложная блокировка; платёж в другой валюте. (№304–312, 316–319)

### Глава 30. Сквозные сценарии II: деньги, диспуты и аварии — `30-scenarios-part-2.md`
Chargeback; нехватка денег у продавца; вывод денег; недоступность acquirer; недоступность провайдера; timeout при уже совершённом списании; множественный приём одной транзакции; восстановление состояния после падения сервиса; расхождение ledger и settlement. (№313–315, 320–325)

---

## Контрольная карта покрытия

Каждая тема исходного перечня (№1–№325) должна быть найдена в одной из глав выше. Если при написании главы автор обнаруживает тему без дома — он добавляет раздел в наиболее подходящую главу и отмечает это в конце своего отчёта.
