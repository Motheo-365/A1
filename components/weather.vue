<!-- u24666981 Motheo Morena-->
<script setup>
    import { ref, onMounted } from 'vue'

    const weather = ref(null);
    const weatherAPI = "https://api.open-meteo.com/v1/forecast?latitude=-25.7479&longitude=28.2293&daily=temperature_2m_max,temperature_2m_min,sunrise,sunset,uv_index_max&hourly=uv_index,is_day,sunshine_duration,rain&current=temperature_2m,relative_humidity_2m,showers,is_day,rain&timezone=auto";

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
        <p>Rain: {{ weather.current.rain }}mm </p>
        <p>Humidity: {{ weather.current.relative_humidity_2m }}% </p>
    
    </div>
</template>

<style scoped>
    h2 {
        font-size: 2.5rem;
    }
</style>