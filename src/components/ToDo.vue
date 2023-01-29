<script>
export default {
  data() {
    return {
      toDoList: [],
      isEdit: false,
      newText: "",
      isElement: true,
      checkedToDo:[],
    };
  },
  methods: {
    addNewText() {
      if (this.newText == "") {
        return;
      }
      let newToDo = {
        id: this.toDoList[this.toDoList.length - 1],
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
    deleteText(id) {
      for (let i = 0; i < this.toDoList.length; i++) {
        if (this.toDoList[i].id == id) {
          this.toDoList.splice(i, 1)
        }
      }
    },
    hideText() {
      for (let i = 0; i < this.toDoList.length; i++) {
        if (this.toDoList[i].isDone == true) {
          this.isElement = !this.isElement   
        }
      }
    }
  },
};
</script>

<template>
  <div class="body">
    <div class="header">
      Todo List
    </div>

    <div class="text">
      <b class="mr-650"> {{toDoList.length}} task(s) left</b>
      <button class="hide_btn" @click="hideText()" >Hide Completed</button>
    </div>

    <div class="toDoList">
      <input type="text" v-model="newText" class="input" />
      <button @click="addNewText" class="add_btn">Add</button>
      <div class="info" v-for="toDo in toDoList" v-bind:key="toDo.id" v-show="isElement">
        <input type="checkbox" @click="toggleDone(toDo.id)"/>
          <p :class="{ done: toDo.isDone }">{{ toDo.text }}</p>
          <button class="btn" @click="deleteText(toDo.id)">X</button>
      </div>
    </div>
  </div>
</template>

<style>
body {
  margin: 0;
  background-color: black;
}

.header {
  margin: 3%;
  width: 90%;
  height: 70px;
  background-color: rgba(128, 128, 128, 0.384);
  border: 2px solid gray;
  border-radius: 5px;
  box-sizing: border-box;
  font-size: 40px;
  color: white;
  font-weight: 900;
  display: flex;
  justify-content: center;
  align-items: center;
}

.text {
  width: 90%;
  height: 30px;
  display: flex;
  justify-content: space-between;
  color: white;
  margin: 1% 0% 0% 3%;
}

.mr-650 {
  margin-right: 650px;
}

.input {
  margin: 2% 3%;
  width: 80%;
  height: 40px;
  background-color: rgba(128, 128, 128, 0);
  border: 2px solid gray;
  border-radius: 5px;
  box-sizing: border-box;
  color: white;
}

.add_btn {
  width: 7%;
  height: 40px;
  background-color: rgba(128, 128, 128, 0.384);
  border: 2px solid gray;
  border-radius: 5px;
  box-sizing: border-box;
  font-size: 16px;
  color: white;
  font-weight: 700;
}

.hide_btn{
  width: 15%;
  height: 40px;
  background-color: rgba(128, 128, 128, 0.384);
  border: 2px solid gray;
  border-radius: 5px;
  box-sizing: border-box;
  font-size: 16px;
  color: white;
  font-weight: 700;
}

.info{
  margin: 0 3%;
  padding: 1% 3%;
  width: 90%;
  height: 30%;
  background-color: rgba(128, 128, 128, 0);
  border: 2px solid rgba(128, 128, 128, 0.514);
  border-radius: 5px;
  box-sizing: border-box;
  color: white;
  display: flex;
  justify-content: space-between;
}

.btn{
  background-color: black;
  color: white;
}

p{
  font-size: 20px;
}

.done {
  text-decoration: line-through;
}
</style>