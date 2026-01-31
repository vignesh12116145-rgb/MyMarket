import requests
import os
import time

def send_message(chat_id, text):
    token = os.getenv("TELEGRAM_TOKEN")
    url = f"https://api.telegram.org/bot{token}/sendMessage"
    requests.post(url, data={"chat_id": chat_id, "text": text})

def listen_for_messages():
    token = os.getenv("TELEGRAM_TOKEN")
    last_update_id = 0
    print("Bot is now listening for 5 minutes...")
    
    # Listen for 5 minutes (GitHub Actions will stop after this)
    timeout = time.time() + 300 
    while time.time() < timeout:
        url = f"https://api.telegram.org/bot{token}/getUpdates?offset={last_update_id + 1}"
        response = requests.get(url).json()
        
        if response.get("result"):
            for update in response["result"]:
                last_update_id = update["update_id"]
                user_msg = update["message"]["text"]
                chat_id = update["message"]["chat"]["id"]
                
                print(f"Received: {user_msg}")
                if "/start" in user_msg:
                    send_message(chat_id, "Hello! I am your Financial Hub. Send me 'market' for prices.")
                elif "market" in user_msg.lower():
                    send_message(chat_id, "Fetching market data for you... (Processing)")
        
        time.sleep(2) # Wait 2 seconds between checks

if __name__ == "__main__":
    # First, send your daily report
    # (Add your get_indian_market() calls here)
    
    # Then, start listening
    listen_for_messages()
