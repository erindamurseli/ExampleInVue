<template>
    <div>
       
      <div v-for="t in tasks" :key="t.id">

          <Task v-bind:task="t" v-on:delete-task="$emit('delete-task',t.id)"/>  
     </div>
    </div>
</template>

<script >
 import Task from "./Task.vue";


export default {
    name:"Tasks",
    components:{
        Task
    },
    props:['tasks'],
    methods:{
        emit(){

        }
    }
}

</script>

<style scoped>

</style>
