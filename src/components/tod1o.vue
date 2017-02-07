<script>
export default {
  data () {
    return {
      editable: true
    }
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
		<div class="tasks-content">
			<h1>Tarefas </h1>
			<div class="tasks add" :contenteditable="editable" v-on:keyup.enter="save" v-on:click="clickHandler">
				<h2 class="active" >Digite e aperte enter</h2>
			</div>
			<div class="tasks">
				<h2>Ir ao mercado</h2>
				<div>
					<i class="fa fa-check fa-2x" aria-hidden="true"></i>
					<i class="fa fa-trash-o fa-2x" aria-hidden="true"></i>
				</div>

			</div>
			<div class="tasks complete">
				<h2>Fazer um todo App</h2>
				<div>
					<i class="fa fa-trash-o fa-2x" aria-hidden="true"></i>
				</div>
			</div>
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

.tasks-content
	background: rgba(51, 51, 51, .6)
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

.tasks-content h1
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

.tasks i
	color: rgba(255, 255, 255, .2)
	cursor: pointer
	padding-left: .6rem

.tasks i:hover
	color: rgba(255, 255, 255, .5)
.add h2
	color: rgba(255, 255, 255, .5)

.complete h2
	text-decoration: line-through
	color: rgba(255, 255, 255, .2)
</style>
