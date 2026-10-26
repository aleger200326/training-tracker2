# GEORGRAD 2

Переработанная версия дневника тренировок для дома и зала. Интерфейс доступен на русском, узбекском и английском языках, со светлой и тёмной темой.

- **Версия 2:** [georgrad2.vercel.app](https://georgrad2.vercel.app/)
- **Исходный код версии 2:** [training-tracker2](https://github.com/aleger200326/training-tracker2)
- **Прежняя версия:** [georgrad.vercel.app](https://georgrad.vercel.app/) и [training-tracker](https://github.com/aleger200326/training-tracker)

## Данные и вход

Вход работает через Neon Auth, а профиль, планы и занятия сохраняются через Neon Data API в таблице `workout_data`. Для таблицы включена политика RLS: вошедший пользователь видит только свою запись. Схема находится в [`neon/schema.sql`](neon/schema.sql).

Версии 1 и 2 сейчас используют **один проект Neon** (`patient-mode-65011168`). Если войти в обе версии под одной учётной записью, они увидят общие данные. Репозитории и проекты Vercel при этом независимы. Вторая версия не использует локальную базу браузера для аккаунтов и тренировок.

Если тренировки остались только на старом [сайте GitHub Pages](https://aleger200326.github.io/training-tracker/), экспортируйте JSON в его профиле, затем войдите во вторую версию и импортируйте файл в профиле. Сохраните файл как резервную копию.

## Локальный запуск

```bash
pnpm install
Copy-Item .env.example .env.local
pnpm dev
```

Заполните `.env.local` публичными HTTPS адресами Neon Auth и Data API. Файл исключён из Git. Для проверки сборки используйте `pnpm build`.

## Публикация

Репозиторий `aleger200326/training-tracker2` подключён к отдельному проекту Vercel `georgrad2`. Ветка `main` публикуется на `georgrad2.vercel.app`. Адреса Neon хранятся в переменных окружения Vercel `VITE_NEON_AUTH_URL` и `VITE_NEON_DATA_API_URL` для Production, Preview и Development. Пароль PostgreSQL и другие секреты не входят в клиентский код. Домен второй версии добавлен в доверенные домены Neon Auth.

Каталог упражнений использует [free-exercise-db](https://github.com/yuhonas/free-exercise-db) ([Unlicense](https://github.com/yuhonas/free-exercise-db/blob/main/LICENSE.md)).
