<template>
    <div>
        <h3>Weather</h3>
        <!-- listen for the weather data from $emit in LocationPicker & trigger updateWeather-->
        <div>
            <!-- display the weather and icon -->
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            weather: {
                // temp
                // icon
            }
        }
    },
    methods: {
        //takes the weather as a parameter
        updateWeather(weather) {
            // update the weather object
        }
    }
}
</script>

<style>

</style>
