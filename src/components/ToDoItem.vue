<template>
	<div>
		<label :for="'todoStatus'+todoItem.id"  class="todo-item__text"> {{ todoItem.title }}</label>
		<input
			:id="'todoStatus'+todoItem.id"
			type="checkbox"
			:checked="todoItem.completed"
			@change="changeState"
		>
	</div>
</template>
<script setup>
const props = defineProps({
	todoItem: {
		type: Object,
		required: true
	}
})

function changeState() {
	props.todoItem.completed = !props.todoItem.completed
}
</script>
<style scoped>
input {
	margin-left: 20px;
	display: block;
	width: 25px;
	height: 25px;
}
</style>