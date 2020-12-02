<template>
  <div id="app">
    <Header />
    <Addtodo @handleadd="handleadd"/>
    <Todos :todos="todos" @handledel="delaction"/>
  </div>
</template>

<script>
import Header from './components/layout/Header.vue';
import Todos from './components/todos.vue';
import Addtodo from './components/Addtodo.vue';
import axios from "axios"
  export default {
    name: "app",
    data(){
      return{
        todos:[
        ]
      }
    },
    components: {
      Todos,
      Header,
      Addtodo
    },
  
       methods: {
      delaction(id){
      //  console.log(id)
     // axios.delete("http://jsonplaceholder.typicode.com/todos/"+id)
     //es6语法
     axios.delete(`http://jsonplaceholder.typicode.com/todos/$(id)`)
     .then(res => {
        this.todos = this.todos.filter(todo => todo.id !==id)
     })
     .catch(err => console.log(err))
     
        },
        handleadd(newtodo){
          //this.todos.unshift(newtodo)
         const{title,completed} = newtodo;
         axios.post("http://jsonplaceholder.typicode.com/todos",{
           title,
           completed
         })
         .then(res => {
          this.todos = [res.data,...this.todos]
         })
         .catch(err => console.log(err))

          
        },
       
    },
     created(){
          //数据请求
          axios
          .get("http://jsonplaceholder.typicode.com/todos?_limit=3")
          .then(res => {
            // console.log(res.data))
            this.todos = res.data;
          })
         
          .catch(err => console.log(err))
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
  color:#fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover{
  background: #666;
}
</style>
