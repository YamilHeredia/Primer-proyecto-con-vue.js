<script setup>
  import {ref} from 'vue'
  import {computed} from 'vue'

  const name = "Hola Vue dinámico";
  
  let counter = ref(0);
  const arrayFavoritos = ref([])

  const increment = () => counter.value++;
  
  const decrement = () => counter.value--;
  
  const reset = () => (counter.value = 0);

  const bloquearBtnAdd = computed (() => {
    const numSearch = arrayFavoritos.value.find(num => num === counter.value);
    console.log(numSearch);
    if(numSearch === 0) return true; 
    return numSearch ? true : false;
    
  });

  const classCounter = computed(() => {
    if(counter.value === 0){
      return 'zero'
    }
    if(counter.value > 0){
      return 'positive'
    }
    if(counter.value < 0){
      return 'negative'
    }
    
  });

  const add = () => {
    arrayFavoritos.value.push(counter.value);
  }

</script>


<template>
  <div class="container text-center mt-3">
    <h1>Hola {{ name.toUpperCase() }}</h1>
    <h2 :class="classCounter">{{ counter }}</h2>
    <button @click="increment" class="btn btn-success">Increment</button>
    <button @click="decrement" class="btn btn-danger">Decrement</button>
    <button @click="reset" class="btn btn-secondary">Reset</button>
    <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary">Add</button>
    <br/>
    {{ arrayFavoritos }}
    <ul class="list-group">
      <li class="list-group-item"
      v-for="(num, index) in arrayFavoritos" :key="index">
        {{ num }}
      </li>
    </ul>

  </div>
  

</template>

<style>
  h1 {
    color: red;
    padding-right: 25px;
  }
  .positive {
    color: green;
  }
  .negative {
    color: red; 
  }
  .zero {
    color: peru;
  }
 
</style>