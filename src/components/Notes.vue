<template>
  <div class="Notes">
    <div class="container">
      <div class="Notes__inner">
        <div class="Notes-add">
          <label for="add">Add note:</label>
          <input minlength="5" type="text" id="add" name="add" placeholder="My note." v-model="newNote" />
          <button type="button" @click="addNote()">+</button> <!-- button for add note -->
        </div>
        <div class="Notes-elements">
          <UsersNote :noteItems="noteItems" :deleteNote="deleteNote" /> <!-- set delete function and note items array -->
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import UsersNote from './UsersNote.vue'; // import note cards

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Notes',
  components: {
    // imports
    UsersNote,
  },
  data() {
    return {
      noteItems: [], // array of notes
      newNote: '', // initial value of new note text
    };
  },
  // functions
  methods: {
    addNote() {
      if (this.newNote.length < 5) {
        alert('Note cannot be less than 5 characters.');
      } else if (this.newNote.length > 100) {
        alert('Note cannot be greater than 100 characters.');
      } else {
        this.noteItems.push(this.newNote);
        this.newNote = '';
        this.saveNotes(); // save note in localStorage
      }
    },
    deleteNote(index) {
      this.noteItems.splice(index, 1); // delete note by index
      this.saveNotes(); // delete note from localStorage
    },
    saveNotes() {
      localStorage.setItem('noteItems', JSON.stringify(this.noteItems)); // add item to localStorage
    },
    loadNotes() {
      const notes = localStorage.getItem('noteItems'); // get note items
      if (notes) {
        this.noteItems = JSON.parse(notes); // parse (JSON)
      }
    },
  },
  // call after component load
  mounted() {
    this.loadNotes();
  },
};
</script>
