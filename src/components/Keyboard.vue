<template>
  <Key v-for="key in keys.a" :name="key.note" />
  <Key name="C#" />
  <Key name="D" />
</template>

<script>
import Key from './Key.vue';

export default {
  name: 'Keyboard',
  components: {
    Key,
  },
  data: function () {
    return {
      keys: {
        a: [
          { note: 'G#', scale: [] },
          { note: 'D#', scale: [] },
          { note: 'A#', scale: [] },
          { note: 'F', scale: [] },
          { note: 'C', scale: [] },
          { note: 'G', scale: [] },
          { note: 'D', scale: [] },
          { note: 'A', scale: [] },
          { note: 'E', scale: [] },
          { note: 'B', scale: [] },
          { note: 'F#', scale: [] },
          { note: 'C#', scale: [] },
        ],
      },
    };
  },
};
</script>

<style scoped>
div.app-key {
  width: 30px;
  height: 30px;
  border-color: black;
  border-style: solid;
  border-width: 0 1px 1px 1px;
}

div.app-key:first-child {
  border-width: 1px;
}
</style>
