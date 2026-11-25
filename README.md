# Telegram Bot Clean Template

A clean, production-ready template for building Telegram bots in Python.

This template follows **Clean Architecture (light)** principles:
- thin Telegram handlers
- explicit business logic layer
- clear dependency wiring
- environment-based configuration

Designed to be reusable for **any Telegram bot**, from simple utilities to complex services.

---

## ✨ Features

- Clean and scalable project structure
- Explicit configuration via `.env`
- Business logic isolated in `services/`
- Thin Telegram handlers
- Repository pattern for data access
- Easy to extend and test
- Docker-ready

---

## 📁 Project Structure

```text
bot/
├── main.py            # Application entry point
├── setup.py           # Composition root (setup_bot)
│
├── config/            # Application settings
├── handlers/          # Telegram handlers (commands, messages, callbacks)
├── keyboards/         # Inline / Reply keyboards
├── services/          # Business logic (use cases)
├── repositories/      # Data access layer
├── db/                # Database infrastructure
├── i18n/              # Internationalization
├── utils/             # Shared helpers
├── workers/           # Background tasks (optional)
├── pipeline/          # Processing pipelines (optional)
└── admin/             # Admin features (optional)
```

---

## 🚀 Quick Start

### 1️⃣ Clone the repository

```bash
git clone https://github.com/your-org/telegram-bot-template.git
cd telegram-bot-template
```

---

### 2️⃣ Create environment config

```bash
cp .env.example .env
```

Edit `.env` and set your bot token:

```env
BOT_TOKEN=your_telegram_bot_token
```

---

### 3️⃣ Install dependencies

```bash
pip install -r requirements.txt
```

---

### 4️⃣ Run the bot

```bash
python -m bot.main
```

---

## ⚙️ Configuration

All configuration is centralized in:

```text
bot/config/settings.py
```

Settings are loaded from environment variables using **Pydantic**.

Example:

```python
from bot.config.settings import settings

settings.bot_token
settings.debug
```

If a required variable is missing, the application will fail fast on startup.

---

## 🧠 Architecture Overview

### Flow

```text
Telegram update
   ↓
Handlers (thin)
   ↓
Services (business logic)
   ↓
Repositories (data access)
```

---

### Handlers

- Only handle Telegram-specific logic
- Delegate all business rules to services

Example:

```python
@router.message(Command("start"))
async def start(message):
    user_service.ensure_user(message.from_user)
    await message.answer("Welcome!")
```

---

### Services

- Contain application business logic
- Independent from Telegram framework
- Easy to unit-test

Example:

```python
class UserService:
    def ensure_user(self, tg_user):
        ...
```

---

### Repositories

- Responsible for data access
- Abstract database logic from services

---

## 🧩 Dependency Wiring

All dependencies are created and connected in one place:

```text
bot/setup.py
```

This file acts as the **composition root** and defines `setup_bot()`.

This approach:
- avoids hidden dependencies
- simplifies testing
- makes the application easier to reason about

---

## 🌍 Internationalization (i18n)

Translations are stored in:

```text
bot/i18n/
```

You can add new languages by creating a new file, e.g. `de.py`.

---

## 🐳 Docker Support

The template includes:

- `Dockerfile`
- `docker-compose.yml`
- `docker-compose.dev.yml`

To run with Docker:

```bash
docker-compose up --build
```

---

## 🧪 Testing (recommended)

Business logic lives in `services/`, which makes it easy to write unit tests.

Suggested structure:

```text
tests/
├── services/
│   └── test_user_service.py
```

---

## 📌 Guidelines

- Keep handlers thin
- Do not access the database directly from handlers
- Put all business rules into services
- Keep `setup.py` as the single place for wiring dependencies

---

## 📄 License

MIT License.

Feel free to use this template for personal or commercial projects.
# sorts_maker
