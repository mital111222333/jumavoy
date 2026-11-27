# JUMAVOY — личный AI-ассистент

Отдельный репозиторий ассистента. CRM — в [mital111222333/MitalCRM](https://github.com/mital111222333/MitalCRM).

## Что здесь

| Папка / файл | Что это |
|---|---|
| `supabase/functions/ai-bot` | JUMAVOY владельца (Telegram @MitalAI_bot). Подробно: `HANDOFF.md` там же |
| `supabase/functions/team-bot` | JUMAVOY для агентов (каждый видит только свой кабинет) |
| `tasks.html`, `wallet.html` | Mini App: 📋 доска задач и 👛 кошелёк (GitHub Pages) |
| `jumavoy/`, `android/` | веб-приложение и Android-обёртка (APK — релиз `jumavoy-app`) |
| `supabase/migrations` | миграции таблиц бота (`ai_*`, `team_*`, `crm_inbox`, `ai_outbox`) |
| `tests/` | проверки страниц в headless Chrome (не в CI) |

## Как связан с MitalCRM

Только через **общую базу Supabase** (проект `oxchgcfyzszemqlvdjjr`), не через код:
- CRM пишет сводку для бота (`botsnap.js` в MitalCRM → `workspaces/<owner>/bot.json.gz`), бот её читает;
- поручения бота в CRM идут через таблицу `crm_inbox` (`botinbox.js` в MitalCRM их забирает);
- задания агентам — в `agent_cabinets`.

Меняете формат этих данных в одном репозитории — проверьте другой.

Миграции, применённые до разделения (27.11.2026), остались и в MitalCRM как история. Новые миграции таблиц бота — сюда, таблиц CRM — в MitalCRM.

## Выкладка

`git push` в `main` → GitHub Actions (`checks`): тесты обоих ботов → выкладка в Supabase. Нужен секрет репозитория `SUPABASE_ACCESS_TOKEN`; без него выкладка пропускается.

Mini App открываются с `https://mital111222333.github.io/jumavoy/` (GitHub Pages из `main`, корень).

Тесты локально: `cd supabase/functions/ai-bot && deno test -A index.test.ts`.
