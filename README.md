import os
import logging
from telegram import Update
from telegram.ext import ApplicationBuilder, CommandHandler, MessageHandler, filters

# Настройки
TOKEN = os.getenv("TELEGRAM_BOT_TOKEN")
if not TOKEN:
    raise ValueError("Переменная TELEGRAM_BOT_TOKEN не установлена")

logging.basicConfig(level=logging.INFO)

# Функция для ответа на любое текстовое сообщение
async def echo(update: Update, context):
    user_message = update.message.text
    await update.message.reply_text(f"Привет! Я Любовь Мира. Ты написал: {user_message}")

# Запуск бота
if __name__ == "__main__":
    app = ApplicationBuilder().token(TOKEN).build()
    app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, echo))
    print("Бот запущен...")
    app.run_polling()
