<template>
  <div id="app">
    <Header></Header>
    <AddTodo v-on:add-todo='addTodo'></AddTodo>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Todos from "./components/Todos.vue";
import AddTodo from "./components/AddTodo.vue";
import Header from './components/layouts/Header'
import axios from 'axios';
export default {
  name: "app",
  components: {
    Header,
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: [
      ]
    };
  },
  methods:{
    deleteTodo(e){
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${e}`)
      .then(()=>this.todos = this.todos.filter(todo=>todo.id !== e))
      .catch()
      this.todos = this.todos.filter(todo=>todo.id !== e);
    },
    addTodo(newTodo){
      const {title:title,completed:completed} = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos',{title,completed})
      .then(res=>this.todos=[...this.todos,res.data]).catch()
    }
  },
  created(){
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
    .then(res=>this.todos = res.data)
    .catch();
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.btn{
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn-hover{
  background: #666;
}
</style>
