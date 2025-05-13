Install with:
pip install requests

main.py
import requests
def get_exchange_rate(base_currency, target_currency):
    url = f"https://api.exchangerate-api.com/v4/latest/{base_currency.upper()}"
    response = requests.get(url)
    if response.status_code != 200:
        raise Exception("Failed to fetch exchange rates.")
    data = response.json()
    rates = data.get("rates")
    if target_currency.upper() not in rates:
        raise Exception("Invalid target currency.")
    return rates[target_currency.upper()]
def convert_currency(amount, base_currency, target_currency):
    try:
        rate = get_exchange_rate(base_currency, target_currency)
        converted_amount = amount * rate
        return converted_amount
    except Exception as e:
        return str(e)

if __name__ == "__main__":
    print("Currency Converter")
    base = input("Enter base currency (e.g., USD): ")
    target = input("Enter target currency (e.g., EUR): ")
    amount = float(input("Enter amount: "))
    result = convert_currency(amount, base, target)
    if isinstance(result, float):
        print(f"{amount} {base.upper()} = {result:.2f} {target.upper()}")
    else:
        print("Error:", result)

README.md
# Currency Converter
A simple Python project to convert one currency to another using real-time exchange rates from a free API.

## Features
- Real-time exchange rates
- Converts any amount between supported currencies
- Handles basic errors

## Requirements
- Python 3
- requests

Install dependencies:
```bash
pip install requests

Usage
python main.py

API Used
ExchangeRate-API (Free Tier)
### 📌 Instructions to Upload on GitHub

1. Create a folder on your computer: `currency-converter`.
2. Add the `main.py` and `README.md` files inside.
3. Open terminal or Git Bash:
   ```bash
   cd path/to/currency-converter
   git init
   git add .
   git commit -m "Initial commit - Currency Converter"
