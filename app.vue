<template>
  <header>
    <div class="navbar sticky top-0 bg-primary">
      <div class="flex-1">
        <a class="btn btn-ghost normal-case text-white text-xl">TODO</a>
      </div>
      <div class="flex-none">
        <ul class="menu text-white menu-horizontal px-1">
          <li><a href="/">Home</a></li>
        </ul>
      </div>
    </div>
  </header>
  <main>
    <div class="flex justify-center mt-10">
      <h1 class="font-bold text-3xl">Todo List</h1>
    </div>
    <div class="flex p-12 flex-col space-y-4">

      <div class="alert alert-warning" v-if="tasks.length <= 0">
        <svg xmlns="http://www.w3.org/2000/svg" class="stroke-current shrink-0 h-6 w-6" fill="none" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
            d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z" />
        </svg>
        <span>Belum ada task</span>
      </div>


      <div v-for="(task, key) in tasks" :key="key" class="bg-reza shadow-md p-4 rounded-lg flex items-center space-x-4">
        <input type="checkbox" class="form-checkbox text-primary" v-model="task.isDone">
        <div class="block">
          <div>
            <h2
              :class="task.isDone ? 'font-semibold text-lg text-white line-through' : 'font-semibold text-lg text-white'">
              {{
                task.title }}</h2>
            <p class="text-white text-sm">{{ task.description }}</p>
          </div>
          <div class="ml-auto">
            <button class="btn btn-danger mt-3 btn-xs text-xs" @click="deleteTask(key)">
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 30 30" stroke-width="1.5"
                stroke="currentColor" class="w-6 h-6">
                <path stroke-linecap="round" stroke-linejoin="round"
                  d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0" />
              </svg>
              <span class="text-xs ms-0">
                Delete
              </span>
            </button>

          </div>
        </div>
      </div>

      <form @submit.prevent="submitTodo" class="space-y-2">
        <input type="text" placeholder="Title" @change="onChangeTitle" class="input input-bordered w-full max-w-full" />
        <input type="text" placeholder="Description" @change="onChangeDesc"
          class="input input-bordered w-full max-w-full" />
        <button class="btn btn-success me-2" type="submit">SAVE</button>
        <button class="btn btn-outline btn-error" type="reset">CANCEL</button>
      </form>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      title: null,
      description: null,
      tasks: [{
        title: 'Task 1',
        description: 'Description 1',
        isDone: false
      },
      {
        title: 'Task 2',
        description: 'Description 2',
        isDone: true
      },
      {
        title: 'Task 3',
        description: 'Description 3',
        isDone: false
      },
      ],
    };
  },
  methods: {
    completeTask(taskId) {
      // Logika untuk menyelesaikan tugas
    },
    deleteTask(taskId) {
      // Logika untuk menghapus tugas
      console.log('task id = ', taskId)
      this.tasks.splice(taskId, 1)
    },
    submitTodo(e) {
      if (!this.title || !this.description) {
        return alert('isi title atau description nya dulu ya..');
      }
      this.tasks.push({ title: this.title, description: this.description, isDone: false })
      this.title = null;
      this.description = null
      e.target.reset();
    },
    onChangeTitle(e) {
      this.title = e.target.value
    },
    onChangeDesc(e) {
      this.description = e.target.value
    }
  },
};
</script>
