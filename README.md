<!DOCTYPE html>
<html lang="ku">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>کێشوهەوا - هەرێمی کوردستان</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(to right, #2b5876, #4e4376);
            color: white;
            text-align: center;
            padding: 20px;
        }
        h1 {
            margin-bottom: 10px;
        }
        .city {
            background: rgba(255, 255, 255, 0.2);
            padding: 15px;
            margin: 10px auto;
            border-radius: 10px;
            width: 80%;
            max-width: 400px;
        }
        .temp {
            font-size: 24px;
            font-weight: bold;
        }
        .desc {
            font-size: 18px;
            margin-top: 5px;
        }
    </style>
</head>
<body>

    <h1>کێشوهەوای هەرێمی کوردستان</h1>
    <div id="weather"></div>

    <script>
        const cities = ["Erbil", "Sulaymaniyah", "Duhok", "Halabja", "Kirkuk"];
        const apiKey = "YOUR_API_KEY";
        const weatherContainer = document.getElementById("weather");

        async function fetchWeather(city) {
            const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric&lang=ku`;
            const response = await fetch(url);
            const data = await response.json();
            return {
                city: city,
                temp: data.main.temp,
                desc: data.weather[0].description
            };
        }

        async function updateWeather() {
            weatherContainer.innerHTML = "";
            for (const city of cities) {
                const weather = await fetchWeather(city);
                weatherContainer.innerHTML += `
                    <div class="city">
                        <h2>${weather.city}</h2>
                        <div class="temp">${weather.temp}°C</div>
                        <div class="desc">${weather.desc}</div>
                    </div>
                `;
            }
        }

        updateWeather();
        setInterval(updateWeather, 3600000); // Update every hour
    </script>

</body>
</html>
