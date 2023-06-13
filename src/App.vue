<template>
  <main>
    <div class="overlay" v-if="showCloseModal">
      <div class="modal">
        <textarea v-model="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <button @click="addNote">Add Note</button>
        <button class="close" @click="closeModal">Close</button>
      </div>
    </div>

    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="openModal">+</button>
      </header>

      <div class="card-container">
        <div v-for="(note, index) in notes" :key="index" class="card" :style="{backgroundColor: note.backgroundColor}">
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
        </div>
      </div>

    </div>
  </main>
</template>

<script setup>
import { ref } from "vue";

const showCloseModal = ref(false);
const newNote = ref("");
const notes = ref([]);

const openModal = () => {
  showCloseModal.value = true;
}

const closeModal = () => {
  showCloseModal.value = false;
}

const getRandomColor = () => {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}

const addNote = () => {
  notes.value.push({
    id: Math.floor(Math.random() * 100000),
    text: (newNote.value).substring(0, 150) + '...',
    date: new Date(),
    backgroundColor: getRandomColor()
  });

  showCloseModal.value = false;
  newNote.value = "";
}

</script>

<style src="./assets/main.css"></style>
<style scoped>
  main{
    width: 100%;
    height: 100vh;
  }

  .container{
    max-width: 1075px;
    padding: 10px;
    margin: 0 auto;
  }

  header{
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  h1{
    font-weight: bold;
    margin-bottom: 25px;
    font-size: 75px;
  }

  header button{
    border: none;
    padding: 10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    border-radius: 100%;
    background-color: #000;
    color: #fff;
  }

  .card-container{
    display: flex;
    flex-wrap: wrap;
  }

  .card{
    width: 225px;
    height: 225px;
    background-color: orange;
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;
  }

  .date{
    font-size: 12.5px;
    font-weight: bold;
  }

  .overlay{
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0,0,0,0.77);
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .modal{
    width: 750px;
    background-color: #fff;
    border-radius: 10px;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;
  }

  .modal button{
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: blueviolet;
    border: none;
    color: #fff;
    cursor: pointer;
    margin-top: 15px;
  }

  .modal .close{
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: crimson;
    border: none;
    color: #fff;
    cursor: pointer;
    margin-top: 15px;
  }
</style>