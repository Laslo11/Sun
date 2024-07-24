import requests
from datetime import datetime, timedelta

# Определяем функцию для получения погодных данных
def get_weather_data(location, date):
    # Пример запроса к API погоды (фиктивный URL)
    # response = requests.get(f"http://api.weather.com/v1/location/{location}/date/{date}/data")
    # data = response.json()
    # В реальном приложении заменить на получение реальных данных
    # Пример структуры ответа
    data = {
        "date": date,
        "weather": "sunny" if int(date.split('-')[2]) % 2 == 0 else "cloudy"
    }
    return data

# Функция для подсчета солнечных и облачных дней
def count_sunny_and_cloudy_days(year, location):
    sunny_days = 0
    cloudy_days = 0

    # Проходим по каждому дню года
    start_date = datetime(year, 1, 1)
    end_date = datetime(year, 12, 31)
    delta = timedelta(days=1)

    current_date = start_date
    while current_date <= end_date:
        date_str = current_date.strftime("%Y-%m-%d")
        weather_data = get_weather_data(location, date_str)
        
        if weather_data["weather"] == "sunny":
            sunny_days += 1
        elif weather_data["weather"] == "cloudy":
            cloudy_days += 1
        
        current_date += delta

    return sunny_days, cloudy_days

# Пример использования
year = 2023
location = "Eastern Europe"
sunny_days, cloudy_days = count_sunny_and_cloudy_days(year, location)
print(f"In {year}, there were {sunny_days} sunny days and {cloudy_days} cloudy days in {location}.")
