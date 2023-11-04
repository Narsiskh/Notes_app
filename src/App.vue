<script setup>
import {ref} from "vue";

const showModal = ref(false);
const newNote = ref("");
const errorMessage = ref("")
const notes = ref([]);

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}

const addNote =() => {
  if (newNote.value.length < 10){
    return errorMessage.value = "Note needs to be 10 characters or more"
  }
  notes.value.push({
    id: Math.floor(Math.random() * 1000000),
    text: newNote.value,
    date: new  Date(),
    backgroundColor: getRandomColor()
  });
  showModal.value = false
  newNote.value = ""
}
</script>

<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <P v-if="errorMessage">{{ errorMessage }}</P>
        <button @click="addNote">Add Note</button>
        <button class="close" @click="showModal = false">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button class="add" @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div v-for="note in notes" class="card" :style="{backgroundColor: note.backgroundColor}" :key="note.id">
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style src="./assets/style.sass" scoped lang="sass"></style>