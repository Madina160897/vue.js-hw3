<script>
export default {
  data() {
    return {
      toDoList: [],
      isEdit: false,
      newText: "",
      editingId: "",
      editText: "",
    };
  },
  methods: {
    addNewText() {
      if (this.newText == "") {
        return;
      }
      let newToDo = {
        id: this.toDoList.length + 1,
        text: this.newText,
        isDone: false,
      };
      this.toDoList.push(newToDo);
      this.newText = "";
    },
    toggleDone(id) {
      this.toDoList = this.toDoList.map((toDo) => {
        if (toDo.id == id) {
          toDo.isDone = !toDo.isDone;
        }
        return toDo;
      });
    },
    openEditText(id) {
      (this.isEdit = true), (this.editingId = id);
    },
    saveText() {
      let newToDo = {
        id: this.editingId,
        text: this.editText,
        isDone: false,
      };
      (this.toDoList = this.toDoList.map((toDo) => {
        if (toDo.id == newToDo.id) {
          return newToDo;
        }
        return toDo;
      })),
        (this.isEdit = false);
      this.editingId = "";
    },
  },
};
</script>

<template>
  <div class="body" :style="body">
    <div class="toDoList">
      <input type="text" v-model="newText" />
      <button @click="addNewText">Add</button>
      <ul>
        <li v-for="toDo in toDoList" v-bind:key="toDo.id">
          <span @click="toggleDone(toDo.id)" :class="{ done: toDo.isDone }">{{
            toDo.text
          }}</span>
          <button @click="openEditText(toDo.id)">Edit</button>
        </li>
      </ul>
    </div>
    <div class="divEdit" v-if="isEdit">
      <input type="text" v-model="editText" />
      <button @click="saveText">Edit</button>
    </div>
  </div>
</template>

<style>
body{
    margin: 0;
    background-color: black;
    /* width: 100%;
    height: 100%; */
}
.done {
  text-decoration: line-through;
}
</style>