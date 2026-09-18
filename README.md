# SoilScout — деплой на Vercel

Це статичний сайт (один самодостатній `index.html`: HTML + CSS + vanilla JS,
Chart.js підключається з CDN). Build-кроку немає, TypeScript немає —
Vercel просто роздає файл як є.

## Локальний перегляд

Відкрий `index.html` у браузері напряму, або через локальний сервер:

```bash
npx serve .
# або
python3 -m http.server 5173
```

## Деплой на Vercel

### Варіант 1 — Vercel CLI
```bash
npm i -g vercel
cd deploy
vercel        # прев'ю-деплой
vercel --prod # продакшн
```
Vercel запитає Framework Preset — обери **Other** (це не Next.js/Vite-проєкт).

### Варіант 2 — через дашборд Vercel
1. Заливаєш цю папку (`index.html` + `vercel.json`) у Git-репозиторій (GitHub/GitLab).
2. New Project → Import Repository у Vercel.
3. Framework Preset: **Other**. Build Command і Output Directory залишити порожніми
   (Vercel сам віддасть `index.html` з кореня).
4. Deploy.

## Перевірено перед деплоєм
- Синтаксис вбудованого JS перевірено через `node --check` — помилок немає.
- Усі HTML-теги збалансовані (`<section>`, `<div>` — open/close рахунок співпадає).
- Усі 10 секцій присутні й у правильному порядку: Hero → Сенсори → Як це працює →
  Переваги → Моніторинг поля → Аналіз ґрунту/Підбір добрив → Графіки → Панель робота → CTA → Footer.
- Зовнішні залежності — лише CDN-скрипт Chart.js (`cdnjs.cloudflare.com`) та шрифти Google Fonts.

## Чому не React/Vite/TypeScript-проєкт
Оригінальний бриф допускав такий стек лише "якщо він не заданий інакше";
середовище, в якому я працюю зараз, публікує сайти як один живий, одразу
відкриваний HTML-файл (без build-кроку) і не має мережевого доступу для
`npm install`, тож я не можу тут виконати й перевірити реальний
`npm run dev` / `npm run build` для Vite-проєкту.

Якщо тобі принципово потрібен саме React + TypeScript + Vite (з окремим
`recommendationEngine.ts` тощо) для деплою через Vercel's Vite-preset —
скажи, і я згенерую повний вихідний код проєкту (package.json, vite.config.ts,
tsconfig.json, src/…). Але зверни увагу: я зможу лише статично, вручну
перевірити типи й синтаксис — реальний `npm install` і `npm run build`
доведеться запустити тобі локально або дати виконати самому Vercel під час
деплою, оскільки в цьому середовищі немає доступу до npm-реєстру.
