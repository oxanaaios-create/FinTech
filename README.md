# {{PROJECT_NAME}}

Пространство проекта сайта. Один репозиторий — один проект: исследование, бренд-кит, решения, код и дневной лог работы. Всё, что важно для проекта, живёт здесь, а не в чатах.

Тип: {{PROJECT_TYPE}} · Старт: {{START_DATE}} · Паспорт проекта: [PROJECT.md](PROJECT.md)

---

## Старт нового проекта

| Шаг | Действие | Критерий приёмки |
|---|---|---|
| 1 | На GitHub: **Use this template → Create a new repository**, имя `<client>-site`, Private | Репозиторий создан, CI запустился |
| 2 | `npm run init -- "Название" commission` (или `concept`) | Плейсхолдеры `{{…}}` заменены, создан первый devlog |
| 3 | Заполнить [PROJECT.md](PROJECT.md) и [docs/brief.md](docs/brief.md) | Нет пустых полей, неизвестное помечено `[DATA NEEDED]` |
| 4 | `npm run day -- "Старт проекта"` | Первый коммит дня в main, CI зелёный |

Node 18+ без зависимостей. `npm install` не нужен.

## Роутер: задача → что читать → куда писать

| Задача | Читать | Писать |
|---|---|---|
| Начало рабочего дня | `CLAUDE.md`, `PROJECT.md`, два последних файла в `docs/devlog/` | `docs/devlog/<дата>.md` |
| Исследование бренда | `research/*` | `research/facts.md`, `research/hypotheses.md` |
| Стратегия и голос | подтверждённые гипотезы | `verbal/*` |
| Дизайн-система | `research/refs.md`, `visual/*` | `visual/visual-system.json` → `npm run tokens` |
| Сайт | `recipes/website.md`, `visual/tokens.css`, `verbal/voice-and-tone.md` | `site/` |
| Брендбук | `recipes/brandbook.md` | `outputs/brandbook/` |
| Кейс для Behance | `docs/decisions.md`, `docs/devlog/` | `outputs/behance/` |
| Любое решение | — | `docs/decisions.md` |
| Новая задача | `docs/plan.md` | `docs/plan.md` или Issue по шаблону «Задача» |
| Сдача клиенту | `docs/handoff.md` | `docs/handoff.md`, `CHANGELOG.md` |

## Структура

```
├── README.md            этот роутер
├── CLAUDE.md            правила для Claude в этом репо
├── PROJECT.md           паспорт: клиент, цель, стек, ссылки, этап
├── CHANGELOG.md         версии сайта для клиента
├── magic_trick.md       идея-фишка проекта, слот в hero
├── _retrieval-rules.yaml что грузить агенту под каждую задачу
├── docs/
│   ├── brief.md         бриф
│   ├── plan.md          задачи с критериями приёмки
│   ├── decisions.md     журнал решений: до / после / почему
│   ├── handoff.md       чеклист сдачи
│   └── devlog/          лог по дням: YYYY-MM-DD.md
├── research/            факты, гипотезы, референсы, конкуренты, скрины
├── verbal/              стратегия, позиционирование, голос, термины
├── visual/              visual-system.json (источник) → tokens.css, правила
├── assets/              logo/, fonts/, imagery/
├── examples/            good/ эталоны, bad/ анти-примеры
├── evals/               чеклист и планка качества
├── recipes/             рецепты: сайт, брендбук, кейс
├── site/                код сайта, только на токенах
├── outputs/             брендбук, кейс
├── scripts/             токены, проверки, devlog, коммит дня
└── .github/             CI, шаблон задачи, шаблон PR
```

## Команды

| Команда | Что делает |
|---|---|
| `npm run init -- "Имя" concept\|commission` | Заполняет плейсхолдеры, создаёт первый devlog и решение «Старт» |
| `npm run tokens` | `visual/visual-system.json` → `visual/tokens.css` и `site/styles/tokens.css` |
| `npm run check` | Токены + дизайн-система + сайт без значений вне токенов + задачи с критериями |
| `npm run devlog` | Создаёт лог сегодняшнего дня из шаблона |
| `npm run day -- "итог дня"` | Проверки → коммит `day: <дата> — итог` → push |
| `python3 scripts/palette.py assets/imagery/*.jpg` | Палитра из изображений (k-means) |

## Правила проекта

1. **Задача без критерия приёмки — не задача.** CI падает, если в `docs/plan.md` есть строка без критерия.
2. **Коммит дня обязателен.** В конце каждого рабочего дня: код + `docs/devlog/<дата>.md` + новые записи в `docs/decisions.md`, одной командой `npm run day`.
3. **Решение записывается сразу**: дата, решение, до → после, почему, ссылка на факт или референс.
4. **В `site/` нет цветов и размеров вне `tokens.css`.** CI проверяет.
5. **Факты не выдумываются.** Нет данных — `[DATA NEEDED]`.
6. **Концепт реального бренда** помечается «Unofficial concept, not affiliated with <brand>» на сайте и в кейсе.
7. Секреты (`.env`, ключи) не коммитятся.

## Сообщения коммитов

`day:` итог дня · `feat:` новая секция или функция · `fix:` исправление · `ds:` дизайн-система · `docs:` документы и исследование · `chore:` служебное.
