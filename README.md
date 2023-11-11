# heraku 
import os
import random
from telegram import Update
from telegram.ext import Updater, CommandHandler, CallbackContext

# Substitua 'SEU_TOKEN_BOT' pelo token do seu bot
TOKEN = '5923582499:AAEFn9OBHHT886VM7d9ZEmoIKnFBsP09gWg'

def start(update: Update, context: CallbackContext) -> None:
    update.message.reply_text('Bem-vindo ao CryptoBot! Use /previsao para obter uma previsão de mercado.')

def previsao(update: Update, context: CallbackContext) -> None:
    # Gere uma previsão aleatória (1 para aumento, 0 para queda)
    previsao = random.choice([1, 0])

    if previsao:
        mensagem = 'A previsão é de aumento no mercado!'
    else:
        mensagem = 'A previsão é de queda no mercado!'

    update.message.reply_text(mensagem)

def main() -> None:
    updater = Updater(TOKEN)

    dp = updater.dispatcher
    dp.add_handler(CommandHandler("start", start))
    dp.add_handler(CommandHandler("previsao", previsao))

    # Use o webhook se estiver hospedando no Heroku
    if 'HEROKU_APP_NAME' in os.environ:
        PORT = int(os.environ.get('PORT', '8443'))
        updater.start_webhook(listen="0.0.0.0", port=PORT, url_path=TOKEN)
        updater.bot.setWebhook(f"https://{os.environ['HEROKU_APP_NAME']}.herokuapp.com/{TOKEN}")

    else:
        updater.start_polling()

    updater.idle()

if __name__ == '__main__':
    main()
