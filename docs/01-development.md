# Журнал разработки — 01-nexcent-landing

Журнал ведётся по этапам из docs/AGENTS.md §5. Записывается только уже
сделанный шаг — с полным описанием выполненного. Раздел появляется, когда
этап завершён.

## 1. Изучить макет

Макет изучен через Figma MCP (файл l9442HdlZ9xWUYbsxcLbuW).

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