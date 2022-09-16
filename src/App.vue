<template>
	<main class="page">
		<div class="page__container">
			<h1 class='page__title'>Todo List</h1>
			<form class='page__form' @submit.prevent="addTodo">
				<input v-model="newTodo" />
				<button class="btn">Add Todo</button>
			</form>
			<ul class="page__list list">
				<li class="list__item" v-for="todo in filteredTodos" :key="todo.id">
					<input type="checkbox" v-model="todo.done">
					<span :class="{ done: todo.done }">{{ todo.text }}</span>
					<button @click="removeTodo(todo)">X</button>
				</li>
			</ul>
			<button @click="hideCompleted = !hideCompleted" class="page__btn-hide btn"> {{ hideCompleted ? 'Show all' :
			'Hide completed' }}</button>
		</div>
	</main>
</template>
<script>
let id = 0; // для подсчета уникального номера каждого элемента списка
export default {
	name: 'todoList',
	data() {
		return {
			newTodo: '',
			hideCompleted: false,
			todos: [
				{ id: id++, text: 'Learn HTML', done: true },
				{ id: id++, text: 'Learn JavaScript', done: true },
				{ id: id++, text: 'Learn Vue', done: false }
			]
		}
	},
	computed: {
		filteredTodos() { // скрываем выполненные элементы списка
			return this.hideCompleted ? this.todos.filter((item) => !item.done) : this.todos;
		}
	},
	methods: {
		addTodo() { // метод на добавление элемента в список
			this.todos.push({ id: id++, text: this.newTodo, done: false });
			this.newTodo = '';
		},
		removeTodo(todo) { // метод на удаление элемента из списка
			this.todos = this.todos.filter((item) => item !== todo)
		}
	}
}
</script>