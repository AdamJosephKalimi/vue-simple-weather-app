<template>
    <div>
        <h3>WEATHER</h3>
        <div v-if="weather.temp" class="forecast-container">
            <p class="temp">{{ weather.temp }}°</p>
            <div>
                <!-- <img class='weather-img' :src="weather.iconPath" alt=""> -->
                <img class='weather-img' :src="weather.icon" alt="">
            </div>
        </div>
        <div class="weather-details">
            <p>{{ weather.detailedForecast}}</p>
        </div>
        
    </div>
</template>

<script>
export default {
    props: [ 'weather' ],
    // data() {
    //     return {
    //     }
    // }
}
</script>

<style>
    .forecast-container {
        width: 18%;
        margin: auto;
        display: flex;
        justify-content: space-around;
        align-items: center; 
    }
    .weather-img { 
        width: 70px;
        height: 70px;
        border-radius: 4px;
    }
    .temp {
        font-size: 60px; 
        font-weight: 800;   
        color: #2b2b2b;
        font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    }
    h3 {
        font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    }

</style>
