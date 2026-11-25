# Shorts Maker

A Telegram bot that makes YouTube Shorts from a video sent by the client.

The client sends a video in chat. The bot cuts it into short vertical clips and returns the finished Shorts.

## How it works

```text
Client sends a video
        ↓
Handlers — accept the message and the file
        ↓
Services — decide what to do with the video
        ↓
Pipeline — cut and assemble the Shorts
        ↓
Client receives the finished clips
```

Handlers only accept Telegram updates and hand work to services. Data access goes through repositories. Dependencies are wired in `bot/setup.py`.

## Layout

```text
bot/
├── main.py            # process entry point
├── setup.py           # bot and dependency wiring
├── config/            # settings from the environment
├── handlers/          # commands, messages, callbacks
├── keyboards/         # keyboards
├── services/          # bot use cases
├── repositories/      # data access
├── db/                # database
├── pipeline/          # Shorts cutting and assembly
├── workers/           # background tasks
├── i18n/              # copy
├── admin/             # admin features
└── utils/             # shared helpers
```

## Run

You need Python 3.11 and a bot token from [@BotFather](https://t.me/BotFather).

```bash
cp .env.example .env
```

Set the token in `.env`:

```env
BOT_TOKEN=your_telegram_bot_token
```

Locally:

```bash
pip install -r requirements.txt
python -m bot.main
```

With Docker:

```bash
docker compose up --build
```

For development, with the project mounted into the container:

```bash
docker compose -f docker-compose.dev.yml up --build
```

Settings are read from environment variables. `BOT_TOKEN` is required. Database path, app mode, and proxies are listed in `.env.example`.
