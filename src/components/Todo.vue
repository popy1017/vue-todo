<template>
  <div class="item-card">
    <div class="check-area">
      <input class="checkbox" type="checkbox" v-model="todo.done" />
    </div>
    <div class="title-area">{{ todo.title }}</div>
    <div class="edit-delete-area">
      <button @click="toEditTodo">編集</button>
      <button @click="remove">削除</button>
    </div>
    <div class="due-date-area">
      <template v-if="showRelative">{{ todo.dueDate | fromNow }}</template>
      <template v-else>{{ todo.dueDate | llll }}</template>
    </div>
    <div class="note-area">{{ todo.note }}</div>
  </div>
</template>

<script>
export default {
  props: ["todo", "showRelative"],
  methods: {
    toEditTodo() {
      this.$router.push({
        name: "edit",
        params: {
          todo: this.todo
        }
      });
    },
    remove() {
      const result = confirm("削除してもよろしいですか？");
      if (result) {
        this.$root.removeTodo(this.todo.id);
      }
    }
  }
};
</script>

<style scoped>
.item-card {
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.3);
  border-radius: 10px;
  margin: 1rem auto;
  display: grid;
  grid-template-rows: 40% 20% 40%;
  grid-template-columns: 50px 1fr 50px;
}
.check-area {
  grid-row: 1 / 4;
  grid-column: 1 / 2;
  display: flex;
  justify-content: center;
  align-items: center;
}
.title-area {
  grid-row: 1 / 2;
  grid-column: 2 / 3;
  margin: 10px;
  font-size: 1.5rem;
  font-weight: bold;
}
.edit-delete-area {
  grid-row: 1 / 3;
  grid-column: 3 / 4;
  margin: auto;
}
.due-date-area {
  grid-row: 2 / 3;
  grid-column: 2 / 3;
  text-align: right;
  margin: 0 1rem;
}
.note-area {
  grid-row: 3 / 4;
  grid-column: 2 / 3;
  margin: 10px;
}
</style>
