<template>
<div class="add">
      <form @submit.prevent="Addtodo">
          <input type="text" placeholder="请添加代办事项" v-model="title">
          <input type="submit" value="添加" class="btn">
      </form>
</div>
  
</template>

<script>
import uuid from "uuid";
export default {
  name: 'Addtodo',
  data(){
      return{
          title: ''
      }
  },
  methods:{
    Addtodo(){
       //console.log(this.title) 
       const newtodo={
           id: uuid.v4(),
           title: this.title,
           completed: false
       };
       //注册事件
       this.$emit("handleadd",newtodo);
       this.title= "";
    }
  }
}
</script>
import uuid from 'uuid';
<style scoped>
form{
    display: flex;
}
input[type="text"]{
    flex: 10;
    padding: 5px;
}
input[type="submit"]{
    flex: 2;
}
</style>
