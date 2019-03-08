<template>
  <div id="app">
    <!--<img src="./assets/logo.png">-->
    <div id="myApplication">
      <h1>{{ title }}</h1>
      <input id="inputAdd" v-model="currentTask" v-on:keyup.13="addTask">
      <h2>ToDo</h2>
      <ul id="task-list">
        <li v-for="task, index in tasks">
          <input type="checkbox" v-model="task.show">
          <span v-if="task.show">
            {{ task.title }}
          </span>
          <span v-else>
            <strike>{{ task.title }}</strike>
          </span>
          <button v-on:click="delTask(index)">X</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>

module.exports = {
  data(){
    return{
      title: "Groutch",
      currentTask: "",
      tasks: [
        {title: 'Tache 1', show:true },
        {title: 'Tache 2', show:true },
        {title: 'Tache 3', show:true },
        {title: 'Tache 4', show:true }
      ]
    }
  },
  methods: {
    addTask : function (event){
      if (this.currentTask!=""){
        this.tasks.push({title:this.currentTask, show:true});
        this.currentTask="";
      }
    },
    delTask : function (index){
      this.$delete(this.tasks, index)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  text-align: center;
}
ul{
  text-align:left;
}

</style>
