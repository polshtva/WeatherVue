<script setup>
    import Button from './Button.vue';
    import IconComponent from '../icons/IconLocation.vue';  
    import {ref, reactive, onMounted,onUpdated, watch, watchEffect, onWatcherCleanup, inject} from 'vue';
    import Input from './Input.vue';
import { cityProvide } from '../constants';


    // onUpdated(() => {
    //     console.log(city.value);
    // })
   
        
    const city = inject(cityProvide);
    // console.log(city.value);
    const inputVal = ref(city.value)



   let isEditer = ref(false);

//    watch(city, (newVal, oldVal) => {
//         console.log("Старое: " + oldVal);
//         console.log("Новое: " + newVal);
//         onWatcherCleanup(() => {
//             console.log("clinup")
//         })
//     })

    // watchEffect(()=> {
    //     console.log("Город: " + city.value);
    //     console.log("Флаг: " + isEditer.value);
    // })

   function select(){
    isEditer.value =false;
    // emit('selectCity', city.value)
    city.value = inputVal.value;
   }

    function edit(){
    isEditer.value =true;
   }




</script>

<template>
<div class="city-select">
        
    <div v-if="isEditer" class="city-input">
    <Input placeholder="Введите город" v-model="inputVal" @keyup.enter="select()" v-focus></Input>
   
    <Button @click="select()">Сохранить</Button>
    </div> 
   
    <Button v-else @click="edit()">
    <IconComponent/>
    Изменить город</Button>
</div>
</template>

<style scoped>
    .city-input{
        display: flex;
        gap: 12px;
    }

    .city-select{
        width: 480px;
    }

</style>