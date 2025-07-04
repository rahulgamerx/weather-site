
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="description" content="Live Weather Checker - Get instant weather updates for any city worldwide. Built by Rahul Gamerx." />
  <meta name="keywords" content="weather, live weather, forecast, city temperature, Rahul Gamerx" />
  <meta name="author" content="Rahul Gamerx" />
  <title>🌦️ Live Weather - Rahul Gamerx</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap" rel="stylesheet">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Poppins', sans-serif;
    }
    body {
      background: linear-gradient(to bottom, #a2d4f6, #f2fbff);
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: flex-start;
      text-align: center;
      padding: 20px;
    }
    header {
      width: 100%;
      background: transparent;
      color: #333;
      padding: 15px;
      display: flex;
      justify-content: center;
      align-items: center;
      position: relative;
    }
    .header-title {
      font-weight: bold;
      font-size: 18px;
      color: #0077ff;
      white-space: nowrap;
      overflow: hidden;
      border-right: 2px solid #0077ff;
      width: 0;
      animation: typing 4s steps(30, end) forwards, blink 0.8s infinite;
    }
    @keyframes typing {
      from { width: 0; }
      to { width: 250px; }
    }
    @keyframes blink {
      0%, 100% { border-color: transparent; }
      50% { border-color: #0077ff; }
    }
    h1 {
      font-size: 2.5rem;
      color: #333;
      margin: 20px 0 10px;
      animation: fadeIn 1s ease-in;
    }
    .input-box {
      margin: 15px 0;
    }
    input {
      padding: 12px;
      font-size: 16px;
      width: 280px;
      border: 1px solid #ccc;
      border-radius: 10px;
      outline: none;
    }
    button {
      padding: 12px 25px;
      font-size: 16px;
      background-color: #0077ff;
      color: white;
      border: none;
      border-radius: 10px;
      margin-top: 10px;
      cursor: pointer;
      transition: all 0.3s ease;
    }
    button:hover {
      background-color: #005fcc;
    }
    #weather {
      margin-top: 25px;
      background: white;
      padding: 25px;
      border-radius: 15px;
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
      width: 90%;
      max-width: 400px;
      animation: slideUp 1s ease;
    }
    #weather img {
      width: 100px;
      height: 100px;
      animation: float 3s infinite ease-in-out;
    }
    footer {
      margin-top: auto;
      padding: 20px;
      width: 100%;
      background-color: #f0f0f0;
      font-size: 14px;
      color: #444;
    }
    footer a {
      text-decoration: none;
      color: #0077ff;
    }
    footer a:hover {
      text-decoration: underline;
    }
    @keyframes fadeIn {
      from {opacity: 0; transform: translateY(-10px);}
      to {opacity: 1; transform: translateY(0);}
    }
    @keyframes slideUp {
      from {opacity: 0; transform: translateY(20px);}
      to {opacity: 1; transform: translateY(0);}
    }
    @keyframes float {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-10px); }
    }
  </style>
</head>
<body>
  <header>
    <div class="header-title">India Weather Dekhoo</div>
  </header>

  <h1>⛅ Weather Checker</h1>
  <div class="input-box">
    <input type="text" id="city" placeholder="Enter city name">
    <br>
    <button onclick="getWeather()">Get Weather</button>
  </div>

  <div id="weather"></div>

  <footer>
    <p><a href="#">Home</a> | <a href="#">Privacy Policy</a> | <a href="#">Disclaimer</a></p>
    <p>Made with ❤️ by <strong>Rahul Gamerx</strong> | Powered by <a href="https://openweathermap.org/">OpenWeatherMap</a></p>
    <p>UI & Code with 🤖 by <a href="https://openai.com/chatgpt">ChatGPT</a></p>
  </footer>

  <script>
    async function getWeather() {
      const city = document.getElementById("city").value;
      const apiKey = "dc169e2c5160f42f9f656016e23be6b8"; // 👈 Replace with your actual API key

      if (!city) {
        alert("Please enter a city name.");
        return;
      }

      document.getElementById("weather").innerHTML = "Loading...";

      try {
        const weatherUrl = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`;
        const response = await fetch(weatherUrl);
        const data = await response.json();

        if (data.cod === 200) {
          const icon = data.weather[0].icon;
          const iconUrl = `https://openweathermap.org/img/wn/${icon}@2x.png`;

          document.getElementById("weather").innerHTML = `
            <img src="${iconUrl}" alt="Weather Icon" />
            <h2>${data.name}, ${data.sys.country}</h2>
            <p><strong>${data.weather[0].description}</strong></p>
            <p>🌡️ Temp: ${data.main.temp}°C</p>
            <p>💨 Wind: ${data.wind.speed} m/s</p>
          `;
        } else {
          document.getElementById("weather").innerHTML = "❌ City not found.";
        }

      } catch (error) {
        document.getElementById("weather").innerHTML = "❌ Error fetching data.";
      }
    }
  </script>
</body>
</html>
