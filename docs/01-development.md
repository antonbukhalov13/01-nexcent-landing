# Журнал разработки — 01-nexcent-landing

Журнал ведётся по этапам из docs/AGENTS.md §5. Записывается только уже
сделанный шаг — с полным описанием выполненного. Раздел появляется, когда
этап завершён.

## 1. Изучить макет

Макет изучен через Figma MCP (файл l9442HdlZ9xWUYbsxcLbuW).

Точный эталон для последующей сверки вёрстки — локальные экспорты
в `docs/reference-images/` (PNG scale 2, выгружены из Figma при исчерпании
лимита MCP): общий вид `full/landing-page.png`, все секции в `sections/`,
палитра/кнопки/типографика/тени/иконки/guide в `style-guide/`, узкая версия
в `mobile/mobile.png`. Значения (цвета, размеры, отступы, координаты) при
вёрстке определяется по этим кадрам.

### Источник

- Основной фрейм — Landing Page (5:573), desktop 1440×4376, одностраничный
  лендинг. Он является эталоном реализации.
- Фреймы Style Guide / превью существуют в файле, но эталоном служит Landing
  Page: макет проверялся по нему.

### Структура страницы (сверху вниз)

- header (логотип, навигация, кнопка Register);
- hero (заголовок, кнопка, иллюстрация);
- clients (логотипы компаний);
- community (заголовок + 3 карточки);
- unlock (текст + иллюстрация);
- achievements (статистика);
- calender (хронология);
- customers (отзыв);
- community updates (новости, 3 карточки);
- cta (призыв к действию);
- footer.

### Палитра

- Primary #28CB8B, Secondary #263238, Info #2194F3;
- шкала Primary: T1 #66BB69, T2 #81C784, T3 #A5D6A7, T4 #C8E6C9, T5 #E8F5E9;
- шкала Shade: S1 #43A046, S2 #388E3B, S3 #237D31, S4 #1B5E1F, S5 #103E13;
- действия: Warning #FBC02D, Error #E53835, Success #2E7D31;
- нейтральные: Black #263238, D_Grey #4D4D4D, Grey #717171, L_Grey #89939E,
  Grey_Blue #ABBED1, Silver #F5F7FA, White #FFFFFF.

### Типографика (Inter, локально в fonts/)

- Headline 1 Semi Bold 64/76;
- Headline 2 Semi Bold 36/44;
- Headline 3 Semi Bold 28/36;
- Headline 4 Semi Bold 20/28;
- Body 1 Regular/Medium 18/28;
- Body 2 Regular/Medium 16/24;
- Body 3 Regular/Medium 14/20;
- Body 4 Regular/Medium 12/16.

### Кнопки

- типы: Primary / Secondary / Tertiary;
- размеры: Normal 56px, Medium 48px, Small 32px (стандартные), иконка 40px;
  икон-кнопки 64/48/32;
- состояния: Default, Hover, Focus, Click, Loading, Disabled;
- варианты: без иконки, иконка слева/справа.

### Иконки

- сетка 24px и 16px; категории: Arrows & Directions, User Interface.

### Вывод анализа

Шрифт — Inter (набор весов: Regular, Medium, Semi Bold). Цвета, типографика,
кнопки и состояния элементов вынесены в Style Guide; конкретные значения при
вёрстке уточняются по Landing Page.

## 2. Декомпозировать макет

Макет разбит на логические блоки по странице Design (0:1), фрейм Landing Page
(5:573), 1440×4376. Узкая версия (~481px) существует отдельным фреймом в
Thumbnail — детально разбирается на этапе адаптива.

### Контейнерная сетка

- ширина страницы 1440px;
- контентная область 1152px, поля 144px слева и справа (Frame Guide);
- внутренний шаг между элементами — кратно 24px;
- верх, мидл, низ — scroll-поток, без перекрытий, кроме точек карусели.

### Дерево блоков → семантика HTML

- Header (высота 84): логотип + nav (6 пунктов, gap 50) + Login/Sign up;
- Hero (599): заголовок h1 + текст + кнопка Primary слева, иллюстрация справа;
- Clients (190): заголовок секции + строка из 7 логотипов (48×48, шаг 184);
- Community (416): заголовок + 3 карточки (298px, центральная поднята на 10px);
- Unlock (433) и Calender (433): паттерн «иллюстрация слева + текст/кнопка
  справа» (контент 601px на колонку);
- Achievements (288): заголовок слева + статистика 2×2 справа (иконка 48 +
  число + подпись);
- Customer's (390): фото 326×326 + цитата + 6 логотипов (шаг 89) + ссылка
  «Meet all customers» со стрелкой;
- Community Updates (506): заголовок + 3 карточки (368×366, gap 24);
- CTA (300): заголовок + кнопка Primary (внутри footer);
- Footer (628): CTA + 4 колонки (бренд + соцсети | ссылки ×2 | copyright).

### Выбор layout-техники

- Flexbox: header, hero (2 колонки), строка логотипов, колонки карточек,
  верхний ряд сниппетов;
- Grid: статистика Achievements (2×2, gap 30×40), колонки футера;
- Normal flow: вертикальный поток секций, текстовые блоки;
- абсолютное позиционирование — только там, где оно оправдано (точки
  карусели, сдвиг центральной карточки Community).

### Переиспользуемые блоки

- Кнопка: Primary / Secondary / Tertiary, размеры 56/48/40/32, состояния по
  Style Guide;
- заголовок секции (текст + подзаголовок);
- карточка-колонка (Community, Community Updates);
- паттерн «иллюстрация + текст + кнопка» — переиспользуется Unlock и Calender;
- строка логотипов — Clients и Customer's;
- stats-grid-ячейка Achievements.

### Тени (Effects)

5 уровней, цвет #ABBED1: 2px 60%, 4px 40%, 6px 30%, 8px 40%, 16px 30%.

### Контент и assets

- Изображения локально в img/ (в т.ч. фоновые section-картинки Hero, карточки
  Community Updates);
- иконки в img/icons/ (SVG, сетка 24px);
- шрифт Inter локально в fonts/ (@font-face);
- у заголовков на фоне цвета использовать переменные из :root.

### Решение по мобильной версии

Мобильная версия существует в макете отдельно; при её реализации — чистый
CSS-гамбургер без JavaScript, hamburger-меню и вертикальная схема секций
разбираются на этапе адаптива.

## 3. Подготовить assets

Все ассеты собраны локально в проекте, внешних CDN нет — сайт полностью
самодостаточен. Источник выгрузки — фрейм Landing Page (5:573) на странице
Design (0:1).

### Шрифты — fonts/

- `Inter-Regular.woff2`, `Inter-Medium.woff2`, `Inter-SemiBold.woff2` —
  скачаны в woff2 с официального релиза Inter (github.com/rsms/inter), формат
  woff2 выбран осознанно: современный сжатый веб-формат, поддерживается всеми
  целевыми браузерами.
- Подключение через `@font-face` на шаге базового CSS; веса соответствуют
  макету (Regular / Medium / Semi Bold), локальные шрифты для Type 1–4.

### Растровые изображения — img/

- `hero.png` — иллюстрация Hero, экспорт через Figma MCP с scale 2 (782×814);
- `unlock.png` (442×433), `calender.png` (442×434) — иллюстрации секций;
- `customer.jpg` (358×358) — фото клиента; в макете контейнер 326×326,
  экспорт захватил тень/рамку — при вёрстке размер задаётся CSS;
- `blog-1.png` … `blog-3.png` (368×286) — изображения карточек
  Community Updates;
- `favicon.png` (64×64) — иконка Nexcent, экспортирована как PNG и
  нормализована в квадрат 64×64: прозрачный холст, логотип вписан по центру
  без искажений.

### Векторные логотипы — img/logos/

- `logo.svg` — логотип шапки (иконка + слово Nexcent), экспорт целого узла
  Header (не Vector, чтобы не «съехала» центровка);
- `client-1.svg` … `client-7.svg` — логотипы компаний секции Clients
  (слева направо, 7 шт);
- `customer-1.svg` … `customer-6.svg` — логотипы партнёров в Customer's
  (6 шт).

### Иконки — img/icons/

- `icon-community-membership.svg`, `icon-community-associations.svg`,
  `icon-community-clubs.svg` — три карточки Community;
- `icon-achievement-members.svg`, `icon-achievement-clubs.svg`,
  `icon-achievement-bookings.svg`, `icon-achievement-payments.svg` —
  статистика Achievements;
- `icon-arrow-right.svg` — стрелка ссылок;
- `icon-social-instagram.svg`, `icon-social-dribbble.svg`,
  `icon-social-twitter.svg`, `icon-social-youtube.svg` — соцсети футера
  (переименованы из social-1..4 по порядку в макете).

### Проверка и коммит

Итоговая раскладка: `fonts/` + `img/` + `img/logos/` + `img/icons/`. Файлы
растровые экспортированы в PNG/JPG (как в макете), ничего лишнего в staging
не попало. Зафиксировано коммитом `chore: add fonts and images` (только
`fonts/` и `img/`).

## 4. Создать HTML-скелет

Скелет написан на чистом HTML без CSS — страница должна оставаться понятной
при отключённых стилях. Контент сверен с макетом Landing Page (5:573).

### Структура страницы

```
body
├── header        логотип + nav (Home, Service, Feature, Product,
│                 Testimonial, FAQ) + Login / Sign up
└── main
    ├── hero      h1 «Lessons and insights from 8 years» + Register
    │             + иллюстрация + точки карусели (3)
    ├── clients   h2 + 7 логотипов (client-1..7)
    ├── community h2 + 3 карточки (Membership / National / Clubs)
    ├── unlock    иллюстрация + h2 + текст + Learn More
    ├── achievements  h2 + сетка статистики 2×2
    ├── calender  иллюстрация + h2 + текст + Learn More
    ├── customers фото + blockquote-отзыв + 6 логотипов
    │             + «Meet all customers»
    ├── updates   h2 + 3 карточки блога (blog-1..3)
    └── cta       h2 + кнопка Get a Demo (белая стрелка 16×16)
footer            бренд + copyright + соцсети | Company ×5 | Support ×5
                  | форма подписки (email + кнопка-самолётик)
```

### Семантика и контент

- Секции оформлены через `<section>` с якорями: `#home`, `#service`,
  `#feature`, `#product`, `#testimonial`, `#faq` (пункты меню ведут на них);
- иерархия заголовков: один `h1` (hero), секции — `h2`, карточки — `h3`;
- карточки Community и блог — через `article` (содержимое повторяющихся
  блоков), отзыв — через `blockquote`;
- списки логотипов (`clients`, `customers`, соцсети, ссылки футера) — `ul`;
- навигация шапки и футера — `nav` с `aria-label`;
- точки карусели hero — кнопки с `role="tablist"`, `role="tab"` и
  `aria-selected` (первая активна, `.hero__dot--active`);
- изображения с `alt` (декоративные иконки — пустой `alt=""`) и
  `width`/`height` из макета (защита от CLS);
- форма подписки: `<label class="visually-hidden">` + `input[type=email]`
  с `placeholder="Your email address"` + кнопка-стрелка (самолётик);
- кнопка CTA Get a Demo содержит белую стрелку `icon-arrow-right-white.svg`
  (16×16, это отдельный SVG-файл, добавлен в img/icons/);
- дополнительные иконки: `icon-send.svg` (самолётик формы, белый под
  тёмный футер).
- контент-тексты взяты из макета (цитата Customer's, тексты Unlock/Calender,
  списки футера Company/Support уточнены по Figma).

### Особенности футера

- copyright из двух строк: `Copyright © 2020 Nexcent ltd.` + `All rights
  reserved`;
- Company: About us, Blog, Contact us, Pricing, Testimonials;
- Support: Help center, Terms of service, Legal, Privacy Policy, Status;
- социальные иконки белые — видимы после стилизации футера (тёмный фон).

### Коммит

Зафиксировано `feat: add html skeleton` (index.html, icon-send.svg,
icon-arrow-right-white.svg). Стилей пока нет: серый фон кнопки формы — это
браузерный UA-стиль, он уйдёт на этапе базового CSS.

## 5. Создать базовый CSS-фундамент

Написан `css/style.css` — общая основа проекта без layout и стилизации
конкретных секций (эти этапы идут дальше).

### Шрифты

- Три правила `@font-face` для Inter (400 Regular, 500 Medium, 600 Semi
  Bold) с локальными woff2 из `fonts/`, `font-display: swap` — текст виден
  до окончания загрузки шрифта.

### Переменные `:root`

- палитра: Primary, Secondary, Info; шкалы Primary T1–T5 и Shade S1–S5;
  действия Warning / Error / Success; нейтральные Black / D_Grey / Grey /
  L_Grey / Grey_Blue / Silver / White (значения из раздела 1);
- типографика Inter: заранее объявлены размеры и линейки h1–h4 и body 1–4
  (в px), веса 400/500/600;
- layout: `--container-width: 1152px`, `--container-gutter: 24px` (поля
  144px на 1440 задаются через центрирование контейнера);
- шкала отступов по сетке 8pt (`--space-1…16`);
- радиусы (`--radius-sm/md/lg/full`);
- тени `--shadow-1…5` (цвет #ABBED1, интерпретация «2px 60%» → сдвиг 1–8px,
  размытие 2–16px, прозрачность соответствует макету; при первой реальной
  стилизации значения будут сверены с Effects в Figma).

### Reset и база

- `box-sizing: border-box` для всех элементов;
- обнуление margin/padding, `list-style: none`;
- `img { display: block; max-width: 100%; height: auto }`;
- `a` — наследует цвет, без подчёркивания;
- `button, input { font: inherit; color: inherit }`, у `button`
  `appearance: none; background: none; border: none; cursor: pointer` —
  это убирает серый UA-фон кнопки формы и стандартный вид кнопок;
- `html { scroll-behavior: smooth }` с отключением для пользователей,
  предпочитающих уменьшение движения (`@media (prefers-reduced-motion)`).

### Контейнер и утилиты

- `.container` — `max-width: 1152px`, центрируется, `padding-inline: 24px`;
- `.visually-hidden` — скрытие видимого, но доступного элемента; кроме
  устаревшего `clip` добавлен современный `clip-path: inset(50%)`.

### Подключение

В `index.html` добавлен `link[rel=stylesheet]` →
`css/style.css`.

### Коммит

Зафиксировано `style: add base styles and variables` (css/style.css,
index.html).