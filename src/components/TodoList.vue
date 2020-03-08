<template>
  <div>
    <div>TodoList</div>
    <div class="list">
      <div class="done">
        <div>Done!!!</div>
        <ul>
          <li v-for="task in doneLists" :key="task.name">
            {{ task.name }}
            <button @click="changeDone(task)">change</button>
          </li>
        </ul>
      </div>
      <div class="notyet">
        <div>Not Yet...</div>
        <ul>
          <li v-for="task in yetLists" :key="task.name">
            {{ task.name }}
          </li>
        </ul>
      </div>
    </div>
    <div class="input">
      <label>
        Add new task
        <input type="text" v-model="newTaskName" />
      </label>
      <button @click="addTask">add!</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoList",
  data() {
    return {
      lists: [
        { name: "Test", isdone: false },
        { name: "test2", isdone: true }
      ],
      newTaskName: ""
    };
  },
  computed: {
    doneLists: function() {
      return this.lists.filter(function(task) {
        return task.isdone;
      });
    },
    yetLists: function() {
      return this.lists.filter(function(task) {
        return !task.isdone;
      });
    }
  },
  methods: {
    addTask() {
      if (this.newTaskName != "")
        this.lists.push({ name: this.newTaskName, isdone: false });
      this.newTaskName = "";
    },
    switchDone: function(task) {
      const index = this.lists.findIndex(item => item === task.name);
      this.lists[index].isdone = false;
    }
  }
};
</script>

<style>
.list {
  width: 100px;
  margin-left: auto;
  margin-right: auto;
}
.list li {
  text-align: left;
}
</style>
