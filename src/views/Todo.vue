<template>
  <div class="home">

    <v-text-field
        v-model="newTaskTitle"
        class="mt-2 pa-3"
        outlined
        hide-details
        label="Add task"
        append-icon="mdi-plus"
        clearable
        @keyup.enter="addTask"
        @click:append="addTask"
    />

    <v-list
        class="pt-0"
        flat
    >
      <div
          v-for="(task, index) in tasks"
          :key="`index_${index}`"
      >
        <v-list-item
            @click="doneTask(task.id)"
            :class="{'blue lighten-5': task.done}"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox
                  :input-value="task.done"
                  color="primary"
              ></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
                  :class="{'text-decoration-line-through': task.done}"
              >{{ task.title }}
              </v-list-item-title>
            </v-list-item-content>

            <v-list-item-action>
              <v-btn
                  icon
                  @click.stop="deleteTask(task.id)"
              >
                <v-icon color="blue lighten-1">mdi-delete</v-icon>
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
  components: {},
  data() {
    return {
      newTaskTitle: '',
      tasks: [
        // {
        //   id: 1,
        //   title: 'Wake up',
        //   done: false
        // },
        // {
        //   id: 2,
        //   title: 'Get bananas',
        //   done: false
        // },
        // {
        //   id: 3,
        //   title: 'Eat bananas',
        //   done: false
        // },
      ]
    }
  },
  methods: {
    doneTask(id) {
      let task = this.tasks.filter(task => task.id === id)[0]
      task.done = !task.done;
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter(task => task.id !== id);
    },
    addTask() {
      let newTask = {
        id: Date.now(),
        title: this.newTaskTitle,
        done: false
      }

      this.tasks.push(newTask);
      this.newTaskTitle = '';
    }
  }
}
</script>
