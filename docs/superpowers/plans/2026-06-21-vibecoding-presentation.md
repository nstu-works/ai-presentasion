# Vibecoding Presentation Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a complete Reveal.js presentation (~39 slides) about vibecoding personal experience with custom dark theme, fragment animations, and speaker notes.

**Architecture:** Reveal.js Full Setup cloned from GitHub into `revealjs/` subfolder. All slides in `revealjs/index.html`, built incrementally section by section. Custom theme in `revealjs/css/custom.css`. Assets copied flat into `revealjs/assets/`.

**Tech Stack:** Reveal.js 5.x, Node.js 20.19.0+, HTML5, CSS3, Inter + JetBrains Mono (Google Fonts)

## Global Constraints

- Clone path: `C:\Users\lebowsskii\Files\additional\projects\AI-presentation\revealjs\`
- Server: `npm start` from within `revealjs/` → `http://localhost:8000`
- Background: `#0f1117` | Text: `#f0f0f0` | Accent: `#7C6FF7`
- Headings: Inter 700 ≥48px | Body: Inter 400 28–32px | Code: JetBrains Mono 24px
- All `<li>` bullet points: `class="fragment"` (appear one by one)
- Tables: appear whole (no fragment wrapper)
- Outer section transition: `fade` | Inner section transition: `slide`
- Progress bar: enabled, color `#7C6FF7`
- Speaker notes: `<aside class="notes">` on every slide, activated with `S`
- Assets: `assets/<filename>` flat — no subfolders
- Language: Russian main text, English for technical terms

---

### Task 1: Project Setup

**Files:**
- Create: `revealjs/` (git clone)
- Create: `revealjs/assets/` (images copied here)
- Create: `revealjs/css/` (directory for custom theme)

**Interfaces:**
- Produces: running dev server at `http://localhost:8000`, `revealjs/assets/` with all 9 images

- [ ] **Step 1: Clone reveal.js**

Run in PowerShell from `C:\Users\lebowsskii\Files\additional\projects\AI-presentation\`:

```powershell
git clone https://github.com/hakimel/reveal.js.git revealjs
```

Expected output ends with: `Resolving deltas: 100% ...`

- [ ] **Step 2: Install dependencies**

```powershell
cd revealjs
npm install
```

Expected: `added N packages in Xs`

- [ ] **Step 3: Copy all images into assets/**

```powershell
New-Item -ItemType Directory -Path "assets" -Force
Copy-Item "..\*.png" -Destination "assets\"
```

Expected: 9 files in `assets/`:
`brainstorming.png`, `claude_plans.png`, `dispatch.png`, `my_qr.png`,
`paperclip_1.png`, `paperclip_2.png`, `paperclip_3.png`, `paperclip_4.png`, `writing_plans.png`

Verify count:
```powershell
(Get-ChildItem assets\).Count
```
Expected: `9`

- [ ] **Step 4: Verify server starts**

```powershell
npm start
```

Open `http://localhost:8000` in browser.
Expected: Default reveal.js demo presentation loads with horizontal slides.

Stop server: `Ctrl+C`

---

### Task 2: Custom CSS Theme

**Files:**
- Create: `revealjs/css/custom.css`

**Interfaces:**
- Produces: CSS classes `.accent`, `.big-quote`, `.meta`, `.cards`, `.card`, `.accent-card`, `.grid-2x2`, `.grid-item`, `.accent-item`, `.flow-chain`, `.flow-step`, `.fan-diagram`

- [ ] **Step 1: Create css/custom.css**

Create file `revealjs/css/custom.css` with this content:

```css
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;700&family=JetBrains+Mono:wght@400&display=swap');

:root {
  --r-background-color: #0f1117;
  --r-main-color: #f0f0f0;
  --r-heading-color: #f0f0f0;
  --r-link-color: #7C6FF7;
  --r-link-color-hover: #9b95f9;
  --r-heading-font: 'Inter', sans-serif;
  --r-main-font: 'Inter', sans-serif;
  --r-code-font: 'JetBrains Mono', monospace;
  --r-heading-font-weight: 700;
  --r-heading-text-transform: none;
  --r-main-font-size: 30px;
}

.reveal .progress {
  background: rgba(124, 111, 247, 0.2);
  color: #7C6FF7;
}

.reveal h1 { font-size: 2.2em; }
.reveal h2 { font-size: 1.6em; }
.reveal h3 { font-size: 1.2em; }

.reveal code {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.8em;
  background: rgba(124, 111, 247, 0.15);
  padding: 0.1em 0.4em;
  border-radius: 4px;
}

.accent { color: #7C6FF7; }
.accent-strong { color: #7C6FF7; font-weight: 700; }

.big-quote {
  font-size: 1.3em;
  font-weight: 700;
  line-height: 1.3;
}

.meta {
  font-size: 0.65em;
  color: #888;
  margin-top: 0.5em;
}

.subtitle {
  font-size: 0.9em;
  color: #ccc;
  margin-top: 0.3em;
}

/* Cards for product overview */
.cards {
  display: flex;
  gap: 1rem;
  justify-content: center;
  flex-wrap: wrap;
  margin: 1.5rem 0;
}

.card {
  background: rgba(255,255,255,0.06);
  border: 1px solid rgba(255,255,255,0.12);
  border-radius: 12px;
  padding: 1rem 1.5rem;
  font-size: 0.85em;
  text-align: center;
  min-width: 120px;
  display: flex;
  flex-direction: column;
  gap: 0.4em;
}

.accent-card {
  border-color: #7C6FF7;
  background: rgba(124, 111, 247, 0.12);
}

/* 2×2 grid for Claude ecosystem */
.grid-2x2 {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.2rem;
  margin: 1.5rem auto;
  max-width: 800px;
}

.grid-item {
  background: rgba(255,255,255,0.06);
  border: 1px solid rgba(255,255,255,0.12);
  border-radius: 12px;
  padding: 1.2rem;
  text-align: left;
  display: flex;
  flex-direction: column;
  gap: 0.3em;
}

.grid-item strong { font-size: 1em; color: #f0f0f0; }
.grid-item span { font-size: 0.7em; color: #aaa; }

.accent-item {
  border-color: #7C6FF7;
  background: rgba(124, 111, 247, 0.12);
}

/* Flow chain for dev flow diagram */
.flow-chain {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
  gap: 0.3rem;
  margin: 1.5rem 0;
  font-size: 0.75em;
}

.flow-step {
  background: rgba(124, 111, 247, 0.15);
  border: 1px solid #7C6FF7;
  border-radius: 8px;
  padding: 0.4em 0.8em;
  white-space: nowrap;
}

.flow-arrow {
  color: #7C6FF7;
  font-size: 1.2em;
}

/* Fan-out / fan-in diagram */
.fan-diagram {
  display: flex;
  align-items: flex-start;
  justify-content: center;
  gap: 1rem;
  margin: 1rem 0;
  font-size: 0.7em;
}

.fan-center { display: flex; flex-direction: column; align-items: center; gap: 0.5rem; }
.fan-branches { display: flex; flex-direction: column; gap: 0.4rem; }
.fan-node {
  background: rgba(124, 111, 247, 0.15);
  border: 1px solid #7C6FF7;
  border-radius: 6px;
  padding: 0.3em 0.8em;
  text-align: center;
}
.fan-main {
  background: #7C6FF7;
  color: #0f1117;
  font-weight: 700;
  border-radius: 8px;
  padding: 0.5em 1em;
}
.fan-arrow-col { display: flex; flex-direction: column; justify-content: center; font-size: 1.5em; color: #7C6FF7; }

/* Two-column layout */
.two-col {
  display: flex;
  gap: 2rem;
  align-items: flex-start;
  justify-content: center;
}

.two-col > div { flex: 1; text-align: left; }

/* Table styling */
.reveal table {
  font-size: 0.72em;
  border-collapse: collapse;
  width: 100%;
}
.reveal table th {
  background: rgba(124, 111, 247, 0.25);
  padding: 0.6em 1em;
}
.reveal table td {
  padding: 0.5em 1em;
  border-bottom: 1px solid rgba(255,255,255,0.08);
}
.reveal table tr:hover td { background: rgba(255,255,255,0.04); }

/* Skill name highlight */
.skill-name {
  font-family: 'JetBrains Mono', monospace;
  color: #7C6FF7;
  font-size: 0.85em;
}

/* Image helpers */
.reveal img {
  border-radius: 8px;
  max-height: 45vh;
  object-fit: contain;
}

/* Separator line */
.rule {
  border: none;
  border-top: 1px solid rgba(124, 111, 247, 0.3);
  margin: 1rem 0;
}
```

- [ ] **Step 2: Verify styles load**

Start server (`npm start`), open `http://localhost:8000`.
Open browser DevTools → Network tab.
Expected: `css/custom.css` is NOT yet loaded (it will be after Task 3 wires it in).
This step just confirms the file was created without syntax errors via DevTools Source.

---

### Task 3: HTML Scaffold + Section 0 (Opening — 3 slides)

**Files:**
- Modify: `revealjs/index.html` (replace default content completely)

**Interfaces:**
- Produces: working Reveal.js presentation with Sections 0.1 (Title), 0.2 (Disclaimer), 0.3 (TOC placeholder)

- [ ] **Step 1: Replace index.html with scaffold + Section 0**

Replace the entire content of `revealjs/index.html` with:

```html
<!doctype html>
<html lang="ru">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>Вайбкодинг — мой опыт</title>
  <link rel="stylesheet" href="dist/reset.css">
  <link rel="stylesheet" href="dist/reveal.css">
  <link rel="stylesheet" href="dist/theme/black.css">
  <link rel="stylesheet" href="plugin/highlight/monokai.css">
  <link rel="stylesheet" href="css/custom.css">
</head>
<body>
<div class="reveal">
<div class="slides">

<!-- ============================================================ -->
<!-- РАЗДЕЛ 0 — Открытие (3 slides) -->
<!-- ============================================================ -->
<section>

  <!-- 0.1 Титул -->
  <section data-transition="fade">
    <h1>Вайбкодинг</h1>
    <p class="subtitle">Мой опыт, мой стек, мои грабли</p>
    <br>
    <p class="meta">Имя докладчика &bull; 2026</p>
    <aside class="notes">Приветствие. Кратко о себе. Настройте аудиторию — это будет разговор, а не лекция.</aside>
  </section>

  <!-- 0.2 Дисклеймер -->
  <section data-transition="slide">
    <p class="big-quote accent">Это не инструкция.</p>
    <p class="big-quote">Это то, что работает у меня.</p>
    <br>
    <p class="fragment">Личный опыт — не научное исследование.</p>
    <p class="fragment">Не универсальный рецепт.</p>
    <p class="fragment">Ваш флоу может быть другим — и это нормально.</p>
    <aside class="notes">Сразу снять ожидания. Это история, не туториал. Вы можете слушать и брать только то, что вам подходит.</aside>
  </section>

  <!-- 0.3 Оглавление -->
  <section data-transition="slide">
    <h2>Что будет сегодня</h2>
    <ol style="font-size: 0.75em; columns: 2; column-gap: 3rem;">
      <li class="fragment">AI-продукты на рынке</li>
      <li class="fragment">Продукты Claude Code</li>
      <li class="fragment">Теоретический флоу</li>
      <li class="fragment">Проблемы ручной работы</li>
      <li class="fragment">Что такое скиллы</li>
      <li class="fragment">Интересные скиллы</li>
      <li class="fragment">Мой стек</li>
      <li class="fragment">Мой флоу</li>
      <li class="fragment">Фишки</li>
      <li class="fragment">Куда расти</li>
      <li class="fragment">Ресурсы</li>
    </ol>
    <aside class="notes">Roadmap доклада. Проходим последовательно — каждый раздел самодостаточен.</aside>
  </section>

</section>
<!-- END РАЗДЕЛ 0 -->

</div><!-- .slides -->
</div><!-- .reveal -->

<script src="dist/reveal.js"></script>
<script src="plugin/notes/notes.js"></script>
<script src="plugin/highlight/highlight.js"></script>
<script src="plugin/markdown/markdown.js"></script>
<script>
  Reveal.initialize({
    hash: true,
    progress: true,
    controls: true,
    center: true,
    transition: 'fade',
    plugins: [ RevealNotes, RevealHighlight, RevealMarkdown ]
  });
</script>
</body>
</html>
```

- [ ] **Step 2: Start server and verify Section 0**

```powershell
npm start
```

Open `http://localhost:8000`. Verify:
- Background is dark (`#0f1117`)
- Heading "Вайбкодинг" is large and white
- Subtitle and meta text visible
- Progress bar shows in purple at bottom
- Press Space/→ → slides within Section 0 advance
- Press S → speaker notes window opens with notes text
- Fragments appear one by one on Space/click

Stop server: `Ctrl+C`

---

### Task 4: Section 1 — AI Products (6 slides)

**Files:**
- Modify: `revealjs/index.html` (insert Section 1 before `</div><!-- .slides -->`)

**Interfaces:**
- Consumes: `.cards`, `.card`, `.accent-card`, `.accent` CSS classes from `css/custom.css`
- Produces: 6 slides covering ChatGPT/Codex, Deepseek, Cursor, Gemini, Claude

- [ ] **Step 1: Add Section 1 to index.html**

In `revealjs/index.html`, find the comment `<!-- END РАЗДЕЛ 0 -->` and insert the following block after it (before `</div><!-- .slides -->`):

```html
<!-- ============================================================ -->
<!-- РАЗДЕЛ 1 — AI-продукты на рынке (6 slides) -->
<!-- ============================================================ -->
<section>

  <!-- 1.0 Обзор -->
  <section data-transition="fade">
    <h2>AI-продукты на рынке</h2>
    <div class="cards">
      <div class="card fragment">
        <strong>ChatGPT</strong>
        <span style="font-size:0.75em;color:#aaa;">/ Codex</span>
      </div>
      <div class="card fragment">
        <strong>Deepseek</strong>
      </div>
      <div class="card fragment">
        <strong>Cursor</strong>
      </div>
      <div class="card fragment">
        <strong>Gemini</strong>
      </div>
      <div class="card accent-card fragment">
        <strong>Claude</strong>
      </div>
    </div>
    <p class="meta fragment">Не реклама. Личное мнение.</p>
    <aside class="notes">Быстрый обзор ландшафта. Не претендую на полноту — только то, с чем работал лично.</aside>
  </section>

  <!-- 1.1 ChatGPT / Codex -->
  <section data-transition="slide">
    <h2>ChatGPT / Codex</h2>
    <ul>
      <li class="fragment">IDE с поддержкой Android/iOS — подключаешь телефон по USB, AI тестирует приложение</li>
      <li class="fragment">Удобный выбор элементов для редактирования во фронтенде</li>
      <li class="fragment">Сильная экосистема для полноценной разработки приложений</li>
    </ul>
    <br>
    <p class="accent fragment">&laquo;Лучший выбор для мобильной разработки и фронтенда&raquo;</p>
    <aside class="notes">USB-тестирование: подключаешь девайс → IDE видит его → AI запускает тесты прямо на устройстве. Для фронтенда — наводишь на элемент, кликаешь, указываешь AI что изменить. Экосистема зрелее для мобайла.</aside>
  </section>

  <!-- 1.2 Deepseek -->
  <section data-transition="slide">
    <h2>Deepseek</h2>
    <ul>
      <li class="fragment">Интерфейс оставляет желать лучшего</li>
      <li class="fragment">Справляется с задачами — результат есть</li>
    </ul>
    <br>
    <p class="accent fragment">&laquo;Выглядит как помойка — работает&raquo;</p>
    <aside class="notes">Честная оценка: UX страдает, но за деньги — достойный вариант. Если нужен результат и не важен комфорт — Deepseek справится.</aside>
  </section>

  <!-- 1.3 Cursor -->
  <section data-transition="slide">
    <h2>Cursor</h2>
    <ul>
      <li class="fragment">Дешёвая, нетребовательная модель</li>
      <li class="fragment">Хорошо справляется с задачами низкого и среднего уровня сложности</li>
    </ul>
    <br>
    <p class="accent fragment">&laquo;Бюджетный вариант для повседневных задач&raquo;</p>
    <aside class="notes">Хорошо для рутины: небольшие правки, простые фичи, рефакторинг. Не тратишь деньги на тяжёлую модель там, где это не нужно.</aside>
  </section>

  <!-- 1.4 Gemini -->
  <section data-transition="slide">
    <h2>Gemini</h2>
    <ul>
      <li class="fragment">Отлично генерирует тексты</li>
      <li class="fragment">Идеален для копирайтеров и работы с контентом</li>
    </ul>
    <br>
    <p class="accent fragment">&laquo;Лучший для работы с текстом&raquo;</p>
    <aside class="notes">Для разработки менее интересен, но если нужно написать README, документацию, маркетинговые тексты — Gemini в топе.</aside>
  </section>

  <!-- 1.5 Claude -->
  <section data-transition="slide">
    <h2>Claude</h2>
    <ul>
      <li class="fragment">Самая умная нейронка на рынке</li>
      <li class="fragment">Подходит для всех видов работ</li>
      <li class="fragment">Скиллы переносимы на другие нейронки — но Claude удобнее: тема хорошо развита</li>
    </ul>
    <br>
    <p class="accent fragment">&laquo;Топ, пушка — но дорого&raquo;</p>
    <aside class="notes">«Зафоршенная тема» = большое комьюнити, активная экосистема скиллов, много туториалов. Скиллы технически работают с любой нейронкой через похожие CLI, но для Claude инфраструктура самая зрелая.</aside>
  </section>

</section>
<!-- END РАЗДЕЛ 1 -->
```

- [ ] **Step 2: Verify Section 1 in browser**

```powershell
npm start
```

Open `http://localhost:8000`. Press Right arrow to navigate to Section 1.
Verify:
- 5 product cards appear one by one on clicks
- "Не реклама. Личное мнение." appears last
- Each product slide has bullets appearing as fragments
- Accent quote appears last on each slide
- Press S → speaker notes visible

Stop server: `Ctrl+C`

---

### Task 5: Section 2 — Claude Products (5 slides)

**Files:**
- Modify: `revealjs/index.html`

**Interfaces:**
- Consumes: `.grid-2x2`, `.grid-item`, `.accent-item`, `.two-col`, `.accent` CSS classes; `assets/claude_plans.png`, `assets/dispatch.png`
- Produces: 5 slides: ecosystem overview, plans & pricing, CLI vs extension, Dispatch, screenshot placeholder

- [ ] **Step 1: Add Section 2 to index.html**

After `<!-- END РАЗДЕЛ 1 -->`, insert:

```html
<!-- ============================================================ -->
<!-- РАЗДЕЛ 2 — Продукты Claude Code (5 slides) -->
<!-- ============================================================ -->
<section>

  <!-- 2.0 Экосистема Claude -->
  <section data-transition="fade">
    <h2>Экосистема Claude</h2>
    <div class="grid-2x2">
      <div class="grid-item fragment">
        <strong>Claude Chat</strong>
        <span>Разговорный интерфейс для всего</span>
      </div>
      <div class="grid-item fragment">
        <strong>Claude Design</strong>
        <span>Прототипирование и UI</span>
      </div>
      <div class="grid-item fragment">
        <strong>Claude Cowork</strong>
        <span>Совместная работа над документами</span>
      </div>
      <div class="grid-item accent-item fragment">
        <strong>Claude Code</strong>
        <span>Разработка прямо в вашем проекте</span>
      </div>
    </div>
    <aside class="notes">Четыре продукта под одним брендом. Сегодня фокус на Claude Code — то, что живёт в терминале и видит ваш код.</aside>
  </section>

  <!-- 2.1 Планы и цены -->
  <section data-transition="slide">
    <h2>Планы и цены</h2>
    <img src="assets/claude_plans.png" alt="Claude Pro vs Max plans" style="max-height: 38vh;">
    <div class="two-col" style="margin-top: 1rem; font-size: 0.75em;">
      <div class="fragment">
        <strong>Pro</strong> — $17/мес (ежегодно) / ~$20 помесячно<br>
        <span style="color:#aaa;">Claude Code, Cowork, Design, больше моделей, память</span>
      </div>
      <div class="fragment">
        <strong>Max</strong> — от $100/мес<br>
        <span style="color:#aaa;">до 20&times; токенов, рекомендован для Code, приоритетный доступ</span>
      </div>
    </div>
    <p class="accent fragment" style="margin-top: 1rem; font-size: 0.9em; font-weight: 700;">
      Лайфхак: Pro можно делить на двоих &rarr; ~$10/мес с человека
    </p>
    <p class="fragment meta">Минус: лимит токенов — общий. Следите за расходом.</p>
    <aside class="notes">На скриншоте: пользователь на месячном биллинге (~$20/мес), ниже — Max от $100. VAT 21% добавляется на чекаут (Нидерланды). Лайфхак с делёжкой — один аккаунт, два разработчика, токены пополам. Работает, пока не упрётесь в лимит.</aside>
  </section>

  <!-- 2.2 CLI vs Extension -->
  <section data-transition="slide">
    <h2>Claude Code: CLI vs расширение</h2>
    <div class="two-col" style="justify-content: center; margin-top: 2rem;">
      <div class="card fragment" style="text-align: center;">
        <strong>Terminal</strong>
        <code>claude</code>
        <span style="font-size: 0.8em; color: #aaa;">Работает везде</span>
      </div>
      <div style="display: flex; align-items: center; font-size: 1.5em; color: #7C6FF7; font-weight: 700; flex: 0;">или</div>
      <div class="card fragment" style="text-align: center;">
        <strong>VS Code</strong>
        <code>Extension</code>
        <span style="font-size: 0.8em; color: #aaa;">Интеграция с IDE</span>
      </div>
    </div>
    <br>
    <p class="accent big-quote fragment">&laquo;Разницы нет — выбирай по удобству&raquo;</p>
    <aside class="notes">Один и тот же Claude Code, одни скиллы, одни возможности. Лично использую CLI + VS Code как редактор.</aside>
  </section>

  <!-- 2.3 Dispatch -->
  <section data-transition="slide">
    <h2>Dispatch</h2>
    <img src="assets/dispatch.png" alt="Dispatch mobile app">
    <ul>
      <li class="fragment">Мобильное приложение для управления Claude с телефона</li>
      <li class="fragment">&laquo;One conversation from anywhere&raquo;</li>
      <li class="fragment">Отошёл от компа — продолжил задачу с дивана</li>
    </ul>
    <aside class="notes">Dispatch «парует» телефон с Claude Code на компьютере. Смотришь прогресс, даёшь инструкции, проверяешь результаты. Удобно когда агент работает долго — не нужно сидеть у монитора. Покажи «Pair your phone» в UI.</aside>
  </section>

  <!-- 2.4 Скриншот Claude Code -->
  <section data-transition="slide">
    <h2>Claude Code в деле</h2>
    <p style="color: #555; font-style: italic; font-size: 0.8em;">[Официальный скриншот интерфейса — добавить перед докладом]</p>
    <ul>
      <li class="fragment">Терминальный интерфейс с полным контекстом проекта</li>
      <li class="fragment">Видит файлы, историю git, структуру кода</li>
      <li class="fragment">Работает прямо в вашем репозитории</li>
    </ul>
    <aside class="notes">Добавить официальный скриншот Claude Code перед докладом (раздел 7 спецификации — открытый вопрос). Показать ключевые элементы UI: промт, файловый контекст, вывод команд.</aside>
  </section>

</section>
<!-- END РАЗДЕЛ 2 -->
```

- [ ] **Step 2: Verify Section 2 in browser**

```powershell
npm start
```

Navigate to Section 2. Verify:
- `claude_plans.png` loads (no broken image icon)
- `dispatch.png` loads
- 2×2 grid cells appear as fragments on 2.0
- Pricing two-column layout renders side by side
- "Лайфхак" accent line appears after pricing details

Stop server: `Ctrl+C`

---

### Task 6: Sections 3 & 4 — Dev Flow Theory + Manual Problems (5 slides)

**Files:**
- Modify: `revealjs/index.html`

**Interfaces:**
- Consumes: `.flow-chain`, `.flow-step`, `.flow-arrow` CSS classes
- Produces: 2 slides (Раздел 3) + 3 slides (Раздел 4)

- [ ] **Step 1: Add Sections 3 & 4 to index.html**

After `<!-- END РАЗДЕЛ 2 -->`, insert:

```html
<!-- ============================================================ -->
<!-- РАЗДЕЛ 3 — Теоретический флоу разработки (2 slides) -->
<!-- ============================================================ -->
<section>

  <!-- 3.0 Схема флоу -->
  <section data-transition="fade">
    <h2>Флоу разработки</h2>
    <div class="flow-chain">
      <div class="flow-step fragment">Идея</div>
      <span class="flow-arrow fragment">&rarr;</span>
      <div class="flow-step fragment">Product Spec</div>
      <span class="flow-arrow fragment">&rarr;</span>
      <div class="flow-step fragment">Tech Spec</div>
      <span class="flow-arrow fragment">&rarr;</span>
      <div class="flow-step fragment">Задачи</div>
      <span class="flow-arrow fragment">&rarr;</span>
      <div class="flow-step fragment">Код</div>
      <span class="flow-arrow fragment">&rarr;</span>
      <div class="flow-step fragment">Тесты</div>
      <span class="flow-arrow fragment">&rarr;</span>
      <div class="flow-step fragment">Review</div>
      <span class="flow-arrow fragment">&rarr;</span>
      <div class="flow-step fragment">Commit</div>
      <span class="flow-arrow fragment">&rarr;</span>
      <div class="flow-step fragment">Прод</div>
    </div>
    <aside class="notes">Классический производственный цикл. Ничего нового — именно так делают продукты уже десятилетия. Важно это проговорить перед следующим слайдом.</aside>
  </section>

  <!-- 3.1 Инсайт -->
  <section data-transition="slide">
    <p class="big-quote">Это не изобретение — это классика.</p>
    <br>
    <p class="accent big-quote fragment">Просто теперь большую часть этого делает AI.</p>
    <aside class="notes">Ключевой инсайт доклада: вайбкодинг не изобрёл новый процесс, он ускорил старый. AI берёт на себя рутину, а не придумывает процесс за тебя.</aside>
  </section>

</section>
<!-- END РАЗДЕЛ 3 -->

<!-- ============================================================ -->
<!-- РАЗДЕЛ 4 — Проблемы ручной работы с Claude Code (3 slides) -->
<!-- ============================================================ -->
<section>

  <!-- 4.0 Проблема 1: промты -->
  <section data-transition="fade">
    <h2>Проблема 1: ручные промты</h2>
    <div class="two-col" style="margin-top: 1.5rem; font-size: 0.8em;">
      <div class="fragment">
        <p style="color: #e05050; margin-bottom: 0.5em;"><strong>Было</strong></p>
        <p>Каждый раз пишешь промт вручную</p>
        <p>&darr;</p>
        <p>Тратишь время на формулировки</p>
        <p>&darr;</p>
        <p>Промты разные — результат непредсказуем</p>
      </div>
      <div class="fragment">
        <p style="color: #50c878; margin-bottom: 0.5em;"><strong>Должно быть</strong></p>
        <p>Стандартизированная инструкция</p>
        <p>&darr;</p>
        <p>Один раз написал — используешь всегда</p>
        <p>&darr;</p>
        <p>Предсказуемый, повторяемый результат</p>
      </div>
    </div>
    <aside class="notes">Классическая боль. Разработчик пишет разные варианты промтов для одной и той же задачи — качество гуляет, время тратится на переформулировки.</aside>
  </section>

  <!-- 4.1 Проблема 2: security-review -->
  <section data-transition="slide">
    <h2>Проблема 2: security-review</h2>
    <ul>
      <li class="fragment">Написал промт для ревью кода &rarr; сохранил где-то</li>
      <li class="fragment">Забыл обновить &rarr; новые уязвимости не проверяются</li>
      <li class="fragment">Промт для security стареет быстрее, чем его обновляешь</li>
    </ul>
    <br>
    <p class="accent fragment">Технологии меняются, промт — нет.</p>
    <aside class="notes">Это реальная проблема: OWASP обновляет список уязвимостей, появляются новые паттерны атак, а ваш промт из 2023 года об этом не знает. Промт нужно поддерживать как код.</aside>
  </section>

  <!-- 4.2 Вывод -->
  <section data-transition="slide">
    <h2 style="font-size: 2.5em;">Нужна система.</h2>
    <br>
    <p class="fragment" style="font-size: 1.2em;">
      &darr;
    </p>
    <p class="accent big-quote fragment">Решение: Skills</p>
    <aside class="notes">Переходим к главной теме доклада. Скиллы — это система, которая решает обе проблемы.</aside>
  </section>

</section>
<!-- END РАЗДЕЛ 4 -->
```

- [ ] **Step 2: Verify Sections 3 & 4 in browser**

```powershell
npm start
```

Navigate to Sections 3 and 4. Verify:
- Flow chain steps appear one by one with arrows between them
- Two-column "Было / Должно быть" layout side by side
- "Нужна система." renders as large heading
- "Решение: Skills" appears in accent color as fragment

Stop server: `Ctrl+C`

---

### Task 7: Sections 5 & 6 — What Are Skills + Interesting Skills (5 slides)

**Files:**
- Modify: `revealjs/index.html`

**Interfaces:**
- Consumes: `.skill-name`, `.accent`, table CSS
- Produces: 2 slides (Раздел 5) + 3 slides (Раздел 6)

- [ ] **Step 1: Add Sections 5 & 6 to index.html**

After `<!-- END РАЗДЕЛ 4 -->`, insert:

```html
<!-- ============================================================ -->
<!-- РАЗДЕЛ 5 — Что такое скиллы (2 slides) -->
<!-- ============================================================ -->
<section>

  <!-- 5.0 Определение -->
  <section data-transition="fade">
    <h2>Скилл — это что?</h2>
    <br>
    <p class="fragment">Markdown-файл с инструкцией для нейронки.</p>
    <br>
    <p class="accent big-quote fragment">Один раз написал — используешь в любом проекте.</p>
    <br>
    <div class="fragment" style="font-size: 0.8em; color: #aaa; display: flex; gap: 2rem; justify-content: center;">
      <span>skill.md &rarr;</span>
      <span>Claude Code читает &rarr;</span>
      <span>применяет к задаче</span>
    </div>
    <aside class="notes">Метафора: skill = плагин/инструкция. Нейронка — умная, но без контекста она не знает ваш процесс. Скилл даёт ей этот контекст один раз и навсегда.</aside>
  </section>

  <!-- 5.1 Как работают -->
  <section data-transition="slide">
    <h2>Как вызвать скилл</h2>
    <br>
    <div style="font-size: 0.95em;">
      <p class="fragment"><code class="skill-name">/brainstorming</code> — генерация идей и требований</p>
      <p class="fragment"><code class="skill-name">/code-review</code> — ревью кода</p>
      <p class="fragment"><code class="skill-name">/security-review</code> — аудит безопасности</p>
      <p class="fragment"><code class="skill-name">/writing-plans</code> — план реализации</p>
    </div>
    <br>
    <p class="fragment meta">Claude Code видит вызов, находит файл скилла, применяет инструкцию.</p>
    <aside class="notes">Вызов скилла — это не магия. Claude видит /название, ищет skill-файл в .claude/skills/, читает его и следует инструкции. Скилл — это просто умный промт, который живёт в файловой системе.</aside>
  </section>

</section>
<!-- END РАЗДЕЛ 5 -->

<!-- ============================================================ -->
<!-- РАЗДЕЛ 6 — Интересные скиллы для разработчика (3 slides) -->
<!-- ============================================================ -->
<section>

  <!-- 6.0 Таблица скиллов -->
  <section data-transition="fade">
    <h2>Интересные скиллы</h2>
    <table>
      <thead>
        <tr><th>Скилл</th><th>Назначение</th></tr>
      </thead>
      <tbody>
        <tr><td><code>gstack</code></td><td>Продуктовая разработка</td></tr>
        <tr><td><code>superpowers</code></td><td>Технический флоу (полный цикл)</td></tr>
        <tr><td><code>oh-my-claudecode</code></td><td>Аналог superpowers</td></tr>
        <tr><td><code>llm-sast-scanner</code></td><td>Аудит безопасности кода</td></tr>
        <tr><td><code>ponytail</code></td><td>Проверяет: нужно ли изобретать велосипед?</td></tr>
      </tbody>
    </table>
    <aside class="notes">Это не исчерпывающий список. Экосистема растёт. Смотрите на GitHub и в Telegram-каналах.</aside>
  </section>

  <!-- 6.1 Детали: superpowers -->
  <section data-transition="slide">
    <h2><code>superpowers</code></h2>
    <p style="font-size: 0.8em; color: #aaa; margin-bottom: 1rem;">Это не один скилл — это набор для полного цикла разработки</p>
    <ul>
      <li class="fragment"><code class="skill-name">/brainstorming</code> — исследование задачи</li>
      <li class="fragment"><code class="skill-name">/writing-plans</code> — план реализации</li>
      <li class="fragment"><code class="skill-name">/test-driven-development</code> — TDD</li>
      <li class="fragment"><code class="skill-name">/code-review</code> — ревью</li>
      <li class="fragment"><code class="skill-name">/security-review</code> — безопасность</li>
      <li class="fragment"><code class="skill-name">/systematic-debugging</code> — дебаггинг</li>
    </ul>
    <aside class="notes">superpowers — это то, что я использую ежедневно. Каждый скилл — отдельный файл, каждый вызывается отдельно. Можно установить всё, можно взять только нужные.</aside>
  </section>

  <!-- 6.2 Как установить -->
  <section data-transition="slide">
    <h2>Как установить скиллы</h2>
    <br>
    <div class="fragment" style="margin-bottom: 1.5rem;">
      <p style="color: #aaa; font-size: 0.8em; margin-bottom: 0.5em;">Способ 1: через Claude Code</p>
      <code style="font-size: 0.85em;">«Установи скилл superpowers»</code>
    </div>
    <div class="fragment">
      <p style="color: #aaa; font-size: 0.8em; margin-bottom: 0.5em;">Способ 2: через документацию</p>
      <p style="font-size: 0.8em;">GitHub README &rarr; команды установки для каждой нейронки</p>
    </div>
    <aside class="notes">Большинство скиллов имеют README с командами установки — отдельно для Claude Code, Gemini CLI и других. Можно просто попросить нейронку: «Найди и установи скилл X» — она справится.</aside>
  </section>

</section>
<!-- END РАЗДЕЛ 6 -->
```

- [ ] **Step 2: Verify Sections 5 & 6 in browser**

```powershell
npm start
```

Navigate to Sections 5 & 6. Verify:
- Skill names render in `JetBrains Mono` with purple color
- Table in 6.0 appears all at once (not as fragments)
- Bullet list in 6.1 appears fragment by fragment
- Layout is readable at presentation font size

Stop server: `Ctrl+C`

---

### Task 8: Sections 7 & 8 — My Stack + My Flow (3 slides)

**Files:**
- Modify: `revealjs/index.html`

**Interfaces:**
- Consumes: `assets/brainstorming.png`, `assets/writing_plans.png`, `.accent`, `.big-quote`
- Produces: 1 slide (Раздел 7) + 2 slides (Раздел 8)

- [ ] **Step 1: Add Sections 7 & 8 to index.html**

After `<!-- END РАЗДЕЛ 6 -->`, insert:

```html
<!-- ============================================================ -->
<!-- РАЗДЕЛ 7 — Мой стек (1 slide) -->
<!-- ============================================================ -->
<section>

  <!-- 7.0 Стек -->
  <section data-transition="fade">
    <h2>Мой стек</h2>
    <br>
    <div style="display: flex; gap: 2rem; justify-content: center; align-items: center; font-size: 1.1em;">
      <div class="card accent-card fragment" style="font-size: 1.1em; padding: 1.5rem 2rem;">
        <strong>VS Code</strong>
      </div>
      <span class="accent" style="font-size: 1.5em;">+</span>
      <div class="card accent-card fragment" style="font-size: 1.1em; padding: 1.5rem 2rem;">
        <strong>CLI</strong>
      </div>
      <span class="accent" style="font-size: 1.5em;">+</span>
      <div class="card accent-card fragment" style="font-size: 1.1em; padding: 1.5rem 2rem;">
        <strong>superpowers</strong>
      </div>
    </div>
    <br>
    <p class="accent big-quote fragment">&laquo;Просто. Работает. Достаточно.&raquo;</p>
    <aside class="notes">Не нужно ничего лишнего. VS Code как редактор, Claude Code CLI как AI, superpowers как набор скиллов. Три инструмента — полный цикл.</aside>
  </section>

</section>
<!-- END РАЗДЕЛ 7 -->

<!-- ============================================================ -->
<!-- РАЗДЕЛ 8 — Мой флоу (2 slides) -->
<!-- ============================================================ -->
<section>

  <!-- 8.0 Флоу шагами -->
  <section data-transition="fade">
    <h2>Мой флоу</h2>
    <div class="two-col" style="align-items: flex-start;">
      <div>
        <p class="fragment"><code class="skill-name">/brainstorming</code></p>
        <p class="fragment" style="font-size: 0.75em; color: #aaa; margin: 0 0 0.8rem 1rem;">Диалог &rarr; требования &rarr; спека</p>
        <p class="fragment"><code class="skill-name">/writing-plans</code></p>
        <p class="fragment" style="font-size: 0.75em; color: #aaa; margin: 0 0 0.8rem 1rem;">Спека &rarr; план реализации</p>
        <p class="fragment"><strong>Реализация по плану</strong></p>
        <p class="fragment" style="font-size: 0.75em; color: #aaa; margin: 0 0 0.8rem 1rem;">Агент выполняет задачи по очереди</p>
        <p class="accent fragment"><strong>Очищай контекст между этапами</strong></p>
      </div>
      <div class="fragment">
        <img src="assets/brainstorming.png" alt="Brainstorming session" style="max-height: 38vh;">
      </div>
    </div>
    <aside class="notes">Ключевой момент — очистка контекста. Новая сессия = чистый фокус на текущей задаче. Нейронка не путается в деталях предыдущих этапов. Показать скриншот — это живой brainstorming в деле.</aside>
  </section>

  <!-- 8.1 Почему очистка контекста важна -->
  <section data-transition="slide">
    <h2>Зачем очищать контекст?</h2>
    <ul>
      <li class="fragment">Нейронка не путается в старых деталях</li>
      <li class="fragment">Каждый этап начинается с нужным контекстом, не с лишним</li>
      <li class="fragment">Экономия токенов</li>
    </ul>
    <br>
    <p class="accent big-quote fragment">Новая сессия = чистый фокус.</p>
    <aside class="notes">Большой контекст — это не всегда хорошо. Нейронка начинает «отвлекаться» на старые детали, делать выводы из устаревших данных. Очищение контекста — это гигиена разработки.</aside>
  </section>

</section>
<!-- END РАЗДЕЛ 8 -->
```

- [ ] **Step 2: Verify Sections 7 & 8 in browser**

```powershell
npm start
```

Navigate to Sections 7 & 8. Verify:
- Three accent cards in a row on Раздел 7
- Two-column layout on 8.0: flow steps left, screenshot right
- `brainstorming.png` loads without broken image
- "Очищай контекст" appears in accent color

Stop server: `Ctrl+C`

---

### Task 9: Section 9 — Features (7 slides, including MCP)

**Files:**
- Modify: `revealjs/index.html`

**Interfaces:**
- Consumes: `.fan-diagram`, `.fan-main`, `.fan-node`, `.fan-center`, `.fan-branches`, `.fan-arrow-col`; `assets/writing_plans.png`
- Produces: 7 slides: Project Memory, Model Management, SDD+TDD, Parallel Agents, 12 Lectures Example, MCP Servers, Context7

- [ ] **Step 1: Add Section 9 to index.html**

After `<!-- END РАЗДЕЛ 8 -->`, insert:

```html
<!-- ============================================================ -->
<!-- РАЗДЕЛ 9 — Фишки (7 slides) -->
<!-- ============================================================ -->
<section>

  <!-- 9.0 Память проекта -->
  <section data-transition="fade">
    <h2>Память проекта</h2>
    <ul>
      <li class="fragment">Файл на диске: <code>CLAUDE.md</code> / <code>memory/*.md</code></li>
      <li class="fragment">Сохраняется между сессиями — нейронка помнит контекст проекта</li>
      <li class="fragment">Пишешь один раз: стек, правила, паттерны</li>
      <li class="fragment">Каждый новый разговор начинается с полным контекстом</li>
    </ul>
    <br>
    <p class="accent fragment">&laquo;Не объясняй нейронке одно и то же дважды&raquo;</p>
    <aside class="notes">CLAUDE.md — главный файл контекста. memory/ — папка с отдельными файлами памяти (пользователь, проект, обратная связь). Claude Code читает их при каждом запуске.</aside>
  </section>

  <!-- 9.1 Управление моделями -->
  <section data-transition="slide">
    <h2>Управление моделями</h2>
    <div class="two-col" style="margin-top: 1.5rem;">
      <div class="card fragment">
        <strong>Haiku</strong>
        <span style="font-size: 0.8em; color: #aaa;">Рутинные задачи</span>
        <span style="font-size: 0.75em; color: #50c878;">Дёшево &amp; быстро</span>
      </div>
      <div class="card accent-card fragment">
        <strong>Opus / Sonnet</strong>
        <span style="font-size: 0.8em; color: #aaa;">Сложные задачи</span>
        <span style="font-size: 0.75em; color: #e0a050;">Мощно &amp; дороже</span>
      </div>
    </div>
    <br>
    <p class="fragment meta">Автоматическое переключение через настройки скиллов</p>
    <p class="accent fragment">Не трать Opus на форматирование README</p>
    <aside class="notes">Умное использование моделей — это экономия. Haiku отлично справляется с простыми задачами: переименование файлов, форматирование, простые рефакторинги. Opus держи для архитектурных решений и сложных алгоритмов.</aside>
  </section>

  <!-- 9.2 SDD + TDD -->
  <section data-transition="slide">
    <h2>SDD + TDD</h2>
    <ul>
      <li class="fragment">1 задача = 1 агент</li>
      <li class="fragment">Задача закрывается когда тесты зелёные</li>
      <li class="fragment">Авто-ревью после завершения</li>
    </ul>
    <br>
    <p class="accent big-quote fragment">Предсказуемое качество без ручного контроля каждого шага.</p>
    <aside class="notes">SDD — субагент-driven development. Каждый агент решает одну задачу, результат проверяется тестами. Это убирает «а AI сделал что-то не то» — у него чёткий критерий успеха.</aside>
  </section>

  <!-- 9.3 Параллельные агенты -->
  <section data-transition="slide">
    <h2>Параллельные агенты</h2>
    <p class="fragment"><code class="skill-name">/dispatching-parallel-agents</code></p>
    <br>
    <div class="fan-diagram fragment">
      <div class="fan-center">
        <div class="fan-main">Главный агент</div>
      </div>
      <div class="fan-arrow-col">&darr;&darr;</div>
      <div class="fan-branches">
        <div class="fan-node">Агент 1</div>
        <div class="fan-node">Агент 2</div>
        <div class="fan-node">Агент 3</div>
        <div class="fan-node">Агент N</div>
      </div>
      <div class="fan-arrow-col">&darr;&darr;</div>
      <div class="fan-center">
        <div class="fan-main">Сборка результатов</div>
      </div>
    </div>
    <p class="fragment meta">Агенты работают одновременно &rarr; скорость &times;N</p>
    <aside class="notes">Классический fan-out / fan-in паттерн. Главный агент раздаёт задачи, параллельные агенты выполняют независимо, главный собирает результат. Работает особенно хорошо для задач без зависимостей между ними.</aside>
  </section>

  <!-- 9.4 Пример: шпаргалка по 12 лекциям -->
  <section data-transition="slide">
    <h2>Пример: шпаргалка по 12 лекциям</h2>
    <ul>
      <li class="fragment">Задача: выписать ключевые знания из 12 лекций</li>
      <li class="fragment">12 агентов запущены параллельно</li>
      <li class="fragment">Каждый обрабатывает одну лекцию &rarr; записывает в файл</li>
      <li class="fragment">Главный агент собирает все файлы в один</li>
    </ul>
    <br>
    <div class="fragment fan-diagram" style="font-size: 0.7em;">
      <div class="fan-center">
        <div class="fan-main">Главный агент</div>
      </div>
      <div class="fan-arrow-col">&darr;&darr;</div>
      <div class="fan-branches">
        <div class="fan-node">Лекция 1 &rarr; файл</div>
        <div class="fan-node">Лекция 2 &rarr; файл</div>
        <div class="fan-node">&#8942;</div>
        <div class="fan-node">Лекция 12 &rarr; файл</div>
      </div>
      <div class="fan-arrow-col">&darr;&darr;</div>
      <div class="fan-center">
        <div class="fan-main">Итоговая шпаргалка</div>
      </div>
    </div>
    <aside class="notes">Реальный кейс. Без параллелизма: 12 лекций × ~3 мин = ~36 мин последовательно. С параллельными агентами: ~3-4 минуты суммарно. Привести реальное время.</aside>
  </section>

  <!-- 9.5 MCP серверы: что это -->
  <section data-transition="slide">
    <h2>MCP серверы</h2>
    <p style="font-size: 0.75em; color: #aaa; margin-bottom: 1rem;">Model Context Protocol</p>
    <ul>
      <li class="fragment">Стандарт для подключения внешних инструментов к AI</li>
      <li class="fragment">Claude &rarr; MCP-сервер &rarr; внешний источник (база, API, документация)</li>
      <li class="fragment">Одна строчка в настройках Claude Code — новый инструмент готов</li>
    </ul>
    <br>
    <p class="accent big-quote fragment">Ты расширяешь мозг нейронки подключаемыми источниками данных.</p>
    <aside class="notes">Без MCP нейронка знает только то, что в тренировочных данных — устаревшее, ограниченное. С MCP она может запросить актуальные данные в реальном времени. Это принципиальная разница в возможностях.</aside>
  </section>

  <!-- 9.6 Context7: MCP для документации -->
  <section data-transition="slide">
    <h2>Context7</h2>
    <p style="font-size: 0.75em; color: #aaa; margin-bottom: 1rem;">MCP-сервер для актуальной документации</p>
    <ul>
      <li class="fragment">Claude пишет код &rarr; Context7 подтягивает доку текущей версии библиотеки</li>
      <li class="fragment">Без него: устаревшие API из обучающей выборки &rarr; deprecated-код</li>
      <li class="fragment">С ним: «Напиши запрос на Prisma» &rarr; доку текущей версии &rarr; правильный код</li>
    </ul>
    <br>
    <p class="accent big-quote fragment">Никаких галлюцинаций из-за устаревших знаний.</p>
    <p class="fragment meta">Бесплатный &bull; одна команда установки &bull; тысячи популярных библиотек</p>
    <aside class="notes">Context7 — один из лучших MCP-серверов для разработчиков. Решает конкретную боль: нейронка обучалась на данных с отсечкой, а библиотеки выпускают новые версии каждые недели. Context7 закрывает этот разрыв.</aside>
  </section>

</section>
<!-- END РАЗДЕЛ 9 -->
```

- [ ] **Step 2: Verify Section 9 in browser**

```powershell
npm start
```

Navigate to Section 9. Verify:
- Fan-out diagram on 9.3 renders with "Главный агент" center boxes and branch nodes
- All 7 slides accessible via down arrow
- MCP slides (9.5 & 9.6) render cleanly
- "Никаких галлюцинаций" accent quote appears as fragment

Stop server: `Ctrl+C`

---

### Task 10: Sections 10 & 11 — Where to Grow + Resources + Final (5 slides)

**Files:**
- Modify: `revealjs/index.html`

**Interfaces:**
- Consumes: `assets/paperclip_2.png`, `assets/my_qr.png`, table CSS
- Produces: 3 slides (Раздел 10) + 2 slides (Раздел 11). Completes the presentation.

- [ ] **Step 1: Add Sections 10 & 11 to index.html**

After `<!-- END РАЗДЕЛ 9 -->`, insert:

```html
<!-- ============================================================ -->
<!-- РАЗДЕЛ 10 — Куда расти (3 slides) -->
<!-- ============================================================ -->
<section>

  <!-- 10.0 gbrain -->
  <section data-transition="fade">
    <h2>gbrain</h2>
    <p style="font-size: 0.8em; color: #aaa;">Проект <strong>@maxson_dev</strong></p>
    <ul>
      <li class="fragment">Проблема: много проектов — каждый раз объяснять AI контекст компании лень</li>
      <li class="fragment">Решение: MCP-сервер + pgvector + эмбеддинги = база знаний компании</li>
      <li class="fragment">Задал вопрос AI &rarr; AI спросил gbrain &rarr; полный ответ за минимум токенов</li>
      <li class="fragment">CI/CD: изменения в проекте &rarr; автоматически попадают в базу знаний</li>
    </ul>
    <aside class="notes">Пост с деталями: https://t.me/maxson_dev/21 — показать аудитории. gbrain индексирует базу через pgvector, выставляет авторизованную ручку наружу. Каждый сотрудник подключает MCP — и AI любого из них знает контекст компании. Произошли изменения → ci/cd → база обновилась автоматически.</aside>
  </section>

  <!-- 10.1 paperclip / hermes -->
  <section data-transition="slide">
    <h2>paperclip / hermes</h2>
    <p style="font-size: 0.8em; color: #aaa;">Бот от <strong>@danokhlopkov</strong></p>
    <div class="two-col" style="align-items: flex-start; margin-top: 1rem;">
      <div>
        <p class="fragment">Автоматически постит контент в Telegram</p>
        <p class="fragment" style="font-size: 0.8em; color: #aaa; margin: 0.5rem 0;">контент &rarr; n8n &rarr; бот &rarr; канал</p>
        <br>
        <p class="fragment" style="font-size: 0.75em;">Оркестр агентов:</p>
        <ul style="font-size: 0.7em;">
          <li class="fragment">PAPERCLIP Orchestrator (CEO)</li>
          <li class="fragment">CTO &rarr; Staff Eng / Release Eng / QA</li>
          <li class="fragment">ANALYST (cron 6AM UTC)</li>
          <li class="fragment">COMMS MNGR</li>
        </ul>
      </div>
      <div class="fragment">
        <img src="assets/paperclip_2.png" alt="PAPERCLIP architecture" style="max-height: 40vh;">
      </div>
    </div>
    <aside class="notes">Видео-разбор: https://youtu.be/E3P0a03mN8A?si=TV-k3gnokuOh6CPq — рекомендую показать ссылку. Дополнительные скриншоты: paperclip_1, 3, 4 — можно показать по запросу аудитории. Это живой пример production-grade мульти-агентной системы.</aside>
  </section>

  <!-- 10.2 Вывод -->
  <section data-transition="slide">
    <p class="big-quote">Экосистема растёт каждую неделю.</p>
    <br>
    <p class="accent big-quote fragment">Следи за комьюнити — там появляются новые инструменты.</p>
    <aside class="notes">Перед тем как перейти к ресурсам — подготовить аудиторию: то, что вы увидели сегодня — это снимок на момент доклада. Через месяц будет лучше.</aside>
  </section>

</section>
<!-- END РАЗДЕЛ 10 -->

<!-- ============================================================ -->
<!-- РАЗДЕЛ 11 — Ресурсы (2 slides) -->
<!-- ============================================================ -->
<section>

  <!-- 11.0 Telegram-каналы -->
  <section data-transition="fade">
    <h2>Telegram-каналы</h2>
    <table>
      <thead>
        <tr><th>Канал</th><th>О чём</th></tr>
      </thead>
      <tbody>
        <tr><td><code>@vibecoding_tg</code></td><td>Скиллы и лайфхаки для вайбкодинга</td></tr>
        <tr><td><code>@seeallochnaya</code></td><td>Научный взгляд на AI</td></tr>
        <tr><td><code>@cryptoEssay</code></td><td>Новости AI</td></tr>
        <tr><td><code>@makebugger</code></td><td>AI со стороны стартапов и бизнеса</td></tr>
        <tr><td><code>@danokhlopkov</code></td><td>Вайбкодер: стартапы</td></tr>
        <tr><td><code>@maxson_dev</code></td><td>Вайбкодер: бэкенд</td></tr>
        <tr><td><code>@artem_designich</code></td><td>Вайбкодер: дизайн и фронтенд</td></tr>
        <tr><td><code>@a168boba</code></td><td>Философия + практика вайбкодинга</td></tr>
      </tbody>
    </table>
    <aside class="notes">Эти каналы — отправная точка. Там регулярно появляются новые скиллы, кейсы, разборы инструментов.</aside>
  </section>

  <!-- 11.1 Финал -->
  <section data-transition="slide">
    <h1 class="accent">Вопросы?</h1>
    <br>
    <img src="assets/my_qr.png" alt="QR code @LEBOWSSKII_DEV" style="max-height: 35vh; border-radius: 12px;">
    <p class="meta" style="font-size: 0.9em; margin-top: 0.5rem;">@LEBOWSSKII_DEV</p>
    <aside class="notes">QR-код ведёт на Telegram @LEBOWSSKII_DEV. Оставайтесь на связь — пишите вопросы, делитесь опытом.</aside>
  </section>

</section>
<!-- END РАЗДЕЛ 11 -->
```

- [ ] **Step 2: Verify full presentation end-to-end**

```powershell
npm start
```

Open `http://localhost:8000`. Press `End` key (or navigate manually) to jump to last slide. Verify:
- `my_qr.png` loads (no broken image)
- `paperclip_2.png` loads in two-column layout
- Telegram table renders with all 8 rows
- Final slide shows "Вопросы?" in accent color with QR code

Navigate back through all sections (Right arrow for sections, Down for sub-slides). Full walkthrough checkpoint:
- Section 0: 3 slides ✓
- Section 1: 6 slides ✓
- Section 2: 5 slides ✓
- Section 3: 2 slides ✓
- Section 4: 3 slides ✓
- Section 5: 2 slides ✓
- Section 6: 3 slides ✓
- Section 7: 1 slide ✓
- Section 8: 2 slides ✓
- Section 9: 7 slides ✓
- Section 10: 3 slides ✓
- Section 11: 2 slides ✓

Total: 39 slides ✓

Stop server: `Ctrl+C`

---

### Task 11: Final Polish & Speaker Notes Verification

**Files:**
- Modify: `revealjs/index.html` — update TOC in slide 0.3 if needed; fix any visual issues found

**Interfaces:**
- Produces: presentation-ready `index.html`, verified fragments, verified speaker notes

- [ ] **Step 1: Verify speaker notes on all section openers**

```powershell
npm start
```

Press `S` to open speaker notes window. Navigate through all 12 section opener slides (0.1, 1.0, 2.0, 3.0, 4.0, 5.0, 6.0, 7.0, 8.0, 9.0, 10.0, 11.0). Confirm each has non-empty notes.

- [ ] **Step 2: Test fragment behavior**

On slides with `class="fragment"` items, press Space bar. Confirm each item appears one at a time. Confirm tables (6.0, 11.0) appear all at once (no fragments on rows).

- [ ] **Step 3: Test keyboard shortcuts**

| Key | Expected behavior |
|-----|-------------------|
| `→` or `Space` | Next slide / next fragment |
| `↓` | Next slide within section |
| `↑` | Previous slide within section |
| `S` | Open speaker notes window |
| `F` | Fullscreen |
| `Esc` | Overview mode |
| `B` | Blackout screen |

All shortcuts should work as expected.

- [ ] **Step 4: Verify progress bar**

Confirm the progress bar at the bottom is visible and shows purple/accent color (`#7C6FF7`).

- [ ] **Step 5: Add official Claude Code screenshot when available**

When the official screenshot is obtained, add it to `assets/` and update slide 2.4:

Find this placeholder in `index.html`:
```html
<p style="color: #555; font-style: italic; font-size: 0.8em;">[Официальный скриншот интерфейса — добавить перед докладом]</p>
```

Replace with:
```html
<img src="assets/claude_screenshot.png" alt="Claude Code interface">
```

- [ ] **Step 6: Final font check**

Open browser DevTools → Network tab → reload page.
Confirm Google Fonts requests succeed (200 status) for:
- `Inter` (wght 400, 700)
- `JetBrains Mono` (wght 400)

If offline/no internet: download fonts locally or use system font fallbacks in `css/custom.css`:
```css
/* Offline fallback — add if Google Fonts unavailable */
:root {
  --r-heading-font: 'Inter', system-ui, sans-serif;
  --r-main-font: 'Inter', system-ui, sans-serif;
  --r-code-font: 'JetBrains Mono', 'Courier New', monospace;
}
```

---

## Self-Review vs Spec

Comparing this plan against `docs/superpowers/specs/2026-06-21-vibecoding-presentation-design.md`:

| Spec Requirement | Task |
|---|---|
| Dark theme `#0f1117` / `#f0f0f0` / `#7C6FF7` | Task 2 (custom.css) |
| Inter + JetBrains Mono fonts | Task 2 |
| Fragments on all bullet points | Tasks 3–10 (all `class="fragment"`) |
| Tables without fragments | Tasks 7, 10 (table rows have no fragment class) |
| `fade` between sections, `slide` within | Tasks 3–10 (`data-transition` on each section) |
| Progress bar enabled + accent color | Task 2 (CSS) + Task 3 (Reveal.initialize) |
| Speaker notes on every slide | Tasks 3–10 (`<aside class="notes">` on each `<section>`) |
| Flat `assets/` folder | Task 1 |
| Full Setup (clone + npm start) | Task 1 |
| Section 0: 3 slides | Task 3 |
| Section 1: 6 slides | Task 4 |
| Section 2: 5 slides (incl. 2.1 Plans) | Task 5 |
| Section 3: 2 slides | Task 6 |
| Section 4: 3 slides | Task 6 |
| Section 5: 2 slides | Task 7 |
| Section 6: 3 slides | Task 7 |
| Section 7: 1 slide | Task 8 |
| Section 8: 2 slides | Task 8 |
| Section 9: 7 slides (incl. 9.5 MCP, 9.6 Context7) | Task 9 |
| Section 10: 3 slides | Task 10 |
| Section 11: 2 slides (QR code) | Task 10 |
| claude_plans.png lайфхак "делить на двоих" | Task 5, slide 2.1 |
| Context7 MCP explanation | Task 9, slide 9.6 |
| `writing_plans.png` referenced | Task 8 (assets copied in Task 1) |

**No gaps found.**
