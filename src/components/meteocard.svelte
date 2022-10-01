<script>
  import hot from '../hot.png';
  import rain from '../rain.png';
  import sun from '../sun.png';
  import wind from '../wind.png';
  import  bad from '../bad-weather.png';
  import cloudy from '../cloudy.png'
  var uv;
  var hum;
  var temp;
  var weather;
  var src;
  var windspeed;
  async function weatherdata() {
    const response = await fetch(
      "https://api.weather.com/v2/pws/observations/current?stationId=IMANER2&format=json&units=m&apiKey=82e1d083032049a8a1d083032029a891"
    );
    const data = await response.json();
    const { observations } = data;
    hum = observations[0].humidity;
    uv = observations[0].uv;
    temp = observations[0].metric.temp;
    windspeed = observations[0].metric.windspeed;
    if (hum > 80) {
      weather = "Piovoso";
      weather = weather;
      src = rain;
    } else if (uv > 3) {
      weather = "Livello UV alto";
      weather = weather;
      src = hot;
    } else if (temp > 30) {
      weather = "Soleggiato e caldo";
      weather = weather;
      src = sun;
    } else if (windspeed > 11) {
      weather = "Vento Moderato";
      weather = weather;
      src = wind;
    } else if (windspeed > 20) {
      weather = "Vento teso";
      weather = weather;
      src = bad;
    } else if (temp < 30) {
      weather = "fresco";
      weather = weather;
      src = cloudy;
    }
  }

  weatherdata();

  console.log(weather);
</script>

<div id="body">
  <div class="card">
    <h4>PIEVE VECCHIA</h4>
    <h6>{weather}</h6>
    <img {src} alt="icon" />
    <h1>{temp}<sup>°</sup></h1>
    <div class="container">
      <div class="details">
        <p>hum</p>
        <span>{hum}<sup>%</sup></span>
      </div>
      <div class="details">
        <p>Uv</p>
        <span>{uv}</span>
      </div>
    </div>
  </div>
</div>

<style>
  * {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  .card {
    height: 360px;
    width: 300px;
    background-color: rgba(255, 255, 255, 0.06);
    position: absolute;
    margin: auto;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    backdrop-filter: blur(20px);
    border: 1px solid rgba(255, 255, 255, 0.1);
    box-shadow: 20px 20px 22px rgba(0, 0, 0, 0.2);
    border-radius: 8px;
    font-family: "arial", sans-serif;
    color: #fcfcfc;
  }
  h4 {
    letter-spacing: 4px;
    font-weight: 600;
    font-size: 18px;
    text-align: center;
    margin: 25px 0 10px 0;
  }
  h6 {
    text-align: center;
    color: #b3b3b3;
    font-size: 15px;
    letter-spacing: 5px;
    font-weight: 300;
    margin-bottom: 25px;
  }
  .card img {
    width: 22%;
    margin-left: 39%;
  }
  h1 {
    letter-spacing: 2px;
    text-align: center;
    font-size: 50px;
    font-weight: 300;
  }
  .container {
    width: 70%;
    margin-left: 15%;
    display: grid;
    grid-template-columns: auto auto;
    margin-top: 30px;
  }
  .details {
    text-align: center;
    font-size: 13px;
    letter-spacing: 1px;
    font-weight: 600;
  }
  .details span {
    color: #b3b3b3;
  }
  .details:first-child {
    border-right: 2px solid #fcfcfc;
  }
</style>
