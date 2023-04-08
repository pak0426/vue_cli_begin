<template>
  <div>
    <TransitionGroup name="list" tag="ul" class="container">
      <li v-for="(todoItem, index) in propsData" v-bind:key="todoItem.item" class="shadow">
        <span v-bind:class="{checkBtnCompleted: todoItem.completed, checkBtn: !todoItem.completed}" v-on:click="toggleComplete(todoItem, index)">
          <i class="fa-solid fa-check"></i>
        </span>
        <span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem.item }}</span>
        <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
          <i class="fa-regular fa-trash-can"></i>
        </span>
      </li>
    </TransitionGroup>
  </div>
</template>

<script>
export default {
  props: ['propsData'],
  data: function () {
    return {
    }
  },
  methods: {
    removeTodo: function (todoItem, index) {
      this.$emit('removeTodo', todoItem, index);
    },
    toggleComplete: function (todoItem, index) {
      this.$emit('toggleComplete', todoItem, index);
    },
  }
}
</script>

<style scoped>
ul {
  list-style-type: none;
  padding-right: 0px;
  margin-top: 0;
  text-align: left;
}
li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}
.checkBtn {
  line-height: 45px;
  color: #62acde;
  margin-left: 5px;
}
.checkBtnCompleted {
  color: #b3adad;
}
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
}
.list-enter-active,
.list-leave-active {
  transition: all 1s ease;
}
.list-enter,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>