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
      todos: [
          {id: id++, text: 'Learn HTML'},
          {id: id++, text: 'Learn Javascript'},
          {id: id++, text: 'Learn Vue'}
      ],
      newToDo = ''
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
      this.todos.push({id: id++, text: 'Todo item'});
   
    },
    removeToDo(e) {
      // let t = this.todos.find(function findObj(d) {
      //   return d.id === e.id;
      // })
      for (let i = 0; i<this.todos.length; i++) {
        if (this.todos[i].id == e.id) {
          this.todos.splice(i,i+1);
        }
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
  <ul>
  <form @submit.prevent="addToDo">
    <input v-model="newToDo">
    <button>Add todo</button>
  </form>
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