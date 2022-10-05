<template>
  <div>
    <NavBar />
    <RouterView
      @update-todo-toast="updateTodoToast"
      @new-todo-toast="newTodoToast"
      @update-load-fail-toast="updateLoadFailToast"
      @update-todo-fail-toast="updateTodoFailToast"
      @err-subject-toast="errSubjectToast"
      @new-todo-fail-toast="newTodoFailToast"
      @list-load-fail-toast="listLoadFailToast"
      @delete-todo-fail-toast="deleteTodoFailToast"
      @delete-todo-toast="deleteTodoToast"
    />
    <Transition name="fade">
      <ToastBox v-if="showToast" :message="toastMessage" :color="toastType" />
    </Transition>
  </div>
</template>
<script>
import NavBar from "@/components/NavBar.vue";
import ToastBox from "@/components/ToastBox.vue";
import { useToast } from "@/composables/toast.js";
export default {
  components: {
    ToastBox,
    NavBar,
  },
  setup() {
    const { showToast, toastMessage, toastType, triggerToast } = useToast();
    const updateTodoToast = () => {
      triggerToast("내용이 업데이트 되었습니다.");
    };
    const newTodoToast = () => {
      triggerToast("새 글이 등록되었습니다.");
    };
    const updateLoadFailToast = () => {
      triggerToast("내용 갱신에 실패하였습니다.", "danger");
    };
    const updateTodoFailToast = () => {
      triggerToast("업데이트에 실패하였습니다.", "danger");
    };
    const errSubjectToast = () => {
      triggerToast("제목을 입력하세요.", "danger");
    };
    const newTodoFailToast = () => {
      triggerToast("새 글 등록이 실패하였습니다.", "danger");
    };
    const listLoadFailToast = () => {
      triggerToast("목록 호출에 실패하였습니다.", "danger");
    };
    const deleteTodoFailToast = () => {
      triggerToast("삭제에 실패하였습니다.", "danger");
    };
    const deleteTodoToast = () => {
      triggerToast("삭제 하였습니다.");
    };
    return {
      updateTodoToast,
      toastMessage,
      showToast,
      toastType,
      triggerToast,
      newTodoToast,
      updateLoadFailToast,
      updateTodoFailToast,
      errSubjectToast,
      newTodoFailToast,
      listLoadFailToast,
      deleteTodoFailToast,
      deleteTodoToast,
    };
  },
};
</script>
<style scoped>
#app {
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(-30px);
}
.fade-enter-to,
.fade-leave-from {
  opacity: 1;
  transform: translateY(0);
}
</style>
