<script>
export default {
  data() {
    return {
      message: 'Hello World!',
      counter: {
        count: 1
      },
      titleClass: 'title',
      text: ''
    }
  },
  methods: {
    increment() {
      this.counter.count++
    }
  } 
}
</script>

<template>  
  <h1>{{message.split('').reverse().join('')}}</h1>
  <h1> {{counter.count}} </h1>
  <h1 :class="titleClass"> Red </h1> 
  <button @click="increment">Count++</button>

  <input v-model="text" />
  <p> {{text}} </p>
</template>

<style>
.title {
  color: red;
}
</style>