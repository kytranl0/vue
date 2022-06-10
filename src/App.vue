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
        { id: id++, text: 'Learn HTML', done: false},
        { id: id++, text: 'Learn JavaScript', done: false },
        { id: id++, text: 'Learn Vue', done: false }
      ],
      hideCompleted: false
      
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
      this.todos.push({id: id++, text: this.newToDo, done: false});
      this.newToDo = '';
    },
    removeToDo(e) {
      this.todos = this.todos.filter((t) => t!=e)
    }
  },
  computed: {
    filteredTodos() {
      if (this.hideCompleted) {
        return this.todos.filter((t) => !t.done )
      } else {
        return this.todos
      }
    }
  },
  mounted() {
      this.$refs.p.textContent = "template ref after mount";
  }
  
}
</script>

<template>  
  <h1 :class="titleClass">{{message.split('').reverse().join('')}}</h1>
  <button @click="increment">Count++</button>
  <h1> {{counter.count}} </h1>

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
    <li v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done">
      <span :class="{done: todo.done}"> {{todo.text}} </span>
      <button @click="removeToDo(todo)">X</button>
    </li>
  </ul> 
  <button @click="hideCompleted = !hideCompleted"> 
  {{hideCompleted ? 'Show all': 'Hide all completed'}}
  </button>

  <p ref="p">template ref before mount</p>

</template>

<style>
.title {
  color: red;
}
.done {
  text-decoration: line-through;
}
</style>