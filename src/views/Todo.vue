<template>
  <div class="home">
    <v-text-field
      v-model="newTaskTitle"
      outlined
      label="Add Task"
      append-icon="mdi-plus"
      class="pa-3"
      hide-details
      clearable
      @click:append="addTask"
      @keyup.enter="addTask"

    />
    <v-list flat class="pt-0">
      <div 
        v-for="task in tasks" 
        :key="task.id" 
        :class="{ 'blue lighten-5' : task.done }">
        <v-list-item @click="taskDone(task.id)">
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox
                :input-value="task.done"
                color="primary"
              />
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
                :class="{ 'text-decoration-line-through' : task.done }"
              >
              {{ task.title }}
              </v-list-item-title>
            </v-list-item-content>

            <v-list-item-action>
              <v-btn 
                icon
                @click.stop="deleteTask(task.id)"
              >
                <v-icon color="primary lighten-1">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider/>
      </div>
    </v-list>
  </div>
</template>

<script>

  export default {
    name: 'Home',
    data() {
      return {
        newTaskTitle: '',
        tasks: []
      }
    },
    methods: {
      addTask() {
        let task = { 
          id: Date.now(),
          title: this.newTaskTitle,
          done: false
        }
        this.tasks.push(task)
        this.newTaskTitle = ''
      },
      taskDone(id) {
        let task = this.tasks.filter(task => task.id === id)[0]
        task.done = !task.done
      },
      deleteTask(id) {
        this.tasks = this.tasks.filter(task => task.id !== id)
      }
    }
  }
</script>
