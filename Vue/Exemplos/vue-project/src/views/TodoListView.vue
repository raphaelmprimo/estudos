<template>
  <div>
    <h1>Lista de Tarefas</h1>
    <input type="text" v-model="currentTask" @keyup.enter="adicionar"> 
    <button @click="adicionar">
      Adicionar
    </button>
    <ul>
      <li
        v-for="task in tasks"
        :key="`${task}-${index}`"
        @dblclick="complete(task)"
        class="task-item"
        :class="{
          'is-done': task.isDone
        }"
      >
        {{ task.name }}
        <button @click="remove(task)">&times;</button>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  data: () => ({
    currentTask: '',
    tasks: [
      {
        name: "Estudar Vue.js",
        isDone: false,
      },
    ],
  }),
  methods: {
    adicionar () {
      if (! this.currentTask) {
        alert('Insira a tarefa');
      }

      this.tasks.push({
        name: this.currentTask,
        isDone: false,
      });

      this.currentTask = '';
    },
    complete (task) {
      this.tasks = this.tasks.map(t => {
        if (t.name === task.name) {
          return { ...t, isDone: !t.isDone }
        }

        return t;
      });
    },
    remove (task) {
      this.tasks = this.tasks.filter((t) => t.name !== task.name);
    },
  },
};
</script>
<style>
.is-done {
  text-decoration: line-through;
}
.task-item {
  cursor: pointer;
}
</style>