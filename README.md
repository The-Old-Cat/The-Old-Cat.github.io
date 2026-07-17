# Цифровой сад и мастерская

Личный блог, база знаний и заметки. Сайт статически генерируется с помощью [Hugo](https://gohugo.io/) и развёртывается через GitHub Pages.

- **URL**: [the-old-cat.github.io](https://the-old-cat.github.io) / [lab.artkov-info.ru](https://lab.artkov-info.ru)
- **Движок**: Hugo (требуется версия **Extended** для компиляции Sass/SCSS)
- **Тема**: [hugo-theme-stack](https://github.com/CaiJimmy/hugo-theme-stack)

## 🚀 Быстрый старт (локальная разработка)

Для корректной работы необходимо скачать не только код репозитория, но и файлы темы, которые подключены как git-сабмодуль.

1. Клонируй репозиторий:
   ```bash
   git clone https://github.com/The-Old-Cat/The-Old-Cat.github.io.git
   cd The-Old-Cat.github.io
   ```

2. Инициализируй и обнови сабмодули (скачает тему):
   ```bash
   git submodule update --init --recursive
   ```

3. Запусти локальный сервер с черновиками:
   ```bash
   hugo server -D
   ```
   Сайт будет доступен по адресу `http://localhost:1313`.

## 🛠 Установленные расширения

### Callouts (Admonitions)

На сайте используется модуль **[hugo-admonitions](https://github.com/KKKZOZ/hugo-admonitions)** — позволяет создавать красивые цветные информационные блоки, аналогично callouts в Obsidian.

#### Примеры использования:

```markdown
> [!note]
> Это обычная заметка.

> [!summary] Знания
> Список связанных заметок по теме.

> [!warning]
> Важное предупреждение!

> [!tip]+
> Это сворачиваемый callout (знак `+` делает его закрытым по умолчанию).
```

**Основные типы callouts:**
- `note`, `summary`, `info`, `tip`, `success`, `question`
- `warning`, `danger`, `caution`, `failure`, `bug`, `quote`

---

## 📂 Структура проекта

```text
├── config/             # Конфигурация Hugo (hugo.toml и др.)
├── content/            # Исходные тексты заметок и страниц (Markdown)
│   ├── post/           # Статьи блога
│   └── page/           # Статические страницы (About, Archive)
├── themes/             # Подмодуль с темой оформления (hugo-theme-stack)
└── .github/workflows/  # Скрипт автоматической сборки и деплоя на GitHub Pages
```

## 🛠 Требования к окружению

- **Git** (для управления сабмодулями)
- **Hugo Extended** (проверка: `hugo version` должен содержать слово `extended`)

> **Важно:** Обычная версия Hugo не умеет компилировать SCSS-стили темы Stack, что приведёт к ошибкам сборки или отсутствию стилей на сайте.

## 🛠 Требования к изображениям

- **webp** (для картинок)
- **SVG** (для иконок)

## 📝 Добавление новой заметки

```bash
hugo new content/post/nazvanie-zametki.md
```

Не забудь проверить Front Matter в начале файла и установить `draft: false` перед публикацией.

---

*Собрано с помощью Hugo. Хостится на GitHub Pages.*
