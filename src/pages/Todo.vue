<template>
  <q-page class="bg-grey-2 column">
    <div class="row no-padding">
      <q-input
        v-model="newTask"
        label="Add Task"
        dense
        class="col bg-white-2"
        >
        <template v-slot:append>
          <q-btn
              @click="addTask(newTask)"
              @keyup.enter="addTask"
              round
              dense
              color-primary
              flat
              icon="add" />
        </template>
      </q-input>
    </div>
    <div>
      <q-list
        class="bg-white"
        separator
        bordered>
        <q-item
          :id="task.title"
          v-for="(task, index) in tasks"
          @click = "task.done = !task.done"
          clickable
          :class="{ 'done bg-blue-1' : task.done }"
          v-ripple>
          <q-item-section avatar>
            <q-checkbox
                v-model="task.done"
                color="primary" />
          </q-item-section>
          <q-item-section>
            <q-item-label>{{ task.title }}</q-item-label>
          </q-item-section>
          <q-item-section
          v-if="task.done"
          side>
          <q-btn
            @click.stop="deleteTask(index)"
            flat round color="primary"
            dense
            icon="delete" />
          </q-item-section>
        </q-item>
      </q-list>

      <div
          v-if="!tasks.length"
          class="no-task absolute-center">
        <q-icon
        name="check"
        size= "70px"
        color="primary"
        />
        <div class="text-center text-h5 text-primary">
          No tasks found
        </div>
      </div>
    </div>

  </q-page>
</template>

<script>
import { useQuasar } from 'quasar'


export default {
  data () {
    return {
      newTask: '',
      tasks : [
        {
          title : 'I cooka da pizza',
          done : false
        },
        {
          title : 'I eata da pizza',
          done : false
        },
        {
          title : 'I tossa da pizza',
          done : false
        }
      ]
    }
  },

  methods : {
    deleteTask (index){
      const $q = useQuasar()
        this.$q.dialog({
          title: 'Confirm',
          message: 'are you sure you want to delete?',
          cancel: true,
          persistent: true
        }).onOk(() => {
        this.tasks.splice(index, 1)
        this.$q.notify('Deleted')
      })
    },

    addTask(newTask){
      let taskNew = { title: newTask, done: false}
      const $q = useQuasar()
      this.$q.dialog({
          title: 'Confirm',
          message: 'are you sure you want to add the task?',
          cancel: true,
          persistent: true
        }).onOk(() => {
        this.tasks.push(taskNew)
        this.newTask = ''
        this.$q.notify('Task added successfully')
      })
    }
  }
}

</script>

<style lang="scss">
.done {
  .q-item__label{
    text-decoration: line-through;
    color: #bbb;
  }
  // background-color: #e0dede;
}

.q-field__bottom{
  height: 0vh;
}
</style>
