<template>
  <div class="home">
    <div class="wrapper">
      <div id="list">
        <ul>
          <li v-for="(item, index) in tasks" :key="index">
            <button
              @click="
                () => {
                  deleteTask(index);
                }
              "
            >
              <span>{{ item }}</span>
            </button>
          </li>
        </ul>
      </div>

      <div id="actions">
        <form
          :on-submit="
            (ev) => {
              ev.preventDefault();
              addTask();
            }
          "
        >
          <input type="text" v-model="newTask" />

          <button
            @click="
              () => {
                addTask();
              }
            "
          >
            Enviar
          </button>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, watch, onMounted } from "vue";

const newTask = ref("");
const tasks = ref([]);

// por enquanto isso está sem ação, mas ele fica observando
// o "newTask" e executa essa função sempre que atualizamos o input
watch(newTask, (current, newValue) => {
  console.log(current, newValue);
});

// quando o componente é montado
onMounted(() => {
  console.log(tasks.value);
});

function deleteTask(index) {
  tasks.value.splice(index, 1);
}

function addTask() {
  if (newTask.value !== "") {
    tasks.value.push(newTask.value);
    newTask.value = "";
  }
}
</script>

<style>
.wrapper {
  margin: 0 auto;
  max-width: 350px;
}
#actions {
  display: flex;
  flex-direction: column;
}

#actions button {
  margin-top: 20px;
}
</style>
