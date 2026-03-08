<!-- u24666981 Motheo Morena-->
<script setup>
    import { ref, onMounted, computed } from 'vue'

    const weather = ref(null)

    const weatherAPI =
        "https://api.open-meteo.com/v1/forecast?latitude=-25.7479&longitude=28.2293&daily=temperature_2m_max,temperature_2m_min,sunrise,sunset,uv_index_max&hourly=uv_index,is_day,sunshine_duration,rain,cloud_cover&current=temperature_2m,relative_humidity_2m,showers,is_day,rain,weather_code&timezone=auto"
    
        async function getWeather() {
        const response = await fetch(weatherAPI)

        try {
            if (response.ok) {
                const data = await response.json()
                weather.value = data
                console.log(data)
            } 
            else {
                throw new Error('Error with network response')
            }
        } 
        catch (error) {
            console.log('Error: ', error)
        }
    }

    onMounted(() => {
        getWeather()
    })

    /* determine if it is day */
    const isDay = computed(() => {
        return weather.value?.current?.is_day === 1
    })

    function formatTime(dateString) {
        const date = new Date(dateString)

        return date.toLocaleTimeString([], {
            hour: '2-digit',
            minute: '2-digit'
        })
    }
</script>

<template>
    <div v-if="weather" class = "block">

        <h2>Current Weather in {{ weather.timezone }}</h2>

        <img :src="isDay ? '/media/sunny.gif' : '/media/night.gif'" alt="Sun animation">
        <p>
        {{ isDay 
            ? 'Sunset: ' + formatTime(weather.daily.sunset[0]) 
            : 'Sunrise: ' + formatTime(weather.daily.sunrise[0]) 
        }}
        </p>   
         <div class = "weather-block">
            <p>Temperature: {{ weather.current.temperature_2m }}ºC</p>
            <p>Rain: {{ weather.current.rain }}mm</p>
            <p>Humidity: {{ weather.current.relative_humidity_2m }}%</p>
        </div>
    </div>
</template>

<style scoped>
    h2 {
        font-size: 2.5rem;
    }

    .block {
        transform: translateY(-30%);
    }
</style>