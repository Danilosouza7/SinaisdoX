import os
import random
import telebot
import time
from datetime import datetime
from pytz import timezone
from telebot.types import InlineKeyboardMarkup, InlineKeyboardButton
7
api_key = '7647223064:AAGwi-FfMGOgoXVpUY3dfPwm-nDx3Si1NzM'  # Substitua com o token do seu bot
chat_id = '-1002308103239'  # Substitua com o ID do canal ou chat

bot = telebot.TeleBot(token=api_key)

# Diretório onde o script está localizado
diretorio_script = os.path.dirname(os.path.abspath(__file__))
diretorio_imagens = os.path.join(diretorio_script, 'imagens')

# Lista os arquivos no diretório de imagens
arquivos = os.listdir(diretorio_imagens)

def enviar_imagem_aleatoria():
    # Escolhe aleatoriamente uma imagem
    imagem_escolhida = random.choice(arquivos)

    # URL do link
    url_link = "LINK DA PLATAFORMA"

    # Define o fuso horário para Brasília
    tz = timezone('America/Sao_Paulo')

    # Abre a imagem selecionada
    with open(os.path.join(diretorio_imagens, imagem_escolhida), 'rb') as imagem:
        bot.send_photo(chat_id=chat_id, photo=imagem, caption="Imagem aleatória")

@bot.callback_query_handler(func=lambda call: call.data == 'finalizado')
def finalizado_callback(call):
    bot.send_message(chat_id, "Processo finalizado")

while True:
    enviar_imagem_aleatoria()
    time.sleep(60 * 60)  # Aguarda uma hora antes de enviar a próxima imagem
