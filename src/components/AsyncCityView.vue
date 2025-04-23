<template>
  <div></div>
</template>

<script setup>
/* useRouter() (Vue Router)
Gives you access to the router instance.

You use it to:

    --Navigate programmatically (e.g., router.push()).

    --Access router-level methods like replace, go, etc. */

/* useRoute() (Vue Router)
Gives you access to the current route object.

You use it to:

    --Read current path, query params, route params, etc.

    --Reactively watch changes in route. */

import axios from "axios";
import { useRoute } from "vue-router";

const route = useRoute();
const getWeatherData = async () => {
  try {
    const weatherData = await axios.get(
      `https://api.openweathermap.org/data/3.0/onecall?lat=${route.query.lat}&lon=${route.query.lng}&exclude={part}&appid=7efa332cf48aeb9d2d391a51027f1a71&units=imperial`
    );

    // cal current date & time
    const localOffset = new Date().getTimezoneOffset() * 60000;
    const utc = weatherData.data.current.dt * 1000 + localOffset;
    weatherData.data.currentTime =
      utc + 1000 * weatherData.data.timezone_offset;

    // cal hourly weather offset
    weatherData.data.hourly.forEach((hour) => {
      const utc = hour.dt * 1000 + localOffset;
      hour.currentTime = utc + 1000 * weatherData.data.timezone_offset;
    });

    return weatherData;
  } catch (err) {
    console.log(err);
  }
};
const weatherData = await getWeatherData();
console.log(weatherData);
</script>
