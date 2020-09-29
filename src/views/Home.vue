<template>
  <div id="app">
     <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Todos from '../components/Todos';
import AddTodo from '../components/AddTodo';
import axios from 'axios';
export default {
  name: 'Home',
  components: {
    Todos,
    AddTodo
  },
  data(){
    return {
      
      todos: []
    }
  },  

/*deleteTodo: function(todos,response, id) {
    axios.delete(`https://jsonplaceholder.typicode.com/todos/` +id)
    .then(response => {
this.todos.splice(id, 1)
console.log(this.todos);
        console.log(response);

})
        },
        
         deleteTodo:function(id) {
            axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
            .then(res => {
              this.todos = this.todos.filter(todo => todo.id !== id)
           
           })            
            
            .catch(err => {
              console.log(err)
            })
 
        },
        
        */
       
   methods: {
       deleteTodo: function(todos,response, id) {
        axios.delete(`https://jsonplaceholder.typicode.com/todos/` +id)
              .then(response => {
                this.todos.splice(id, 1)
                  console.log(this.todos);
                  console.log(response);

              })
        },

     addTodo(newTodo){
       const { title, completed } = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos', {
         title,
         completed
      })
      .then(res => this.todos = this.todos = [...this.todos, res.data])
      .catch(err => console.log(err))
      
     }
   },
   created() {
     axios.get('https://jsonplaceholder.typicode.com/todos?_limit=10')
     .then(res => this.todos = res .data)
    .catch(err => console.log(err)); 
   } 
}



</script>

<style>
* {
  box-sizing: border-box;
  margin: 0px;
  padding: 0px;
}

body{
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover{
  background: #666;
}
</style>
