# Справочник по химии

Статический сайт-справочник по химии с отрисовкой линейных и структурных формул.

**Сайт:** https://dzhem.github.io/chem-ref/
**Исходники:** https://github.com/Dzhem/chem-ref

- **Автор:** Dzhem
- **Начало разработки:** ноябрь 2026

## Что здесь есть

Справочный материал по химии в Markdown, собираемый в документационный сайт:

- линейные формулы веществ;
- уравнения химических реакций (например, качественная реакция на Fe²⁺);
- структурные формулы (например, куркумин) — в виде SVG.

## Стек

| Компонент | Роль | Ссылка |
|---|---|---|
| [GitHub Pages](https://pages.github.com/) | хостинг статического сайта | https://pages.github.com |
| [Jekyll](https://jekyllrb.com/) | генератор статического сайта | https://jekyllrb.com |
| [Just the Docs](https://github.com/just-the-docs/just-the-docs) | тема оформления документации | https://github.com/just-the-docs/just-the-docs |
| [CharChem](http://charchem.org) | отрисовка химических формул (JS + SVG) | http://charchem.org |

Тема подключается через `remote_theme` в `_config.yml` — на GitHub Pages плагин `jekyll-remote-theme` встроен.

## Структура проекта

```
.
├── _config.yml              # настройки сайта, тема, baseurl
├── _config.dev.yml          # локальные переопределения (не в git)
├── Gemfile / Gemfile.lock   # зависимости сборки
├── index.md                 # главная страница
├── _includes/
│   ├── head_custom.html     # подключение charchem.css и charchem2.js
│   └── footer_custom.html   # span.CharChemConfig.auto-compile
└── assets/
    ├── css/charchem.css     # локальная копия стилей CharChem
    └── js/charchem2.js      # локальная копия библиотеки CharChem
```

## Локальная сборка

Нужны Ruby 3.x, Bundler и Git.

```bash
bundle install
bundle exec jekyll serve --config _config.yml,_config.dev.yml
```

Сайт: http://localhost:4000/chem-ref/

Два конфига нужны потому, что `remote_theme` без гема `jekyll-remote-theme` локально не работает — `_config.dev.yml` подменяет его на `theme: just-the-docs` из установленного гема.

## Как вставлять формулы

Файлы CharChem подключены локально (`assets/js/`, `assets/css/`), а не с `http://charchem.org`, — иначе на HTTPS-сайте браузер заблокировал бы их как mixed content.

Формула — блок с классом `echem-formula`:

```html
<div class="echem-formula">H2SO4</div>

<div class="echem-formula">
  3K3[Fe(CN)6] + 3Fe^2+ -> 3KFe(ii)[Fe(iii)(CN)6]"|v" + 6K^+
</div>
```

Автокомпиляция включена через `<span class="CharChemConfig auto-compile"></span>` в `_includes/footer_custom.html` — это равноценно классу `echem-auto-compile` на `<body>`, но не требует переопределять layout темы.

Описание формул удобно готовить в тестовом стенде на [charchem.org](http://charchem.org) и вставлять готовый HTML-код.

## Авторство и лицензии

- **Текстовое содержание справочника:** Dzhem, ноябрь 2026 — по усмотрению автора сайта.
- **Техническая часть** (структура проекта, подключение темы и CharChem, сборка и публикация) создана с помощью **MultiTool** (GigaChat 3.5 MoA).
- **Just the Docs** — © Patrick Marsceill и участники проекта, MIT.
- **CharChem / easyChem** — © PeterWin (peterwin@yandex.ru), http://charchem.org. Исходный код: https://github.com/Peter-Win/charchem2.ts.
Автор указывает: система может быть использована бесплатно для целей науки и образования. При ином использовании условия уточняйте у автора.
