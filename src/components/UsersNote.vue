<template>
  <!-- iterate each note item -->
  <div class="Notes-item" v-for="(note, index) in noteItems" :key='index'>
    <p>{{ note }}</p> <!-- print note value -->
    <button type="button" @click="deleteNote(index)">X</button> <!-- button for delete note -->
  </div>
</template>

<script>
export default {
  name: 'UsersNote',
  props: {
    noteItems: {
      type: Array,
      required: true,
    },
    deleteNote: {
      type: Function,
      required: true,
    },
  },
};
</script>
