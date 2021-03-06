# Env переменные

Для работы приложения необходимо заполнить следующие env переменные (через командную строку или `.env` файл):
- `SENTRY_DSN`: DSN URL от Sentry
- `SENTRY_ENV`: окружение в Sentry (development/production/etc)
- `LOGDNA_KEY`: ключ от logDNA
- `LOGDNA_APP`: название приложение в logDNA, желательно с окончанием текущего окружения (-dev/-prod/-etc)
- `LOG_LEVEL`: "trace" | "debug" | "info" | "warn" | "error" | "fatal" (по-умолчанию "trace")
- `APOLLO_EXPLORER`: "true" включает локальный GraphQL Explorer
- `APOLLO_INTROSPECTION`: "true" включает интроспекцию
- `CORS_ORIGINS`: CORS URL разделенные запятой, для работы Apollo Studio должен включать "https://studio.apollographql.com"
- `SUPERUSER_TOKEN`: токен для авторизации запросов под директивой @superuser
- `DATABASE_URL`: connection url от PlanetScale
- `SHADOW_DATABASE_URL`: connection url от shadow ветки в PlanetScale, нужен только при локальной разработке

Заготовка уже есть в файле `.env.example`, его можно просто переименовать в `.env` и заполнить. Если проект задеплоен на Vercel, то для получения актуальных переменных Development окружения можно воспользоваться командой `vercel env pull`.


Для полноценной интеграции с Apollo Studio также необходимо проставить ещё пару переменных в Vercel:
- `APOLLO_KEY`: ключ от Apollo Studio
- `APOLLO_GRAPH_ID`: ID графа в Apollo Studio

Подробнее о Apollo Studio и его фичах можно почитать в [infrastructure.md](docs/infrastructure.md#Apollo%20Studio).


### Файл `src/env.ts`

В этом файле (и только в нём) производится чтение env переменных всего приложения, а уже из него они пробрасываются дальше. То есть чтение `process.env` вне этого файла запрещено.