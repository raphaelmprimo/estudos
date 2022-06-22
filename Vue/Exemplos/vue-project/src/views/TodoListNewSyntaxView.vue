<template>
  <div>
    <h1>Lista de Tarefas</h1>
    <input type="text" v-model="state.currentTask" @keyup.enter="adicionar"> 
    <button @click="adicionar">
      Adicionar
    </button>
    <ul>
      <li
        v-for="task in state.tasks"
        :key="`${task}-${index}`"
        @dblclick="completar(task)"
        class="task-item"
        :class="{
          'is-done': task.isDone
        }"
      >
        {{ task.name }}
        <button @click="remover(task)">&times;</button>
      </li>
    </ul>
  </div>
</template>
<script>
import { reactive } from 'vue';

export default {
    setup () {
        const state = reactive({
            currentTask: '',
            tasks: [
                {
                    name: "Estudar Vue.js",
                    isDone: false,
                },
            ],
        })

        function adicionar () {
            if (! state.currentTask) {
                alert('Insira a tarefa');
            }

            state.tasks.push({
                name: state.currentTask,
                isDone: false,
            });

            state.currentTask = '';
        }

        function completar (task) {
            state.tasks = state.tasks.map(t => {
                if (t.name === task.name) {
                    return { ...t, isDone: !t.isDone }
                }

                return t;
            });
        }

        function remover (task) {
            state.tasks = state.tasks.filter((t) => t.name !== task.name);
        }

        return {
            state,
            adicionar,
            completar,
            remover
        }
    }
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