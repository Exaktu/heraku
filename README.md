[requirements.txt](https://github.com/Exaktu/heraku/files/13324388/requirements.txt)# heraku 
import os
import random[Uploading rFlask==2.0.1
python-telegram-bot==19.13
equirements.txt…]()

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

