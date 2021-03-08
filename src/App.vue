<template>
  <div id="app">
<div class="container">
  <div class="row">
    <div class="col-6 offset-md-3">
    <AddNewTask v-on:add-new-task="addNewTask"/>
    <div class="card">
     <div class="card-body">
    <Tasks :tasks="openTask" v-on:delete-task="deleteTask" />
     </div>
    </div>
  
<input type="checkbox" v-model="showCompletedTask" id="show-completed-tasks">
 <label for="show-completed-task" class="pl-2">Show Completed Task</label> 
</div>
</div>
</div>
</div>
  
<!-- <button class="btn btn-primary"> I am a button</button> -->
  
</template>

<script>

import Tasks from "./components/Tasks.vue"
import AddNewTask from "./components/AddNewTask.vue"
import Axios from 'axios';

export default {
  name: 'App',
  components: {
   Tasks,
   AddNewTask
  },
  
  data(){
    return{
      tasks:[
       
    
      ],
      showCompletedTask :true
    }
  },
  methods:{
    deleteTask(id){
      this.tasks=this.tasks.filter(task =>task.id !==id);

    // },
    // fetch(`https://jsonplaceholder.typicode.com/todos/${id}`, {method: 'DELETE'})
    // .then()
Axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
.then(response => console.log(response.data))
.catch(e=>console.log(e));

    },
    
    addNewTask(task){
      this.tasks=[...this.tasks, task];
      localStorage.setItem('tasks',JSON.stringify(this.tasks));


    }
  
   } ,
  computed:{
  openTask(){
 return this.showCompletedTask ? this.tasks: this.tasks.filter(task => task.completed==false);  
  
  }
},

mounted(){
  // const ls_tasks=localStorage.getItem('tasks');
  // if(ls_tasks!==null)
  // this.tasks=JSON.parse(ls_tasks);
//   fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
//  .then(response=> response.json())
//  .then(data=> this.tasks=data)
//  .catch(e=>console.log(e));


Axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
.then(response => {
  console.log(response.data)
  this.tasks = response.data;
  })
.catch(e=>console.log(e));



}
}
// data(){
//   return{
//     title:'Hello'
//   }


// created(){
//   document.write(this.title);
// }

</script>

<style>

 
</style>
