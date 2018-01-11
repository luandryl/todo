<script>
export default {
  data () {
    return {
      editable: true,
      task: '',
      tasks: []
    }
  },
  methods: {
    getText: function () {
      this.editable = !this.editable
      this.task = this.$refs.active.textContent
      this.$refs.active.innerHTML = 'Digite e aperte enter'
      this.save()
    },
    clickHandler: function () {
      this.$refs.active.innerHTML = ''
      this.editable = true
    },
    save: function () {
      if (JSON.parse(this.$parent.localStorage.get('tasks')) === null) {
        let tasks = {
          items: []
        }
        this.$parent.localStorage.set('tasks', JSON.stringify(tasks))
      }

      let task = {
        'task': this.task,
        'status': 0
      }
      let tasks = JSON.parse(this.$parent.localStorage.get('tasks'))
      tasks.items.push(task)
      this.$parent.localStorage.set('tasks', JSON.stringify(tasks))
      this.loadData()
    },
    done: function (item) {
      item.status = 1
      window.localStorage.removeItem('tasks')
      this.$parent.localStorage.set('tasks', JSON.stringify(this.tasks))
      this.loadData()
    },
    remove: function (item) {
      this.tasks.items.splice(item, 1)
      this.$parent.localStorage.set('tasks', JSON.stringify(this.tasks))
    },
    loadData: function () {
      if (JSON.parse(this.$parent.localStorage.get('tasks')) != null) {
        this.tasks = JSON.parse(this.$parent.localStorage.get('tasks'))
      }
    }
  },
  created: function () {
    this.loadData()
  }
}
</script>
<template>
	<div class="todoContainer">
		<div class="todoTop">
			<div>
				<label class="day">31</label><label class="data-end"> Janeiro <br /> 2017 </label>
			</div>
			<h1>Bem Vindo</h1>
		</div>

    <div class="todoWrapper">
      <i class="fa fa-angle-left fa-5x arrow" aria-hidden="true"></i>
  		<div class="tasks-box">

  			<h1>Tarefas </h1>
  			<div class="tasks add" ref="active" :contenteditable="editable" v-on:keyup.enter="getText" v-on:click="clickHandler">
  				Digite e aperte enter
  			</div>

        <div class="tasks" v-for="item in tasks.items" v-bind:class="{ 'complete': item.status }" >
  				<h2>{{item.task}}</h2>
  				<div>
  					<i class="fa fa-check fa-2x" aria-hidden="true" @click='done(item)' v-if="!item.status" ></i>
  					<i class="fa fa-trash-o fa-2x" aria-hidden="true" @click='remove(item)' ></i>
  				</div>
  			</div>

  		</div>
      <i class="fa fa-angle-right fa-5x arrow" aria-hidden="true"></i>
    </div>

	</div>
</template>
<style lang="sass">
@import url(https://fonts.googleapis.com/css?family=Lato)
$font: 'Lato', sans-serif

.todoContainer
	display: flex
	justify-content: space-between
	align-items: center
	flex-direction: column

.todoTop
	@extend .flex
	padding: 1rem
	width: 95%
	margin-bottom: 1rem

.todoWrapper
  display: flex
  justify-content: space-between
  align-items: strech
  width: 95%
  margin-bottom: 5rem

.arrow
  color: #fff
  cursor: pointer
  margin-top: 3rem

.tasks-box
	background: rgba(51, 51, 51, 1)
	width: 450px
	-webkit-border-radius: 10px
  -moz-border-radius: 10px
  -ms-border-radius: 10px
  border-radius: 10px
	box-shadow: 0 4px 5px 0 rgba(0,0,0,0.14), 0 1px 10px 0 rgba(0,0,0,0.12), 0 2px 4px -1px rgba(0,0,0,0.3)

.flex
	display: flex
	justify-content: space-between
	align-items: center

.title
	font-family: $font
	color: #fff
	font-size: 5rem
	margin: .5rem

.day
	@extend .title

.data-end
	@extend .day
	font-size: 2rem

.todoTop h1
	@extend .title
	font-weight: 400

.tasks-box h1
	@extend .title
	font-size: 2rem
	margin: 2rem

.tasks
	margin: 0 2rem 1rem  2rem
	border-bottom: 1px solid rgba(255, 255, 255, .5)
	padding: 0 0 .5rem  0
	display: flex
	justify-content: space-between
	align-items: center


.tasks h2
	@extend .title
	font-size: 1.2rem
	margin: 0
  cursor: pointer

.tasks i
	color: rgba(255, 255, 255, .2)
	cursor: pointer
	padding-left: .6rem

.tasks i:hover
	color: rgba(255, 255, 255, .5)

.add
  @extend .title
  font-size: 1.2rem
  color: rgba(255, 255, 255, .5)

.complete h2
	text-decoration: line-through
	color: rgba(255, 255, 255, .2)

@media (max-width: 660px)
  .title
  	font-size: 2rem
  	margin: .5rem

  .day
    font-size: 2rem

  .data-end
  	font-size: 1rem

  .tasks-box
    width: 90%

  .tasks-box h1
    font-size: 2rem
    margin: .5rem

  .tasks h2
    font-size: 1.2rem
    margin: .5rem
  .add
    font-size: 1.5rem
    margin: 1.5rem 1rem 1.5rem  1rem

</style>
