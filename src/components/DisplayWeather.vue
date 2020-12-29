<template>
    <div>
        <h3>WEATHER</h3>
        <div v-if="weather.temp" class="forecast-container">
            <p class="temp">{{ weather.temp }}°</p>
            <div v-if="iconPath" >
                <img class='weather-img' :src='iconPath' alt="">
            </div>
        </div>
        <p>{{ weather.shortForecast}}</p>
    </div>
</template>

<script>
export default {
    props: [ 'weather' ],
    data() {
        return {
            iconPath: '../assets/mostly_sunny.svg'
        }
    }, 
    updated() {
        let key = this.weather.shortForecast.split('')
        for(let i = 0; i <= key.length; i++) {
            if(key[i] === ' '){
                key[i] = '_'
            }
        }
        key = key.join('').toLowerCase()
        var iconPath ="../assets/" + key + ".svg"
        this.iconPath = iconPath
        console.log(iconPath)
    }
    
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
