<template>
  <q-page v-touch-pan.vertical.prevent.mouse="handlePan" v-touch-pan.horizontal.prevent.mouse="handlePan2" class="flex flex-center text-white">

    <div class="row">
        <q-input 
          v-model="data.name"
          input-class="text-center text-h5 text-white"
          color="teal"
          placeholder="Counter"
          filled 
          />
      </div>
    <div class="row full-width items-center">
      <div class="row full-width items-center">
        <div class="col text-center">
          <q-btn 
            @click="decreaseCounter"
            v-touch-repeat:300:300:300:300:50.mouse="decreaseCounter"
            icon="remove" 
            size="xl"
            round 
          />
        </div>

        <div class="col text-center text-h2">
          {{ data.counter }}
        </div>

        <div class="col text-center">
          <q-btn
            @click="increaseCounter"
            v-touch-repeat:300:300:300:300:50.mouse="increaseCounter"
            icon="add" 
            size="xl"
            round 
          />
        </div>
      </div>

    </div>
    <div class="row">
        <q-btn
          @click="resetCounter" 
          icon="restart_alt" 
          size="xl"
          round 
        />
      </div>
  </q-page>
</template>

<style scoped>
.q-page {
  max-width: 700px;
  margin: 0 auto;
}
</style>

<script setup>
import { reactive, watch } from 'vue';
import { useQuasar } from 'quasar';

const $q = useQuasar();

/*
  Reactive data
*/
const data = reactive({
  counter: 0,
  name: ''
});

/*
  Load data from localStorage
*/
const savedData = $q.localStorage.getItem('data');
if (savedData) Object.assign(data, savedData);

watch(data, value => {
  $q.localStorage.set('data', value);
});

/*
  Counter methods
*/
const increaseCounter = () => {
  data.counter++;
};

const decreaseCounter = () => {
  if (data.counter > 0) data.counter--;
};

const resetCounter = () => {
  data.counter = 0;
};

/*
  Handle touch-pan
*/
const handlePan = (e) => {
  if (e.delta.y< 0) increaseCounter();
  else decreaseCounter();
};

const handlePan2 = (e) => {
  if (e.delta.x< 0) decreaseCounter();
  else increaseCounter();
};
</script>
