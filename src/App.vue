<template lang="pug">
 #app
  h1 {{name}}

  .container
   input(type="text" v-model="newTask.title")
   br
   br
   input(type="number",v-model="newTask.hour")
   br
   br

  button(@click="addTask") Add Task


  ul
   li(v-for="(t,i) in tasks") {{t.title}} {{t.hour}}
    button.remove-task(@click="removeTask(i)") X


</template>

<script>
export default {
  name: 'app',
  data () {
    return {
       key_storage : 'k-task',
       name :'task Jonathan',
       tasks:[],
       newTask : [
           {title:'',hour:''}
       ]
    }
  },
  created:function(){
     this.tasks = JSON.parse(localStorage.getItem(this.key_storage)) || [];
  },
  methods:{
     addTask(){
         this.tasks.push({
             title:this.newTask.title,
             hour :this.newTask.hour
         });

         //Save in local storage
         this.saveDataInLocalStorage();
     },

     saveDataInLocalStorage(){
         const data = JSON.stringify(this.tasks);
         localStorage.setItem(this.key_storage,data);
     },

     removeTask(index){
         this.tasks.splice(index,1);
         //Save in local storage
         this.saveDataInLocalStorage();
     }
  }

}
</script>

<style lang="scss">

</style>
