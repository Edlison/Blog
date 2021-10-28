---
title: telegram bot
categories:
- Telegram
tags:
- bot
---

# Intro

build a telegram bot for yourself

# hello code

```python
from telegram import Update
from telegram.ext import Updater, CommandHandler, CallbackContext
import logging


def start(update: Update, context: CallbackContext) -> None:
    context.bot.send_message(chat_id=update.effective_chat.id, text="I'm a bot, created by Edlison.")
```

```python
if __name__ == '__main__':
    REQUEST_KWARGS = {'proxy_url': 'socks5h://127.0.0.1:1080'}
    u = Updater('bot token here', use_context=True, request_kwargs=REQUEST_KWARGS)

    start_handler = CommandHandler('start', start, pass_job_queue=True)
    u.dispatcher.add_handler(start_handler)

    logging.basicConfig(format='%(asctime)s - %(name)s - %(levelname)s - %(message)s', level=logging.INFO)

    u.start_polling()
```

There's a problem about proxy.

To use v2ray agenting my data, the args `proxy_url` should be defined and passing it to the `Updater`.







----

Reference

https://github.com/python-telegram-bot/python-telegram-bot/wiki/Extensions-%E2%80%93-Your-first-Bot