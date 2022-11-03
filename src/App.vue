<script setup>
import { ref } from "vue";

const modalShow = ref(false);
const newNote = ref("");
const errorMessage = ref("");
const notes = ref([]);

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}

const addNote = () => {
  if (newNote.value.trim.length < 10) {
    return (errorMessage.value = "needs to be ten character");
  }

  notes.value.push({
    id: Math.floor(Math.random() * 1000000),
    text: newNote.value,
    date: new Date(),
    backgroundColor: getRandomColor(),
  });
  modalShow.value = false;
  newNote.value = "";
  errorMessage.value = "";
};
</script>


<template>
  <main>
    <div v-show="modalShow" class="all-container">
      <div class="modal">
        <textarea
          v-model="newNote"
          name="notes"
          id="notes"
          cols="20"
          rows="12"
        ></textarea>
        <p v-if="errorMessage">{{ errorMessage }}</p>
        <button @click="addNote">Add Note</button>
        <button class="close" @click="modalShow = false">Close</button>
      </div>
    </div>

    <div class="container">
      <header>
        <h2>Notes</h2>
        <button @click="modalShow = true">+</button>
      </header>
      <div class="card-container">
        <div
          v-for="note in notes"
          :key="note.id"
          class="card"
          :style="{ backgroundColor: note.backgroundColor }"
        >
          <p class="p-main">{{ note.text }}</p>
          <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  height: 100vh;
  width: 100vw;
}
.container {
  max-width: 800px;
  padding: 10px;
  margin: 0 auto;
}
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
h2 {
  font-weight: bold;
  margin-bottom: 20px;
  font-size: 50px;
}
header button {
  width: 40px;
  height: 40px;
  border-color: blueviolet;
  cursor: pointer;
  background-color: black;
  border-radius: 100%;
  color: cyan;
}
.card {
  width: 150px;
  height: 150px;
  background-color: rgb(255, 255, 150);
  padding: 10px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 17px;
  margin-bottom: 17px;
}
.date {
  font-size: 12px;
  flex-wrap: wrap;
}
.card-container {
  display: flex;
  flex-wrap: wrap;
}
.all-container {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgb(126, 123, 123);
  z-index: 9999;
  display: flex;
  align-items: center;
  justify-content: center;
}
.modal {
  width: 550px;
  background-color: white;
  border-radius: 10px;
  padding: 25px;
  position: relative;
  display: flex;
  flex-direction: column;
}
.modal button {
  padding: 10px 20px;
  font-size: 13px;
  width: 100%;
  background-color: blueviolet;
  border: none;
  color: aqua;
  cursor: pointer;
  margin-top: 10px;
}
.modal .close {
  background-color: rgb(180, 7, 7);
}
.modal p {
  color: red;
}
</style>