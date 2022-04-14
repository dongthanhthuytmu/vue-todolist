<template>
    <div id="section">
        <div class="box-content">
            <img class="img-line" src="./assets/line.png" alt="">
            <p class="title">TO DO LIST</p>
            <p class="all-task"><i class="fa-solid fa-list-check"></i>  List Tasks <span v-if="isTask">({{isTask}})</span></p>
            <input v-model="task" placeholder="Add your new todo..." type="text"><br>
            <button @click="addTask()" class="btn-add">ADD</button>
            <div class="box-btn">
                <button @click="clearCompleted()" class="clear-complete"><i class="fa-solid fa-check-double"></i>  Clear Completed</button>
                <button @click="clearAll()" class="clear-all"><i class="fa-solid fa-delete-left"></i>  Clear All</button>
            </div>
            <table>
                <tr v-bind:key="item.id" v-for="item in tasks" class="list-task">
                    <td v-bind:class="{success : item.completed}" class="td-check"><input @click="completedTask(item)" type="checkbox"></td>
                    <td class="td-name"><p v-bind:class="{done : item.completed}" class="name-task">{{item.name}}</p></td>
                    <td class="td-remove"><a v-on:click.prevent="removeTask(item)" href="">X</a></td>
                </tr>
            </table>
        </div>
    </div>
</template>

<script>

export default {
    name: 'App',
    components: {
    
    },
    data() {
        return {
            tasks: [
                {
                    id: 1,
                    name: "Learn English",
                    completed: false
                },
                {
                    id: 2,
                    name: "Coding Time",
                    completed: false
                },
                {
                    id: 3,
                    name: "Reading Book",
                    completed: false
                },
            ],
            task: '',
        }
    },
    computed: {
        isTask() {
            return this.tasks.filter(this.existTask).length;
        }
    },
    methods: {
        addTask() {
            if(this.task) {
                 this.tasks.push({
                id: Math.floor(Math.random() * 900),
                name: this.task,
                completed: false,
            });
            this.task = "";
            }
        },
        completedTask(task) {
            task.completed = ! task.completed;
        },
        removeTask(task) {
          let newTask = this.tasks.filter(function(item) {
              return task.id !== item.id;
          });
          this.tasks = newTask;
        },
        clearCompleted() {
            let taskTodo = this.tasks.filter(this.existTask);
            this.tasks = taskTodo;
        },
        isCompleted(task) {
            return task.completed;
        },
        existTask(task) {
            return  !this.isCompleted(task);
        },
        clearAll() {
            this.tasks = [];
        }
    },
}
</script>

<style>
body {
    margin: 0 !important;
    font-family: 'Fredoka One', cursive;
}
.box-content {
    background-image: linear-gradient(to right, #83f8ca, #57edf3, #73dcff, #a7c8fe, #cab5e1);
    width: 40%;
    margin: 100px auto;
    height: 100%;
    box-shadow:
       inset 0 -3em 3em rgba(0,0,0,0.1),
             0 0  0 2px rgb(255,255,255),
             0.3em 0.3em 1em rgba(0,0,0,0.3);
    border-radius: 10px;
    text-align: center;
    padding-bottom: 30px;
}
.title {
    color: #052939;
    text-shadow: 3px 3px 0px #eb452b, 6px 6px 0px #efa032, 9px 9px 0px #46b59b, 12px 12px 0px #017e7f, 15px 15px 0px #052939, 18px 18px 0px #c11a2b;
   letter-spacing: 0px;
   font-size: 80px;
   text-align: center;
   margin: 20px;
}
.img-line {
    width: 80%;
    margin-top: -10px;
}
input[type=text] {
  width: 50%;
  border: 2px solid #052939;
  border-radius: 4px;
  font-size: 20px;
  padding: 12px 20px 12px 40px;
  transition: width 0.4s ease-in-out;
   font-family: 'Fredoka One', cursive;
}
input[type=text]:focus {
  width: 70%;
}
.btn-add {
    font-family: 'Fredoka One', cursive;
    background: rgb(247,150,192);
    background: radial-gradient(circle, rgba(247,150,192,1) 0%, rgba(118,174,241,1) 100%);
    padding: 0;
    border: none;
    color: #fff;
    padding: 10px 50px;
    border-radius: 20px;
    margin: 20px 0;
    font-size: 20px;
    cursor: pointer;
}
table {
    width: 80%;
    margin: 0 auto;
    line-height: 0;
}
.done {
    text-decoration: line-through;
}
.list-task {
    background-color: #fff;
}
.td-check {
    border-top-left-radius: 5px;
    border-bottom-left-radius: 5px;
    width: 40px;
}
.success {
    background-color: #0075FF;
}
.box-btn {
    margin: 10px 0;
}
.clear-complete {
    font-size: 16px;
    font-family: 'Fredoka One', cursive;
    margin-right: 20px;
    padding: 5px 10px;
    border: 1px solid #000;
    border-radius: 5px;
    background-color: #FFD43B;
    color: #183153;
    cursor: pointer;
}
.clear-complete:hover {
     background-color: #183153;
    color: #FFD43B;
}
.clear-all:hover {
    background-color: #FFD43B;
    color: #183153;
}
.clear-all {
    font-size: 16px;
    font-family: 'Fredoka One', cursive;
    margin-right: 20px;
    padding: 5px 10px;
    border: 1px solid #000;
    border-radius: 5px;
    background-color: #183153;
    color: #FFD43B;
    cursor: pointer;
}
.all-task {
    font-size: 20px;
}
</style>
