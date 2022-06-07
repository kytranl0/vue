<script>
export default {
  data() {
    return {
      message: 'Hello World!',
      counter: {
        count: 1
      },
      titleClass: 'title',
      text: '',
      switch: false
    }
  },
  methods: {
    increment() {
      this.counter.count++
    }, 
    toggle() {
      if (this.switch) {
        this.switch = false;
      } else {
        this.switch = true;
      }
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
  <button @click="toggle">Toggle</button>
  <h1 v-if="switch">Vue</h1>
  <h1 v-else>No</h1>
</template>

<style>
.title {
  color: red;
}
</style>