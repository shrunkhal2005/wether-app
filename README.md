# weather-app
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Weather App</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
      max-width: 400px;
      margin: auto;
      background: #f0f8ff;
      text-align: center;
    }
    input {
      padding: 10px;
      width: 70%;
      font-size: 1rem;
      margin-right: 5px;
      border: 1px solid #ccc;
      border-radius: 4px;
    }
    button {
      padding: 10px 15px;
      font-size: 1rem;
      border: none;
      background-color: #007bff;
      color: white;
      border-radius: 4px;
      cursor: pointer;
    }
    button:hover {
      background-color: #0056b3;
    }
    #result {
      margin-top: 20px;
      font-weight: bold;
      font-size: 1.2rem;
    }
  </style>
</head>
<body>
  <h1>Weather App</h1>
  <input type="text" id="city" placeholder="Enter city name" />
  <button onclick="getWeather()">Get Weather</button>
  <div id="result"></div>

  <script>
    async function getWeather() {
      const city = document.getElementById('city').value.trim();
      if (!city) {
        alert('Please enter a city name');
        return;
      }
      const apiKey = 'YOUR_OPENWEATHERMAP_API_KEY'; // Replace with your API key
      const url = `https://api.openweathermap.org/data/2.5/weather?q=${encodeURIComponent(city)}&appid=${apiKey}&units=metric`;

      const resultDiv = document.getElementById('result');
      resultDiv.textContent = 'Loading...';

      try {
        const response = await fetch(url);
        if (!response.ok) throw new Error('City not found');
        const data = await response.json();
        resultDiv.textContent = `Temperature in ${data.name}: ${data.main.temp}°C, ${data.weather[0].description}`;
      } catch (error) {
        resultDiv.textContent = error.message;
      }
    }
  </script>
</body>
</html>

