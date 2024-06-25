<template>
  <div class="Notes-item" v-for="(note, index) in noteItems" :key='index'>
    <p>{{ note }}</p>
    <button type="button" @click="deleteNote(index)">X</button>
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
