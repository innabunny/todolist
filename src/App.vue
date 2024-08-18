<template>
  <body>
    <h1>Список задач</h1>
    <!-- Список -->

    <div v-for="task in tasks" :key="task.id" class="task-item">
      <div class="flex">
        <p :class="{ completed: task.completed }">{{ task.title }}</p>
        <input
          @click="toggleCompleted(task)"
          type="checkbox"
          class="checkbox"
          v-bind:checked="task.completed"
        />
      </div>
      <div class="btns">
        <button @click="deleteTask(task)">Удалить</button>
        <button @click="editTask(task)">Изменить</button>
      </div>
    </div>

    <!-- Добавить задачу -->
    <form @submit.prevent="addTask()">
      <input type="text" placeholder="Новая задача" v-model="taskInput" />
      <button type="submit">Создать</button>
    </form>
  </body>
</template>

<script>
export default {
  data() {
    return {
      tasks: [
        {
          id: 1,
          title: "delectus aut autem",
          completed: false,
        },
        {
          id: 2,
          title: "quis ut nam facilis et officia qui",
          completed: false,
        },
        {
          id: 3,
          title: "fugiat veniam minus",
          completed: false,
        },
        {
          id: 4,
          title: "et porro tempora",
          completed: true,
        },
        {
          id: 5,
          title:
            "laboriosam mollitia et enim quasi adipisci quia provident illum",
          completed: false,
        },
      ],
      taskInput: "",
      isChecked: false,
    };
  },
  methods: {
    addTask() {
      if (this.taskInput !== null && this.taskInput.trim() !== "") {
        const newTask = {
          id: Math.random().toString(),
          title: this.taskInput,
          completed: false,
        };
        this.tasks.push(newTask);
        this.taskInput = "";
      }
    },
    deleteTask(task) {
      const taskIndex = this.tasks.indexOf(task);
      this.tasks.splice(taskIndex, 1);
    },
    editTask(task) {
      const taskIndex = this.tasks.indexOf(task);
      const editedTodo = prompt("Редактировать задачу:");
      if (editedTodo !== null && editedTodo.trim() !== "") {
        this.tasks[taskIndex].title = editedTodo.trim();
      }
    },
    toggleCompleted(task) {
      task.completed = !task.completed;
    },
  },
};
</script>

<style scoped>
* {
  margin: 0 auto;
  box-sizing: border-box;
  padding: 0;
}
body {
  background-image: linear-gradient(#2e9aff, #f498ad);
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}
h1 {
  font-size: 30px;
  text-align: center;
  padding-top: 1%;
  font-family: Arial, Helvetica, sans-serif;
  color: rgb(49, 46, 46);
  padding-bottom: 1%;
}

.task-item {
  width: 50%;
  border: 2px solid rgb(100, 126, 240);
  padding: 10px;
  margin: 10px;
  display: flex;
  flex-direction: column;
  row-gap: 20px;
}

form {
  padding-bottom: 3%;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
}

button {
  width: 80px;
  height: 30px;
  background-color: transparent;
  border: 1px solid rgb(100, 126, 240);
  border-radius: 3px;
  cursor: pointer;
  text-transform: uppercase;
  font-size: 12px;
  font-family: Arial, Helvetica, sans-serif;
}
.completed {
  text-decoration: line-through;
}

.flex {
  width: 60%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 20px;
}

p {
  font-family: Arial, Helvetica, sans-serif;
  font-size: 16px;
  margin: 0;
}

.checkbox {
  width: 20px;
  height: 20px;
  list-style-type: none;
  margin: 0;
}
.btns button {
  margin-right: 10px;
}

input:last-of-type {
  list-style-type: none;
  height: 30px;
  background-color: transparent;
  border: none;
  border-bottom: 1px solid rgb(100, 126, 240);
  margin-right: 3%;
}
</style>
