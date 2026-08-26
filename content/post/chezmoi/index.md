---
title: "Chezmoi: элегантное управление dot-файлами в Linux и Windows"
description: "Как безопасно и удобно синхронизировать пользовательские конфиги между разными ОС с помощью chezmoi, шаблонов Go и Git."
date: 2026-02-25
draft: false
slug: "chezmoi-dotfiles-management"
image: chezmoi-dotfiles-management-cover.webp
categories:
  - DevOps
  - Инфраструктура
  - Операционные системы
tags:
  - Linux
  - Windows
  - DevOps
  - Chezmoi
  - Git
  - CLI
---

Управление конфигурационными файлами (`dotfiles`) на нескольких машинах рано или поздно превращается в хаос. Обычный Git-репозиторий в домашней директории быстро замусоривается, симлинки ломаются на Windows, а хранить в открытом доступе токены или имена пользователей крайне небезопасно.

Решением этой проблемы стал **chezmoi** — современный менеджер dotfiles, написанный на Go. Он позволяет безопасно и системно управлять настройками в Linux, WSL и Windows.

---

### 🚀 В чём преимущество Chezmoi?

В отличие от традиционного подхода с симлинками, **chezmoi** хранит целевые конфиги в отдельной директории (по умолчанию `~/.local/share/chezmoi`) и применит изменения в реальную систему только по вашей команде.

* **Кроссплатформенность**: Одинаково эффективно работает в Unix-подобных системах, WSL и Windows.
* **Шаблонизация на базе Go Templates**: Позволяет динамически подставлять переменные (имя пользователя, hostname, email) в зависимости от текущего хоста.
* **Безопасность**: Нативная поддержка шифрования секретных данных через `age` или `GnuPG`.
* **Автоматизация**: Возможность выполнения `run_once_` скриптов установки пакетов при первом развертывании системы.

---

### 📦 Структура и организация dotfiles

Пример структуры репозитория dotfiles, управляемого chezmoi:

```text
dotfiles/
├── .chezmoi.toml.tmpl                     # Шаблон конфигурации chezmoi
├── .chezmoiignore                         # Игнорируемые файлы и директории
├── dot_bashrc                             # Превратится в ~/.bashrc
├── dot_gitconfig.tmpl                     # Шаблон ~/.gitconfig с переменными
├── private_dot_config/                    # Превратится в ~/.config/
│   ├── helix/                             # Конфигурация редактора Helix
│   ├── starship/                          # Настройки промпта Starship
│   └── wezterm/                           # Кроссплатформенный терминал WezTerm
├── run_once_after_10-base-packages.sh.tmpl   # Установка CLI-пакетов (Linux/WSL)
└── run_once_after_20-windows-packages.ps1.tmpl # Установка пакетов (Windows)
```

> [!note] Именование файлов
> Префиксы в именах файлов chezmoi указывают на их атрибуты в целевой системе: `dot_` превращается в точку (`.bashrc`), `private_` создает приватную папку (`chmod 700`), а `.tmpl` включает генератор шаблонов.

---

### ⚡ Быстрый старт и инициализация

#### Linux / WSL

1. **Установка утилиты:**
   ```bash
   sh -c "$(curl -fsLS get.chezmoi.io)" -- -b ~/.local/bin
   export PATH="$HOME/.local/bin:$PATH"
   ```

2. **Инициализация из репозитория GitHub:**
   ```bash
   chezmoi init --apply <ваш-username>
   ```

#### Windows

В Windows удобнее всего использовать менеджер пакетов **Scoop**:

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned -Force
iwr -useb get.scoop.sh | iex
scoop install main/chezmoi git gh

# Инициализация конфигурации в Git Bash:
chezmoi init --apply <ваш-username>
```

---

### 🔄 Шпаргалка по ежедневным командам

| Команда | Описание |
| :--- | :--- |
| `chezmoi edit ~/.bashrc` | Открыть файл в редакторе по умолчанию. |
| `chezmoi diff` | Показать различия между репозиторием и текущей `$HOME`. |
| `chezmoi apply -v` | Применить изменения из исходников к рабочей системе. |
| `chezmoi update` | Подтянуть изменения из Git и сразу применить их. |
| `chezmoi add ~/.config/helix/` | Добавить новую директорию под управление chezmoi. |
| `chezmoi cd` | Перейти в локальную рабочую директорию chezmoi. |

---

### 📊 Использование шаблонов (Templates)

Благодаря шаблонам Go вы можете использовать единый `dot_gitconfig.tmpl` для всех своих устройств:

```text
[user]
    name = {{ .name }}
    email = {{ .email }}
```

Переменные считываются из вашего персонального файла `.chezmoi.toml` или вводятся через интерактивный промпт при инициализации.

> [!warning] Внимание при работе со скриптами
> Скрипты с префиксом `run_once_` запускаются автоматически только один раз. Перед их применением всегда проверяйте сгенерированный код командой `chezmoi execute-template < <file>`.
>
> На Windows для исключения случайно запущенных Bash-скриптов рекомендую выполнять компиляцию с параметром:
> `chezmoi apply --exclude=scripts`.

---

### 📚 Источники и ссылки

* 🌐 [Официальная документация Chezmoi](https://www.chezmoi.io/)
* 🛠 [Пример конфигурации dotfiles на GitHub](https://github.com/The-Old-Cat/dotfiles)
