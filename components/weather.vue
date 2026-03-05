<!-- u24666981 Motheo Morena-->
<script setup>
    import { ref, onMounted } from 'vue'

    const weather = ref(null);
    const weatherAPI = "https://api.open-meteo.com/v1/forecast?latitude=52.52&longitude=13.41&daily=weather_code,temperature_2m_max,temperature_2m_min,sunrise,sunset,daylight_duration,uv_index_max,rain_sum,wind_speed_10m_max&hourly=temperature_2m,rain,showers,uv_index,is_day,sunshine_duration&current=temperature_2m,relative_humidity_2m,showers,is_day&timezone=auto";
    
        async function getWeather() { 
            const response = await fetch(weatherAPI);
            
            try {
                if (response.ok) {
                    const data = await response.json();
                    weather.value = data;
                    console.log(data);
                }

                else {
                    throw new Error('Error with network response');
                }
            }

            catch(error) {
                console.log('Error: ', error);
            }
            
        }

    onMounted( ()=> {
        getWeather();
    })
</script>

<template>
    <div v-if = "weather">
        <h2> Current Weather </h2>

        <p>Temperature: {{ weather.current.temperature_2m }}ºC </p>
        <p>Humidity: {{ weather.current.relative_humidity_2m }}% </p>
    </div>
</template>