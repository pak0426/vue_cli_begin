<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" @keyup.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
      <i class="fa-solid fa-plus addBtn"></i>
    </span>
    <TodoModal v-if="showModal" @close="showModal = false">
      <!--
    you can use custom content here to overwrite
    default content
  -->
      <h3 slot="header">
        경고!!
        <span class="closeModalBtn" @click="closeModal">
          <i class="fa-solid fa-xmark"></i>
        </span>
      </h3>
      <div slot="body">
        아무것도 입력하지 않았습니다.
      </div>
    </TodoModal>
  </div>
</template>

<script>
import TodoModal from "@/components/common/TodoModal.vue";

export default {
  data: function () {
    return {
      newTodoItem: "",
      showModal: false
    }
  },
  methods: {
    addTodo: function() {
      if(!this.newTodoItem) {
        this.showModal = !this.showModal;
        return;
      }
      this.$emit('addTodoItem', this.newTodoItem);
      this.clearInput();
    },
    clearInput: function() {
      this.$emit('clearTodoItem');
      this.newTodoItem = '';
    },
    closeModal: function () {
      this.showModal = !this.showModal;
    },
  },
  components: {
    'TodoModal' : TodoModal
  }
}
</script>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
  margin-left: 40px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9em;
  line-height: 50px;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478FB, #8763FB);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: white;
  vertical-align: middle;
}

.closeModalBtn {
  color: #42b983;
}
</style>