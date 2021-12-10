<template>
  <div id="app" class="p-4">
    <div class="row">
      <div class="col form-inline">
        <b-form-input
          v-model="newTask"
          placeholder="Задача"
          @keyup.enter="add"
        >
      </b-form-input>
      <b-button
        @click="add" variant="primary" class="ml-3"
      >
        Добавить
      </b-button>
      </div>
    </div>
    <div class="row mt-5">
      <div class="col-3">
        <div class="p-2 alert alert-secondary">
          <h3>Бэклог</h3>
          <draggable
            class="list-group kanban-column"
            :list="arrBackLog"
            group="tasks"
          >
            <div class="list-group-item my-2"
              v-for="element in arrBackLog"
              :key="element.name"
            >
              {{ element.name }}
            </div>
          </draggable>
        </div>
      </div>
      <div class="col-3">
        <div class="p-2 alert alert-primary">
          <h3>В работе</h3>
          <draggable
            class="list-group kanban-column"
            :list="arrInProgress"
            group="tasks"
          >
            <div class="list-group-item my-2"
              v-for="element in arrInProgress"
              :key="element.name"
            >
              {{ element.name }}
            </div>
          </draggable>
        </div>
      </div>
      <div class="col-3">
        <div class="p-2 alert alert-primary">
          <h3>В тестировании</h3>
          <draggable
            class="list-group kanban-column"
            :list="arrTested"
            group="tasks"
          >
            <div class="list-group-item my-2"
              v-for="element in arrTested"
              :key="element.name"
            >
              {{ element.name }}
            </div>
          </draggable>
        </div>
      </div>
      <div class="col-3">
        <div class="p-2 alert alert-primary">
          <h3>Готово</h3>
          <draggable
            class="list-group kanban-column"
            :list="arrDone"
            group="tasks"
          >
            <div class="list-group-item my-2"
              v-for="element in arrDone"
              :key="element.name"
            >
              {{ element.name }}
            </div>
          </draggable>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import draggable from "vuedraggable";

export default {
  name: 'App',
  data() {
    return {
      newTask: '',
      arrBackLog: [
        {
          name: 'Создать страницу регистрации',
        },
        { name: 'Протестировать дашборд' },
        { name: 'Написать стили' },
        { name: 'Протестировать UX' }
      ],
      arrInProgress: [],
      arrTested: [],
      arrDone: []
    }
  },
  methods: {
    add() {
      if (this.newTask) {
        this.arrBackLog.push({ name: this.newTask });
        this.newTask = '';
      }
    }
  },
  components: {
    draggable
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.kanban-column {
  min-height: 300px;
}
</style>
