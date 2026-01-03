<script setup>
import { computed, inject } from 'vue';
import IconLocation from '../icons/IconLocation.vue';
import { cityProvide } from '../constants';

    const {dayData, dataObject} = defineProps({
        dayData: Object,
        data: Object
    })

    const city = inject(cityProvide)

    const weekday = computed(() => {
        return  new Date(dayData.date).toLocaleDateString("ru-RU", {weekday: "long"})
    })

    const day = computed(() => {
        return new Date(dayData.date).toLocaleDateString("ru-RU", {day: "numeric", month: "long", year:"numeric"})
    })
</script>

<template>
    <div class="panelLeft">
        <div class="panelLeft__data">
            <div class="panelLeft__weekday">{{ weekday}}</div>
            <div class="panelLeft__day">{{ day}}</div>
            <div class="panelLeft__city">
                <IconLocation/>
                <div>{{ city}}</div>
            </div>
        </div>
        <!-- {{ data.forecast.forecastday[] }} -->
        <!-- <img src="data.forecast.forecastday.day.condition.icon" alt="" > -->
        <div class="panelLeft__info">
            <img :src="dayData.day.condition.icon" alt="">
            <div class="panelLeft__temp">{{ dayData.day.avgtemp_c }}°C</div>
            <div class="panelLeft__text">{{ dayData.day.condition.text}}</div>
        </div>

    
    </div>
</template>

<style scoped>
    .panelLeft{
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        height: 100%;
        font-family: var(--font);
    }
    .panelLeft__weekday{
        font-weight: 700;
        font-size: 37px;
        color: #fff;
        text-transform: capitalize;
        margin-bottom: 16px;
    }

    .panelLeft__day{
   
    font-weight: 500;
    font-size: 22px;
    color: #fff;
    margin-bottom: 13px;
    }

    .panelLeft__city{
        display: flex;
        align-items: center;
        column-gap: 8px;
        font-weight: 600;
        font-size: 20px;
        color: #fff;
    }

    .panelLeft__info img{
        width: 95px;
        height: 95px;
        object-fit: cover;
        margin-bottom: 9px;
    }

    .panelLeft__temp {
    font-weight: 700;
    font-size: 50px;
    color: #fff;
    margin-bottom: 13px;

}
    .panelLeft__text {
        
    font-weight: 700;
    font-size: 30px;
    color: #fff;
    }
</style>