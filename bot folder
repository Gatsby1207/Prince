from binance.client import Client
from telegram import Bot
import time

# API va tokenlar
BINANCE_API_KEY = "sArqgrCmEnAazqKgta2tDjCpTemixn0mlA5Gf5ibadqkTIXfTAr7p5czmtDWlxUn"
BINANCE_API_SECRET = "kHA2Yl5cujTKOiR2SRPSImnNqCFVMPxyC7QKbPU5jNb6lib5B6U2gdTfsqySgxB4"
TELEGRAM_BOT_TOKEN = "7801057914:AAGIbNyC5dTgqCWV7Ji8_NZ2d_Ti1pJwLnQ"
TELEGRAM_CHAT_ID = "1608597038"

# Coinlar
COINS = ["COTIUSDT", "LEVERUSDT", "ACHUSDT", "REZUSDT", "EIGENUSDT", "ETHUSDT", "BBUSDT", "IDUSDT"]

client = Client(BINANCE_API_KEY, BINANCE_API_SECRET)
bot = Bot(token=TELEGRAM_BOT_TOKEN)

def get_volume(symbol):
    klines = client.get_klines(symbol=symbol, interval=Client.KLINE_INTERVAL_1HOUR, limit=2)
    return float(klines[-1][5]) if len(klines) >= 2 else 0

def find_top_gainer():
    volumes = {coin: get_volume(coin) for coin in COINS}
    top_coin = max(volumes, key=volumes.get)
    return top_coin, volumes[top_coin]

async def send_telegram_message(message):
    await bot.send_message(chat_id=TELEGRAM_CHAT_ID, text=message)

async def main():
    while True:
        top_coin, volume = find_top_gainer()
        message = f"📈 Eng katta hajm o‘sishi: {top_coin}\n🔹 Hajm: {volume}"
        await send_telegram_message(message)
        time.sleep(3600)

if __name__ == "__main__":
    import asyncio
    asyncio.run(main())
