<template>
  <div class="container">
    <h2>Todo List</h2>
    <!-- Todo 검색폼 -->
    <input
      class="form-control mb-2"
      type="text"
      v-model="searchText"
      placeholder="Search"
    />
    <!-- Todo 입력창 -->
    <TodoForm @addTodo="addTodo" />
    <div v-if="!todos.length">내용이 없습니다.</div>
    <!-- Todo 목록 -->
    <TodoList
      :todos="filterTodos"
      @delete-todo="deleteTodo"
      @toggle-todo="toggleTodo"
    />
  </div>
</template>

<script>
import { ref, computed } from "vue";
import TodoForm from "./components/TodoSimpleForm.vue";
import TodoList from "./components/TodoList.vue";
export default {
  components: {
    TodoForm,
    TodoList,
  },
  setup() {
    const todos = ref([
      { id: 1, subject: "할일목록1", complete: false },
      { id: 2, subject: "할일목록2", complete: false },
      { id: 3, subject: "할일목록3", complete: false },
    ]);
    const searchText = ref("");
    const addTodo = (todo) => {
      todos.value.push(todo);
    };
    const filterTodos = computed(() => {
      if (searchText.value) {
        return todos.value.filter((todo) => {
          return todo.subject.includes(searchText.value);
        });
      }
      return todos.value;
    });
    const deleteTodo = (index) => {
      todos.value.splice(index, 1);
    };
    const toggleTodo = (index) => {
      todos.value[index].complete = !todos.value[index].complete;
    };

    return { todos, addTodo, deleteTodo, toggleTodo, searchText, filterTodos };
  },
};
</script>

<style>
#app {
}
.todostyle {
  text-decoration: line-through;
  color: gray;
}
</style>
