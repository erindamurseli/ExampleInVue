<template>
   
        <div class="d-flex align-items-center justify-content-between">
            <input type="checkbox" v-model="task.completed"/>
     <span v-bind:class="{completed: task.completed==true}">{{task.title}}</span> 
     <button v-on:click="$emit('delete-task',task.id)" class="btn btn-danger">x</button>
    </div>
</template>

<script>
export default{
    name:"Task",
    props:["task"],
    methods:{
    
    }
}

</script>

<style scoped>
 .completed{
   text-decoration: line-through;
 }

</style>

