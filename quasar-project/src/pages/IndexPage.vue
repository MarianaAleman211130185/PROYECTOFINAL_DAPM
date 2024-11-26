<template>
  <q-page class="flex flex-center text-whith">
    <div class="row">
      <q-input 
      v-model="data.name"
      input-class="text-center text-h5 text-white"
      color="teal"
      filled 
      placeholder="Counter" />
    </div>
    <div class="row full-width items-center">
      <div class="col text-center">
        <q-btn 
        @click="decreaseCounter"
        round 
        icon="remove" 
        size="xl" />
      </div>
      <div class="col text-center text-h2">
        {{ data.counter }}
      </div>
      <div class="col text-center">
        <q-btn round 
        @click="increaseCounter"
        icon="add" 
        size="xl"
        />
      </div>
      <div class="row">
        <q-btn
        @click="resetCounter" 
        round 
        icon="restart_alt" 
        size="xl"
        />
      </div>
    </div>
  </q-page>
</template>
<style scoped>
.q-page{
  max-width: 700px;
  margin: 0;
}
</style>
<script setup>
  /*
    imports
  */

 import { reactive } from 'vue';

 /*
    data
 */

  const data= reactive ({
    counter: 0,
    name:''
  })

  /*
    counter methods
  */

  const increaseCounter =()=>{
    data.counter++
  }

  const decreaseCounter =()=>{
    if (data.counter>0)
      data.counter--
  }

  const resetCounter =()=>{
    data.counter=0
  }

</script>
