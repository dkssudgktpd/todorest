<template>
  <form action="" @submit.prevent="onSubmit">
    <div class="d-flex">
      <div class="flex-grow-1 mr-2 mb-2">
        <input
          class="form-control"
          type="text"
          v-model="todo"
          placeholder="Type New Todo"
        />
      </div>
      <div>
        <button class="btn btn-primary" type="submit">Add</button>
      </div>
    </div>
    <div v-show="hasError" style="color: red">내용을 기재해 주세요.</div>
  </form>
</template>

<script>
import { ref } from "vue";
export default {
  setup(props, context) {
    const hasError = ref(false);
    const todo = ref("");
    // todo 등록
    const onSubmit = () => {
      if (todo.value === "") {
        hasError.value = true;
      } else {
        hasError.value = false;
        context.emit("addTodo", {
          id: Date.now(),
          subject: todo.value,
          complete: false,
        });
      }
      todo.value = "";
    };
    return { onSubmit, hasError, todo };
  },
};
</script>

<style></style>
