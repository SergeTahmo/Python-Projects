import requests
import datetime
import matplotlib.pyplot as plt

API_KEY = "your_openweathermap_api_key"
BASE_URL = "http://api.openweathermap.org/data/2.5/weather?"

def get_weather_data(city):
    """Fetch current weather data for a city."""
    url = BASE_URL + f"q={city}&appid={API_KEY}&units=metric"
    response = requests.get(url)
    if response.status_code == 200:
        return response.json()
    else:
        print("Error fetching weather data.")
        return None

def display_weather(data):
    """Display weather information from the API response."""
    print("\n📍 Weather Information:")
    print(f"City: {data['name']}")
    print(f"Temperature: {data['main']['temp']}°C")
    print(f"Feels Like: {data['main']['feels_like']}°C")
    print(f"Weather: {data['weather'][0]['description'].capitalize()}")
    print(f"Humidity: {data['main']['humidity']}%")
    print(f"Wind Speed: {data['wind']['speed']} m/s")
    print(f"Date/Time: {datetime.datetime.now().strftime('%Y-%m-%d %H:%M:%S')}")

def plot_temperature_trend(city):
    """Simulate and plot a temperature trend over 7 days."""
    import random
    days = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
    temps = [random.randint(15, 35) for _ in range(7)]

    plt.figure(figsize=(8, 5))
    plt.plot(days, temps, marker='o', color='royalblue', linestyle='--')
    plt.title(f"Weekly Temperature Forecast (Simulated) - {city}")
    plt.xlabel("Day")
    plt.ylabel("Temperature (°C)")
    plt.grid(True)
    plt.tight_layout()
    plt.savefig("temperature_trend.png")
    plt.show()

if __name__ == "__main__":
    print("🌦️  Welcome to the Weather CLI Tool!")
    city = input("Enter a city name: ")
    
    weather_data = get_weather_data(city)
    
    if weather_data:
        display_weather(weather_data)
        plot_temperature_trend(city)
