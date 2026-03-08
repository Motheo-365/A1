<!-- Weather.vue -->
<script setup>
    import { ref, onMounted, computed } from 'vue'

    const weather = ref(null)
    const airQuality = ref(null)

    const weatherAPI =
    "https://api.open-meteo.com/v1/forecast?latitude=-25.7479&longitude=28.2293&daily=temperature_2m_max,temperature_2m_min,sunrise,sunset,uv_index_max&hourly=uv_index,is_day,sunshine_duration,rain,cloud_cover&current=temperature_2m,relative_humidity_2m,showers,is_day,rain,weather_code&timezone=auto"

    const airQualityAPI =
    "https://air-quality-api.open-meteo.com/v1/air-quality?latitude=-25.7479&longitude=28.2293&hourly=pm10,pm2_5,us_aqi"

    async function getWeather() {
        try {
            const res = await fetch(weatherAPI)
            const data = await res.json()
            if (!res.ok) throw new Error("Weather API error")
            weather.value = data
        } 
        
        catch (err) {
            console.error(err)
        }
    }

    async function getAirQuality() {
        try {
            const res = await fetch(airQualityAPI)
            const data = await res.json()
            if (!res.ok) throw new Error("Air Quality API error")
            airQuality.value = data
        } 
        
        catch (err) {
            console.error(err)
        }
    }

    onMounted(() => {
        getWeather()
        getAirQuality()
    })

    const isDay = computed(() => weather.value?.current?.is_day === 1)

    const latestAQI = computed(() => {
        if (!airQuality.value?.hourly) return null
        const lastIndex = airQuality.value.hourly.pm2_5.length - 1
        return {
            pm2_5: airQuality.value.hourly.pm2_5[lastIndex],
            pm10: airQuality.value.hourly.pm10[lastIndex],
            us_aqi: airQuality.value.hourly.us_aqi[lastIndex]
        }
    })

    const aqiStatus = computed(() => {
        if (!latestAQI.value) return ''
        const aqi = latestAQI.value.us_aqi
        if (aqi <= 50) return 'Good'
        if (aqi <= 100) return 'Moderate'
        if (aqi <= 150) return 'Unhealthy for sensitive groups'
        if (aqi <= 200) return 'Unhealthy'
        if (aqi <= 300) return 'Very Unhealthy'
        return 'Hazardous'
    })

    function formatTime(dateStr) {
        if (!dateStr) return ''
        return new Date(dateStr).toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })
    }

    const bgGradient = computed(() => {
        if (!weather.value) return 'linear-gradient(180deg, #4c6ef5, #1b1b3a)'
        
        const sunrise = new Date(weather.value.daily.sunrise[0])
        const sunset = new Date(weather.value.daily.sunset[0])
        const now = new Date()

        let topColor = '#4c6ef5'
        let bottomColor = '#1b1b3a'

        if (now >= sunrise && now <= sunset) {
            topColor = '#ffd166'
            bottomColor = '#06d6a0'
        } else {
            topColor = '#1b1b3a'
            bottomColor = '#3a0ca3'
        }

        if (latestAQI.value?.us_aqi >= 150) {
            topColor = '#ff6b6b'
            bottomColor = '#d90429'
        }

        return `linear-gradient(180deg, ${topColor}, ${bottomColor})`
    })
</script>

<!-- Weather.vue (only the template section shown) -->
<template>
    <h2>Current Weather in {{ weather?.timezone }}</h2>
    <section v-if="weather" class="hero" :style="{ background: bgGradient }">
        <div class="overlay">
            <div class="content">
                <!-- LEFT COLUMN: Weather -->
                <div class="weather-col">
                    <p>
                        {{ isDay
                        ? 'Sunset: ' + formatTime(weather?.daily?.sunset?.[0])
                        : 'Sunrise: ' + formatTime(weather?.daily?.sunrise?.[0])
                        }}
                    </p>
                    
                    <div class="weather-block">
                        <img :src="isDay ? '/media/sunny.gif' : '/media/night.gif'" alt="Sun animation">
                        <p>Temperature: {{ weather?.current?.temperature_2m }}ºC</p>
                        <p>Rain: {{ weather?.current?.rain }}mm</p>
                        <p>Humidity: {{ weather?.current?.relative_humidity_2m }}%</p>
                    </div>
                </div>

                <!-- RIGHT COLUMN: Air Quality -->
                <div v-if="latestAQI" class="air-quality-block">
                    <h3>Air Quality: {{ aqiStatus }}</h3>
                        <p>US AQI: {{ latestAQI.us_aqi }} </p>
                        <img src = '/media/elements.gif' alt = "Animation of the four elements" >
                        <p>PM2.5: {{ latestAQI.pm2_5 }} µg/m³ (fine particles)</p>
                        <p>PM10: {{ latestAQI.pm10 }} µg/m³ (dust & coarse particles)</p>
                </div>
            </div>
        </div>
  </section>

  <p v-else class="loading-text">Loading weather & air quality...</p>
</template>

<style scoped>
    .hero {
        position: relative;
        width: 100%;
        min-height: 60vh;
        border-radius: 16px;
        overflow: visible;
        transition: background 1s ease;
        padding-bottom: 2rem;
    }

    .overlay {
        position: relative;
        inset: auto;
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: flex-start;
        padding: 2rem;

        font-size: 1.2rem;
    }

    .content {
        color: #fff;
        max-width: 95%;
        width: 100%;

        display: grid;
        grid-template-columns: 1.4fr 1fr;
        gap: 2rem 2.5rem;
        align-items: start;
    }

    .weather-col {
        display: grid;
        align-content: start;
        gap: 0.75rem;
    }

    h2 {
        font-size: 3rem;
        margin-bottom: 1rem;
    }

    h3 {
        font-size: 1.4rem;
    }

    .weather-block p,
    .air-quality-block p {
        margin: 0.25rem 0;
    }

    .air-quality-block,
    .weather-col {
        background-color: rgba(0,0,0,0.6);
        border-radius: 12px;
        padding: 1rem 1.5rem;
        max-width: 75%;
        text-align: center;
        box-shadow: 0 4px 12px rgba(0,0,0,0.3);
    }

    .air-quality-block h3 {
        margin-bottom: 0.5rem;
    }

    .loading-text {
        text-align: center;
        margin-top: 2rem;
        font-size: 1.25rem;
        color: #555;
    }
</style>