<template>
  <div>
    <h1>할 일</h1>
    <table>
      <tr><td>ID</td><td>기한</td><td>할일</td></tr>
      <tr v-for="(todo, index) in todos" v-bind:key="todo.id" v-bind:class="{done: todo.done}">
        <td>{{ todo.id }}</td>
        <td>{{ todo.date }}</td> 
        <td>
          <input type="checkbox" v-model="todo.done" />
          {{ todo.title }}
          <span v-on:click="deleteTodo(index)">x</span>
        </td>
      </tr>
    </table>
    <input type="text" v-model="title" placeholder="할 일을 입력하세요." />
    <input type="date" v-model="selectedDate" />
    <button type="button" v-on:click="addTodo">추가</button>

  </div>
</template>

<script>

export default {
  name: "MyTodo",
  data() {
    return {
      todos: [
        { id: 1, title: "과제", done: false, date: "2023-05-23" },
        { id: 2, title: "시험공부", done: false, date: "2023-06-01"  },
        { id: 3, title:"코딩훈련", done: false, date: "2023-06-05"  }
      ],
      title: "",
      lastId: 3,
      selectedDate: null 
    }
  },
  methods: {
    addTodo: function() {
        this.todos.push({ id: ++this.lastId, title: this.title, date: this.selectedDate });
        this.title = "";
        this.selectedDate = null; // 입력 후 초기화
        },
    deleteTodo(index) {
      if (confirm("삭제하시겠습니까?"))
        this.todos.splice(index, 1);
    }
  }
}
</script>

<style scoped>
h1 { border-bottom: 1px solid gray; }
div { padding: 30px; margin: 30px auto; width: 600px;
  border: 1px solid #ccc; box-shadow: 3px 3px 3px #aaa; }
table { border-collapse: collapse; margin: 20px 0; width: 100%; }
tr:nth-child(1) { background-color: #ddd; text-align: center; }
td { border: 1px solid gray; padding: 6px; }
td:nth-child(1) { text-align: center; width: 30px; }
input[type=text] { padding: 5px; margin-right: 5px; width: 300px; }
button { padding: 0.3em 1.5em; }
span { font-weight: bold; margin-left: 10px; cursor: pointer; float: right;}
tr.done { background-color: #f8f8f8; color: #bbb; text-decoration: line-through; }
input[type=checkbox] { accent-color: #bbb; }
</style>
