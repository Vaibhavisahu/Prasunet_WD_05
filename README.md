Prasunet_Code_TaskNo.05. HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h1 id="city-name"></h1>
    <p id="date"></p>
    <p id="temperature"></p>
    <p id="description"></p>
    <p id="wind-speed"></p>
    <img id="weather-icon" src="" alt="Weather Icon">
    <script src="script.js"></script>
</body>
</html

  Prasunet_Code_TaskNo.05. CSS
   
   body {
    font-family: Arial, sans-serif;
    text-align: center;
}

#city-name {
    font-size: 24px;
    font-weight: bold;
}

#date {
    font-size: 18px;
    color: #666;
}

#temperature {
    font-size: 36px;
    font-weight: bold;
    color: #333;
}

#description {
    font-size: 18px;
    color: #666;
}

#wind-speed {
    font-size: 18px;
    color: #666;
}

#weather-icon {
    width: 50px;
    height: 50px;
    margin: 20px;
}

 Prasunet_Code_TaskNo.05. JAVA

 const apiKey = 'YOUR_API_KEY';
const url = `https://api.openweathermap.org/data/2.5/weather`;

async function getWeatherData(city) {
    const response = await fetch(`${url}?q=${city}&appid=${apiKey}&units=metric`);
    const data = await response.json();
    return data;
}

async function displayWeatherData(city) {
    const data = await getWeatherData(city);
    document.getElementById('city-name').textContent = data.name;
    document.getElementById('date').textContent = moment().format('MMMM Do YYYY, h:mm:ss a');
    document.getElementById('temperature').innerHTML = `${data.main.temp}°C`;
    document.getElementById('description').textContent = data.weather[0].description;
    document.getElementById('wind-speed').innerHTML = `Wind Speed: ${data.wind.speed} m/s`;
    document.getElementById('weather-icon').src = `http://openweathermap.org/img/w/${data.weather[0].icon}.png`;
}

document.addEventListener('DOMContentLoaded', () => {
    const cityInput = document.createElement('input');
    cityInput.type = 'text';
    cityInput.placeholder = 'Enter city name';
    document.body.appendChild(cityInput);

    const button = document.createElement('button');
    button.textContent = 'Get Weather';
    document.body.appendChild(button);

    button.addEventListener('click', () => {
        const city = cityInput.value;
        displayWeatherData(city);
    });
});
