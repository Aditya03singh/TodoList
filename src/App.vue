<script>
import Task from './components/Task.vue';
export default{
  name:"App",
  data(){
    return{
      tasks:[
        {
          id: 1,
          title:"Go to Gym",
          completed: true
        },

        {
          id: 2,
          title: "Fresh-up and Breakfast",
          completed: true
        },

        {
          id: 3,
          title: "Login in the Office ",
          completed: true
        },

        {
          id: 4,
          title: "Work",
          completed: false
        },

        {
          id: 5,
          title: "Logout",
          completed: false
        }
      ]
    }
  },
  components:{
    Task,
  },
}
</script>

<template>
  <div id = "app">
    <task :tasks="tasks"></task> <!--props to pass the tasks from parent to child-->
  </div>
</template>

<style>
  *{
    margin: 5px;
    padding: 0px;
    box-sizing: border-box;
  }

  body{
    background:white;
    color:black;
  }

  #app{
    width:100%;
    padding:60px 0px;
  }
</style>
