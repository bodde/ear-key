<template>
  <div class="app-keyboard">
    <div class="app-keysets">
      <div class="app-keyset">
        <Key
          v-for="(key, index) in keys.minor"
          :name="key.note"
          :code="(index + 1).toString() + 'A'"
        />
      </div>
      <div class="app-keyset">
        <Key
          v-for="(key, index) in keys.major"
          :name="key.note"
          :code="(index + 1).toString() + 'B'"
        />
      </div>
    </div>
  </div>
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
        minor: [
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
        major: [
          { note: 'B', scale: [] },
          { note: 'F#', scale: [] },
          { note: 'C#', scale: [] },
          { note: 'G#', scale: [] },
          { note: 'D#', scale: [] },
          { note: 'A#', scale: [] },
          { note: 'F', scale: [] },
          { note: 'C', scale: [] },
          { note: 'G', scale: [] },
          { note: 'D', scale: [] },
          { note: 'A', scale: [] },
          { note: 'E', scale: [] },
        ],
      },
    };
  },
};
</script>

<style scoped>
.app-keyboard {
  display: flex;
  flex-direction: row;
}

.app-keysets {
  display: flex;
  flex-direction: row;
}

.app-keyset {
  display: flex;
  flex-direction: column;
}

.app-keyset:first-child .app-key {
  border-right: 0;
}
</style>
