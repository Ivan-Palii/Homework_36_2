<script setup>
import ToDoItem from "./components/ToDoItem.vue";
import axios from 'axios';
import {ref} from "vue";

const BASE_URL = 'https://jsonplaceholder.typicode.com/'
//https://jsonplaceholder.typicode.com/users/4/todos

const todoList = ref([])
const currentUser = ref(5)

function getToDoList() {
	console.log('here')
	axios.get(BASE_URL + 'users/' + currentUser.value + '/todos').then(
		function (response) {
			console.log(response.data)
			todoList.value = []
			response.data.forEach(item => todoList.value.push(item))
		},
		function (error) {
			console.log(error)
		}
	)

}

getToDoList()
</script>
<template>
	<div class="wrapper">
		<header class="header">
			<h1 class="header__title">ToDo list</h1>
		</header>
		<main class="main">
			<div class="main__todo-container todo">
				<ToDoItem
					v-for="item in todoList"
					class="todo__item"
					:class="{'todo__item_done': item.completed,
					'todo__item_pending': !item.completed}"
					:todo-item="item"
				/>
			</div>
		</main>
	</div>
</template>
<style
	scoped
	lang="scss"
>
.wrapper {
	padding: 15px;
}

.header {
	// .header__title
	&__title {
		font-size: 46px;
		font-weight: 700;
	}
}

.main {
	margin: 20px;
	// .main__todo-container
	&__todo-container {
		height: 800px;
		overflow-y: scroll;

	}
}

.todo {
	// .todo__item
	&__item {
		height: 50px;
		border: 3px solid;
		border-radius: 15px;
		display: flex;
		align-items: center;
		padding: 5px;
		&_pending {
			background-color: #ffc662;
			border-color: orangered;
		}

		&_done {
			background-color: lightgreen;
			border-color: darkgreen;
		}
		&:not(:last-child){
			margin-bottom: 2px;
		}
	}

}
</style>
