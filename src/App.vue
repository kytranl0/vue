<script>
export default {
  data() {
    return {
      message: 'Hello World!',
      counter: {
        count: 1
      },
      titleClass: 'title'
    }
  },
  methods: {
    increment() {
      this.counter.count++
    },
    onInput(e) {
      this.text = e.target.value
      console.log(this.text)
    }
  } 
}
</script>

<template>  
  <h1>{{message.split('').reverse().join('')}}</h1>
  <h1> {{counter.count}} </h1>
  <h1 :class="titleClass"> Red </h1> 
  <button @click="increment">Count++</button>

  <input :value="text" @input="onInput" />
</template>

<style>
.title {
  color: red;
}
</style>