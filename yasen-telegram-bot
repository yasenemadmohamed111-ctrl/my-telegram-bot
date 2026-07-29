import telebot
import requests

TELEGRAM_TOKEN = '8975671165:AAHYLM8rHhhUsyLh89m4_TZbA9VE1qpyuHc'
GEMINI_API_KEY = 'AQ.Ab8RN6Ir5ha1lEjqXpIaSz6Mn7jN9CjLaox9xazaMuZlTlPPyQ'

bot = telebot.TeleBot(TELEGRAM_TOKEN)

def get_ai_response(prompt):
    url = f"https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key={GEMINI_API_KEY}"
    headers = {'Content-Type': 'application/json'}
    data = {
        "contents": [{"parts": [{"text": prompt}]}]
    }
    
    try:
        response = requests.post(url, json=data, headers=headers)
        if response.status_code == 200:
            result = response.json()
            return result['candidates'][0]['content']['parts'][0]['text']
        else:
            return "Sorry, there was an issue connecting to the AI server."
    except Exception as e:
        return "Sorry, please try again."

@bot.message_handler(func=lambda message: True)
def handle_message(message):
    user_text = message.text.strip()
    
    if user_text.lower() in ["hi", "hello", "hey"]:
        bot.reply_to(message, "Hello! How can I help you today?")
    elif user_text.lower() in ["who are you", "who r u"]:
        bot.reply_to(message, "I am an AI bot, ready to answer your questions!")
    else:
        ai_reply = get_ai_response(user_text)
        bot.reply_to(message, ai_reply)

print("Smart bot is running...")
bot.infinity_polling()
