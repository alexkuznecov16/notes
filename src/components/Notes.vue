<template>
  <div class="Notes">
    <div class="container">
      <div class="Notes__inner">
        <div class="Notes-add">
          <label for="add">Add note:</label>
          <input minlength="5" type="text" id="add" name="add" placeholder="My note." v-model="newNote" />
          <button type="button" @click="addNote()">+</button>
        </div>
        <div class="Notes-elements">
          <UsersNote :noteItems="noteItems" :deleteNote="deleteNote" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import UsersNote from './UsersNote.vue';

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Notes',
  components: {
    UsersNote,
  },
  data() {
    return {
      noteItems: [],
      newNote: '',
    };
  },
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
      this.noteItems.splice(index, 1);
      this.saveNotes(); // save note in localStorage
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
  // Вызывается после того, как компонент был смонтирован
  mounted() {
    this.loadNotes();
  },
};
</script>
