<script>
let id = 0;
export default {
  data() {
    return {
      message: 'Hello World!',
      counter: {
        count: 1
      },
      titleClass: 'title',
      text: '',
      switch: false,
      newToDo: '',
      todos: [
        { id: id++, text: 'Learn HTML' },
        { id: id++, text: 'Learn JavaScript' },
        { id: id++, text: 'Learn Vue' }
      ]
      
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
    },
    addToDo() {
      this.todos.push({id: id++, text: this.newToDo});
      this.newToDo = '';
    },
    removeToDo(e) {
      this.todos = this.todos.filter((t) => t!=e)
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

  <form @submit.prevent="addToDo">
    <input v-model="newToDo">
    <button>Add todo</button>
  </form>

  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{todo.text}}
      <button @click="removeToDo(todo)">X</button>
    </li>
  </ul> 

</template>

<style>
.title {
  color: red;
}
</style>