<template>
  <div class="Todo__Container">
    <h5>Enter Messages For Your Todo</h5>

    <div>
      <form class="input__container">
        <input type="text" name="screen" id="screen" v-model="TodoMessage" />
        <button @click.prevent="AddTodo(TodoMessage)">Add</button>
      </form>
    </div>
  </div>

  <div class="Output__Container" v-if="DbTodo.length < 1">
    <h2>No Messages</h2>
  </div>

  <div class="Output__Container" v-for="todo in DbTodo" :key="todo.id">
    <div class="box">
      <h4>{{ todo.message }}</h4>
      <h3 @click="deleteTodoHandler(todo.id)">x</h3>
    </div>
  </div>
</template>


<script >
export default {
  name: "TodoScreen",

  data() {
    return {
      TodoMessage: "",
      TodoArray: [],
      DbTodo: JSON.parse(localStorage.getItem("Todo")),
    };
  },

  methods: {
    AddTodo: function (data) {
      const isMessageAlreadyExist = this.DbTodo.find(
        (todo) => todo.message == data
      );
      if (!this.TodoMessage) {
        return alert("Empty: Please enter a message");
      } else if (isMessageAlreadyExist) {
        alert("Hey!! You already added that to your list");
      } else {
        this.DbTodo.push({
          id: this.DbTodo.length,
          message: data,
          isEditing: false,
          bgColor: "#ffffff",
        });
        this.TodoMessage = "";
      }
      localStorage.setItem("Todo", JSON.stringify(this.DbTodo));
    },

    deleteTodoHandler: function (id) {
      const FindSpecificData = this.DbTodo.filter((todo) => todo.id !== id);
      this.DbTodo = FindSpecificData;
      localStorage.setItem("Todo", JSON.stringify(this.DbTodo));
    },
  },
};
</script>

<style scoped>
.Todo__Container,
.Output__Container {
  width: 80%;
  background-color: rgb(16, 30, 92);
  padding: 1em;
  margin: 0 auto;
  color: white;
  border-radius: 2px;
}

@media (max-width: 768px) {
  .Todo__Container,
  .Output__Container {
    width: 90%;
  }
}

.input__container {
  display: flex;
  gap: 0.5em;
  align-items: center;
  margin: 0.5em 0;
}
form {
  width: 100%;
}

input {
  width: 100%;
  padding: 1em;
  border-radius: 1px;
  outline: none;
  border: none;
}

button {
  background-color: rgb(0, 123, 254);
  border-radius: 1px;
  outline: none;
  border: none;
  padding: 1em 2em;
  color: white;
  font-weight: bold;
  text-align: center;
  cursor: pointer;
}

.Output__Container {
  margin-top: 1em;
  background-color: white;
  color: black;
  border: 1px solid rgba(204, 214, 246, 0.311);
  box-shadow: rgba(0, 0, 0, 0.1) 0px 1px 3px 0px,
    rgba(0, 0, 0, 0.06) 0px 1px 2px 0px;
  transition: all 0.4s ease-in-out;
}

.Output__Container:active {
  transform: scale(1.02);
}

.box {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.box h4 {
  cursor: pointer;
  font-size: 16px;
}

.box h3 {
  cursor: pointer;
  color: red;
  font-size: 20px;
}
</style>