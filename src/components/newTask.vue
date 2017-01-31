<script>
export default {
  data () {
    return {
      clocks: 0,
      title: '',
      desc: '',
      task: null
    }
  },
  methods: {
    close: function () {
      this.$emit('newTask_close', this.newTask)
    },
    save: function () {
      if (JSON.parse(window.localStorage.getItem('tasks')) === null) {
        let tasks = {
          items: []
        }
        window.localStorage.setItem('tasks', JSON.stringify(tasks))
      }

      let task = {
        'title': this.title,
        'desc': this.desc,
        'clocks': this.clocks
      }

      let tasks = JSON.parse(window.localStorage.getItem('tasks'))
      tasks.items.push(task)
      window.localStorage.setItem('tasks', JSON.stringify(tasks))
      this.close()
    }
  }
}
</script>
<template>
  <div class="newTaskContent">
    <div class="newTaskBox">
      <div class="content">

        <div class="inputRow">
          <label>Titulo</label>
          <input type="text" v-model="title"></input>
        </div>
        <div class="inputRow">
          <label>Descrição</label>
          <input type="text" v-model="desc"></input>
        </div>
        <div class="inputRow center">
          <label class="space">Pomodoros</label>
          <div class="space">
            <span class="button" v-on:click="clocks -= 1">-</span> <span class="button">{{clocks}}x</span> <span class="button" v-on:click="clocks += 1" >+</span>
          </div>
        </div>
        <div class="inputRow center space">
          <button v-on:click="close" class="bt bt-close">Fechar</button>
          <button v-on:click="save" class="bt" >Salvar</button>
        </div>
      </div>
    </div>
  </div>
</template>
<style>
.center {
  text-align: center;
}
.space {
  margin-top: 2rem;
}
.newTaskContent {
  width: 100%;
  height: 100vh;
  position: fixed;
  left: 0;
  top: 0;
  z-index: 1;
  background:rgba(51,51,51,.5);
  display: flex;
  justify-content: center;
  align-items: center;
}
.newTaskBox {
  background: #fff;
  border-radius: 15px;
}
.content {
  padding: 3rem;
}
.inputRow {
  margin-bottom: 20px;
}
.inputRow label {
  display: block;
  font-family: 'Roboto', sans-serif;
  font-weight: bolder;
  font-size: 15px;
  margin-bottom: 10px;
}
.inputRow input {
  width: 100%;
  border: 1px solid #cdc3c7;
  border-radius: 5px;
  padding: 5px;
  font-family: 'Roboto', sans-serif;
  font-size: 15px;
  color: #A0A0A7;
}
.button {
  background: #19b5fe;
  color: #fff;
  font-family: 'Roboto', sans-serif;
  font-size: 20px;
  cursor: pointer;
  border-radius: 10px;
  padding: 1rem;
}
.bt {
  border:1px solid #dadfe1;
  margin: .5rem;
  -webkit-border-radius:40px/24px;
 -moz-border-radius:40px/24px;
  border-radius:40px/40px;
  cursor: pointer;
  vertical-align: middle;
  white-space: nowrap;
  -webkit-font-smoothing: antialiased;
  font-family: 'Roboto', sans-serif;
  font-weight: lighter;
  font-size: 1rem;
  transition: all .5s ease;
  display: inline-block;
  padding: .5rem 1rem .5rem 1rem;
  box-shadow: 0 2px 5px 0 rgba(0,0,0,0.16), 0 2px 10px 0 rgba(0,0,0,0.12);
  font-size: 1.2rem;
  padding: 1rem 3rem 1rem 3rem;
  margin: .5rem;
  text-transform: uppercase;
  background: #0AC25A;
  border: 1px solid #0AC25A;
  color: #fff;
  }

.bt:hover {
  background: #2ecc71;
  border: 1px solid #0AC25A;
}
.bt-close {
  background: #fff;
  color: #ef4836;
  box-shadow: none;
  border:none;
}
.bt-close:hover {
  background: none;
  border: none;
}
</style>
