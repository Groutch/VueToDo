<template>
  <div id="app">
    <!--<img src="./assets/logo.png">-->
    <div id="myApplication">
      <h1>{{ title }}</h1>
      <input id="inputAdd" v-model="currentTask" v-on:keyup.13="addTask">
      <button class="btn btn-success" v-on:click="addTask">+</button>
      <hr style="width:10%">
      <table id="task-list">
        <tr v-for="(task, index) in tasks" :key="index">
          <!--<td><input type="checkbox" v-model="task.show"></td>-->
          <td v-on:click="toggleTask(index)">
            <span v-if="task.show" >
              {{ task.title }}
            </span>
            <span v-else>
              <strike>{{ task.title }}</strike>
            </span>
          </td>
          <td><button class="btn btn-danger" v-on:click="delTask(index)">X</button></td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>

module.exports = {
  data(){
    return{
      title: "Groutch's ToDoList",
      currentTask: "",
      tasks: [
        {title: 'Tache 1', show:true },
        {title: 'Tache 2', show:true },
        {title: 'Tache 3', show:true },
        {title: 'Tache 4', show:true }
      ]
    }
  },
  mounted() {
    if (localStorage.tasks) {
      this.tasks = JSON.parse(localStorage.tasks);
    }
  },
  methods: {
    addTask : function (event){
      if (this.currentTask!=""){
        this.tasks.push({title:this.currentTask, show:true});
        this.currentTask="";
        this.saveToDo();
      }
    },
    delTask : function (index){
      this.$delete(this.tasks, index)
      this.saveToDo();
    },
    toggleTask : function (index){
      this.tasks[index].show = !this.tasks[index].show;
      this.saveToDo();
    },
    saveToDo : function(){
      data = JSON.stringify(this.tasks);
      localStorage.tasks=data;
    }
  }
}
</script>

<style lang="scss">
  @import './styles/custom-bootstrap.scss';
  @import '../node_modules/bootstrap/scss/bootstrap.scss';
</style>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  text-align: center;
}
table{
  margin: 0px auto;
}
span { cursor: pointer; }

</style>
