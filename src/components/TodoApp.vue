<template>
  <div class="container">
  <h2 class="text-center mt-5">My Vue Todo App</h2>
<!-- Input   -->
<div class="d-flex">
  <input type="text" 
   v-model="task"
   placeholder="Enter text"
   class="form-control">
   <button @click="submitTask" 
   class="btn btn-warning rounded-0">SUBMIT</button>
</div>
<!-- Task table -->
<table class="table">
  <thead>
      <tr>
   <th scope="col">Task</th>
   <th scope="col">Status</th>
   <th scope="col" class="text-center">#</th>
   <th scope="col" class="text-center">#</th>
      </tr>
  </thead>
  <tbody>
   
      <tr v-for="(task,index) in tasks" :key="index">
      <td scope="col">
          <span :class="finished">{{task.name}}</span>
          </td>
      <td style="width:120px" scope="col">
          <span class="pointer" @click="changeStatus(index)" >
              {{task.status.toString().charAt(0).toUpperCase()+task.status.toString().slice(1)}}
              
              </span>
          </td>
      

    
      <td>
        <div class="text-center" @click="editTask(index)">
          <span class="fa fa-pen"></span>

        </div>
        <div class="text-center" @click="deleteTask(index)">
           <span class="fa fa-trash"></span>
        </div>

      </td>
      </tr>
  </tbody>
</table>

  </div>
</template>

<script>
export default {
   name:'ToDoApp',
   props:{
       msg:String
   },
   data(){
       return {
           task:'',
           editedTask:null,
           availableStatuses:['to-do', 'in-progress', 'finished'],
           tasks:[
               {
                   name:'Steal bananas from the store',
                   status:'to-do'
               },
               {
                   name:'Eat 1 kg chocolate in one hour',
                   status:'in-progress'
               }
           ]
       }
   }, 
   created(){
     
   },
   computed:{
  
   
 
   },
   methods:{
       submitTask(){
           if(this.task.length === 0) return;
          if(this.editedTask === null){
           this.tasks.push({
               name:this.task,
               status:'to-do'
           })
          }
          else{
              this.tasks[this.editedTask].name = this.task;
          }
           this.task='';
       }, 
       deleteTask(index){
           this.tasks.splice(index,1);
       },
       editTask(index){
           this.task= this.tasks[index].name;
           this.editedTask= index;
       },
       changeStatus(index){
         let newIndex =  this.availableStatuses.indexOf(this.tasks[index]);
         if(++newIndex > 2) newIndex = 0;
         this.tasks[index].status = this.availableStatuses[newIndex];
       },
      
   }
}
</script>

<style scoped>
.pointer{
    cursor:pointer
}
.finished{
    text-decoration: line-through;
}
</style>