<template>
  <div id="app">
   <!-- {{msg}} -->
   <Header />
   <AddTodo v-on:add-todo="addTodo"/>
   <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Header from './components/layout/Header';
import Todos from './components/Todos';
import AddTodo from './components/AddTodo';
import axios from 'axios'
export default {
  name: 'App',
  components:{
Todos,
Header,
AddTodo
  },
  data(){
    return{
     // msg:'Hello'
     todos:[
    //    {
    //  id:1,
    //  title:"Todo one",
    //  completed:false
    //  },
    //  {
    //  id:2,
    //  title:"Todo Two",
    //  completed:true
    //  },
    //  {
    //  id:3,
    //  title:"Todo Three",
    //  completed:false
    //  },
     ]
     }
    },
  
  methods:{
    deleteTodo(id) {
      this.todos=this.todos.filter(todo => todo.id !== id);
    },
    addTodo(newTodo){
      this.todos=[...this.todos,newTodo];
      const{title,completed}=newTodo;
      // axios.post('https://jsonplaceholder.typicode.com/todos',
      // {
      //   title,completed
      //   })
      // .then(res => this.todos=[...this.todos, res.data])
      // .catch(err => console.log(err));
     
    }
  },
  created(){
  axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
  .then(res => this.todos=res.data)
    .catch(err => console.log(err));
  
  }
}
</script>

<style>
*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
 body{
   font-family: Arial, Helvetica, sans-serif;
   line-height: 1.4;
 }
.btn{
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
