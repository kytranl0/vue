<script>
import ChildComp from './components/ChildComp.vue'
let id = 0;
export default {
    data() {
        return {
            counter: {
                count: 1
            },
            titleClass: "title",
            text: "",
            switch: false,
            newToDo: "",
            todos: [
                { id: id++, text: "Learn HTML", done: false },
                { id: id++, text: "Learn JavaScript", done: false },
                { id: id++, text: "Learn Vue", done: false }
            ],
            hideCompleted: false,
            todoId: 1,
            todoData: null,
            greeting: 'Greeting from parent class',
            childMsg: 'No child messages yet'
        };
    },
    methods: {
        increment() {
            this.counter.count++;
        },
        toggle() {
            if (this.switch) {
                this.switch = false;
            }
            else {
                this.switch = true;
            }
        },
        addToDo() {
            this.todos.push({ id: id++, text: this.newToDo, done: false });
            this.newToDo = "";
        },
        removeToDo(e) {
            this.todos = this.todos.filter((t) => t != e);
        },
        async fetchData() {
            this.todoData = null;
            const res = await fetch(`https://jsonplaceholder.typicode.com/todos/${this.todoId}`);
            this.todoData = await res.json();
        }
    },
    computed: {
        filteredTodos() {
            if (this.hideCompleted) {
                return this.todos.filter((t) => !t.done);
            }
            else {
                return this.todos;
            }
        }
    },
    mounted() {
        this.$refs.p.textContent = "Template reference after mounted event";
        this.fetchData();
    },
    watch: {
        todoId(id) {
            this.fetchData();
        }
    },
    components: {
        ChildComp
    }
}
</script>

<template>  
  <br/>
  <button @click="increment">Count++</button>
  <h1> {{counter.count}} </h1>
  <br/>
  <input v-model="text" />
  <p> {{text}} </p>
  <br/>
  <br/>
  <button @click="toggle">Toggle</button>
  <h1 v-if="switch">Vue</h1>
  <h1 v-else>No</h1>

  <br/>
  <br/>
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
    <br/>
      <br/>
  <button @click="hideCompleted = !hideCompleted"> 
  {{hideCompleted ? 'Show all': 'Hide all'}}
  </button>

  <p ref="p">Template ref before mount</p>
  <br/>
  <br/>
  <p>Todo id: {{todoId}}</p>
  <button @click="todoId++">Fetch next Todo</button>
  <p v-if="!todoData">Loading...</p>
  <pre v-else>{{todoData}}</pre>
  <br />
  <ChildComp :msg="greeting" @response="(msg) => childMsg = msg">Message: {{ childMsg }}</ChildComp>
  <p> {{ childMsg }} </p>
</template>

<style>
.title {
  color: red;
}
.done {
  text-decoration: line-through;
}
</style>