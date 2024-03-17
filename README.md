import requests
from datetime import datetime

# Replace 'YOUR_API_KEY_ID' and 'YOUR_API_SECRET_KEY' with your actual API keys
API_KEY_ID = 'PKY0ZZIZH3ZIPZSQZ7AV'
API_SECRET_KEY = 'lg7eQzGZQqRVfoMrTxuKbxUJENwFTdwQbADR6Gv3'

# Define the symbol for QQQ
symbol = 'QQQ'

# Get today's date
today_date = datetime.now().strftime('%Y-%m-%d')

# Make API request to retrieve latest quote data for QQQ
response = requests.get(f'https://data.alpaca.markets/v1/last_quote/stocks/{symbol}',
                        headers={'APCA-API-KEY-ID': API_KEY_ID, 'APCA-API-SECRET-KEY': API_SECRET_KEY})

# Check if request was successful
if response.status_code == 200:
    data = response.json()
    
    # Extract the latest quote data
    latest_quote = data['last']
    
    # Extract open and close prices
    open_price = latest_quote['o']
    close_price = latest_quote['c']
    
    print(f'Open price for {symbol} on {today_date}: ${open_price}')
    print(f'Close price for {symbol} on {today_date}: ${close_price}')
else:
    print(f'Failed to retrieve data. Status code: {response.status_code}')
