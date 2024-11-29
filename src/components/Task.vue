<template>
    <div class="container">
        <div class="task">
            <!--title-->
            <div class="title">
                <h1>To Do List</h1>
            </div>

            <!--form-->
            <!--keyup is used to add the new task in the to do list on hitting the enter button-->
            <div class="form">
                <input type = "text"
                placeholder=" Add New Task"
                v-model="newTask"
                @keyup.enter="addTask"/>
                <button @click="addTask"><i class="fas fa-plus">+</i></button>
            </div>

            <!--task lists-->
            <div class="taskItems">
                <!--emit used to pass the data form the child to parent-->
                <ul>
                    <task-item :task="task"
                    v-for="(task,index) in tasks"
                    :key="task.id"
                    @remove = "removeTask(index)" 
                    @complete="completeTask(task)"></task-item>
                </ul>
            </div>

            <!--buttons-->
            <div class="clearBtns">
                <button @click="clearCompleted">Clear Completed</button>
                <button @click="clearAll">Clear all</button>
            </div>

            <!--pending task-->
            <div class="pendingTasks">
                <span>Pending Tasks: {{ incomplete }}</span>
            </div>
        </div>
    </div>
</template>

<script>
import TaskItem from './TaskItem.vue';
    export default {
        name:"Task",
        props:['tasks'],
        data(){
            return{
                newTask:"",
            }
        },
        components:{
            TaskItem,
        },
        computed:{
            incomplete(){
                return this.tasks.filter(this.inProgress).length;
            }
        },
        methods:{
            addTask(){      
                if (this.newTask){
                    this.tasks.push({
                        title:this.newTask,
                        completed: false
                    });
                    this.newTask=" ";
                }
            },

            inProgress(task){
                return !this.isCompleted(task);
            },

            isCompleted(task){
                return task.completed;
            },

            clearCompleted() {
                this.tasks = this.tasks.filter(this.inProgress);
            },

            clearAll(){
                this.tasks = [];
            },

            completeTask(task){
                task.completed = !task.completed;
            },

            removeTask(index){
                this.tasks.splice(index,1)
            }
        }
    }
</script>

<style>
.container{
    max-width: 800px;
    margin:0 auto;
    padding:10px;
}

input[type="text"]{
    width:100%;
    height:15px;
    padding:20px;
    background:#ffffff;
    color:#000000;
    border:1px solid black;
    border-radius: 10px;
}

button{
    cursor: pointer;
    color:black;
}

h1{
    font-size: 25px;
    text-align: center ;
    text-decoration: underline;
    font-size: medium;
}

ul{
    list-style:none;
    margin:0;
    padding:15px;
}

.task{
    background:black;
    color:white;
    border-radius:10px;
    padding: 20px;
    box-shadow: 0px 0px 20px 20px rgba(96, 126, 134, 0.473);
    position:fixed;
    width: 300px;
    top:5px;
    bottom: 5px;
    margin: 0 0 0 320px;
}

.title{
    text-align: center;
    margin:0 0 10px
}

.form{
    position: relative;
    margin:0 0 20px;
}

.form button{
    background:none;
    border:none;
    color:rgb(11, 148, 234);
    position: absolute;
    top: 50%;
    right:20px;
    transform: translateY(-50%);
}

.form button:hover{
    color:darkblue;
}

.clearBtns{
    display:flex;
    justify-content:space-between;
    margin:0px 0 20px;
}

.clearBtns button{
    width:100%;
    background:blue;
    color: black;
    border-radius: 5px;
    padding:5px;
    margin: 0 35px;
}

.clearBtns button:hover{
    background: darkblue;
    color:white
}

.pendingTasks{
    padding:0 4px;
}

.taskItems{
    padding:5px;
    /* background: rgb(70, 114, 106); */
    /* border-radius: 10px; */
}

.taskItems li{
    display:flex;
    justify-content: space-between;
    margin:0 0 18px;
}

.taskItems button{
    background:none;
    border: none;
    color:white;
}

.taskItems button:hover{
    color: blue;
}

.taskItems .toggle i{
    margin:0 10px 0 0;
    font-size: 12px;
}

.taskItems .toggle.toggle-completed{
    text-decoration: line-through;
}
</style>