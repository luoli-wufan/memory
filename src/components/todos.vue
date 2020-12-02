<template>
    <div>
        <div v-for='(todo,index) in todos' :key='index'>
           <todoItem :todo='todo' @del="$emit('handledel',todo.id)"/>
         </div>
    </div>
</template>

<script>
import todoItem from "../components/todoItem.vue"
export default {
    name:'Todos',
   props: ["todos"],
   components:{
       todoItem
   },
   methods:{
    //    del(id){
    //        console.log(id);
    //    }
   }
}
</script>

<style scoped>

</style>