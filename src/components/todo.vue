
<script>
import New from './newTask.vue'

export default {
  data () {
    return {
      newTask: false,
      tasks: []
    }
  },
  components: {
    New
  },
  methods: {
    loadData: function () {
      if (JSON.parse(window.localStorage.getItem('tasks')) != null) {
        this.tasks = JSON.parse(window.localStorage.getItem('tasks'))
      }
    },
    taskClose: function () {
      this.newTask = !this.newTask
      this.loadData()
    }
  },
  created: function () {
    this.loadData()
  }

}
</script>
<template>
  <div >
    <New v-on:newTask_close='taskClose' v-if="newTask"></New>
    <div class="todoContent" >
      <div class="topContent">
        <h1 class="title">Tasks</h1>
      </div>

      <div class="new">
        <div class="play">
          <i class="fa fa-play fa-2x" aria-hidden="true"></i>
        </div>
        <div class="add" @click="newTask = !newTask" >
          <i class="fa fa-plus fa-2x" aria-hidden="true"></i>
        </div>
      </div>

      <div class="todoItem" v-for="task in tasks.items">
        <div class="descItem">
          <h1>{{task.title}}</h1>
          <h2>{{task.desc}}</h2>
          <div class="tags">
            <span>{{task.clocks}} Ciclos</span>
          </div>
        </div>
        <div class="delete">
          <i class="fa fa-trash fa-2x" aria-hidden="true">
        </div>
      </div>

    </div>
  </div>

</template>

<style>
.delete {
  background: #d91e18;
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding: 2rem;
  border-radius: 5px;
  color: #fff;
  cursor: pointer;
  transition: all .3s ease;
}
.delete:hover {
  background: #FF7470;
}
.topContent {
  display: flex;
  justify-content: space-around;
  align-items: center;
  flex-direction: row;
  width: 100%;
}
.title {
  font-family: 'Oswald', sans-serif;
  font-size: 30px;
}

.todoContent {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.todoItem {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  border: 1px solid #cecece;
  border-radius: 5px;
  width: 45%;
  margin: 5px;
  background: #fff;
  box-shadow: 0 2px 2px 0 rgba(0,0,0,0.14), 0 1px 5px 0 rgba(0,0,0,0.12), 0 3px 1px -2px rgba(0,0,0,0.2);
}
.new {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  border-radius: 5px;
  width: 45%;
  margin: 5px;
  background: #A0A0A0;
  color: #fff;
  cursor: pointer;
  border: none;
}
.play {
  width: 50%;
  background: #19b5fe;
  text-align: center;
  padding: 1rem;
  transition: all .3s ease;

}
.play:hover {
  background: #73CFFC
}
.add {
  width: 50%;
  background: #00b16a;
  text-align: center;
  padding: 1rem;
  transition: all .3s ease;
}
.add:hover {
  background: #4DC595;
}
.todoItem h1{
  font-family: 'Oswald', sans-serif;
  font-size: 20px;
  margin: 5px;
}
.todoItem h2 {
  font-family: 'Roboto', sans-serif;
  font-size: 15px;
  font-weight: lighter;
  margin: 5px;
  margin-top: 10px;
  margin: 10px 0 15px 5px;
}
.tags span {
  font-family: 'Roboto', sans-serif;
  font-size: 12px;
  border: 1px solid #19b5fe;
  border-radius: 3px;
  padding: 3px;
  color: #19b5fe;
  cursor: pointer;
  margin-left: 7px;
}
.descItem {
  padding: 10px;
}

@media screen and (max-width: 900px) {

  .todoItem {
    width: 100%
  }
  .new {
    width: 100%;
  }
}
</style>
