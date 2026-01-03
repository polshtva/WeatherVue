<script setup>
import { computed } from 'vue';
import CitySelect from './CitySelect.vue';
import DayCard from './DayCard.vue';
import Error from './Error.vue';
import Stat from './Stat.vue';
import { errorMap } from '../constants';


  const {data, error, activeIndex} = defineProps({
    data: Object,
    error: Object,
    activeIndex: Number
  })

  // console.log(data);

  const emit = defineEmits(['select-index', 'select-city'])

 

  const errorDisplay = computed(() => {
    return errorMap.get(error.error?.code)
  })
  
  const statModified = computed(() => {
    if(!data) return
    return [
      {
        label: 'Влажность',
        stat:  data.forecast.forecastday[activeIndex].day.avghumidity + " %"
      },
      {
        label: 'Вероятность дождя',
        stat:  data.forecast.forecastday[activeIndex].day.daily_chance_of_rain + " %"
      },
       {
        label: 'Ветер',
        stat:  data.forecast.forecastday[activeIndex].day.maxwind_kph + " км/ч"
      },
    ] 
  })


</script>

<template>
      <Error v-if="error" :error="errorDisplay"/>
    
       <div v-if="data && data.current" class="stat-list">
        <div class="stats">
          <Stat v-for="item in statModified" v-bind="item" :key="item.label"></Stat>
        </div>
    
        <div class="day-card-list">
          <DayCard v-for="(item, i) in data.forecast.forecastday"
          :key="item.date"
          :weather-img="item.day.condition.icon"
           :temp="item.day.avgtemp_c"
           :date="new Date(item.date)"
           :is-active="activeIndex == i"
           @click="() => (emit('select-index', i))"/>
        </div>
    
      </div>
    
    <CitySelect /> 
</template>

<style scoped>

    .day-card-list{
      display: flex;
      column-gap: 10px;
    }

    .stat-list{
      display: flex;
      flex-direction: column;
      gap: 80px;
      margin-bottom: 70px;
    }
    .stats{
      display: flex;  
      flex-direction: column;
      row-gap: 16px;
    }
</style>