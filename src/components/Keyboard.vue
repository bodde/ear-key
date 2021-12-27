<template>
  <div class="app-keyboard">
    <div class="app-keysets">
      <div class="app-keyset">
        <Key
          v-for="(key, index) in keys.minor"
          :note="key.note"
          :code="(index + 1).toString() + 'A'"
          :selected="key.selected"
          @click="select(key, 'minor')"
        />
      </div>
      <div class="app-keyset">
        <Key
          v-for="(key, index) in keys.major"
          :note="key.note"
          :code="(index + 1).toString() + 'B'"
          :selected="key.selected"
          @click="select(key, 'major')"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Key from './Key.vue';
import { Sampler, Transport, Synth, PolySynth } from 'tone';

export default {
  name: 'Keyboard',
  components: {
    Key,
  },
  created: function () {
    this.synth = new Synth().toDestination();
    console.log(this.synth);
  },
  data: function () {
    return {
      keys: {
        minor: [
          { note: 'G#', scale: [], selected: false },
          { note: 'D#', scale: [], selected: false },
          { note: 'A#', scale: [], selected: false },
          { note: 'F', scale: [], selected: false },
          { note: 'C', scale: [], selected: false },
          { note: 'G', scale: [], selected: false },
          { note: 'D', scale: [], selected: false },
          { note: 'A', scale: [], selected: false },
          { note: 'E', scale: [], selected: false },
          { note: 'B', scale: [], selected: false },
          { note: 'F#', scale: [], selected: false },
          { note: 'C#', scale: [], selected: false },
        ],
        major: [
          { note: 'B', scale: [], selected: false },
          { note: 'F#', scale: [], selected: false },
          { note: 'C#', scale: [], selected: false },
          { note: 'G#', scale: [], selected: false },
          { note: 'D#', scale: [], selected: false },
          { note: 'A#', scale: [], selected: false },
          { note: 'F', scale: [], selected: false },
          { note: 'C', scale: [], selected: false },
          { note: 'G', scale: [], selected: false },
          { note: 'D', scale: [], selected: false },
          { note: 'A', scale: [], selected: false },
          { note: 'E', scale: [], selected: false },
        ],
      },
    };
  },
  methods: {
    select: function (key, keyset) {
      const allKeys = this.keys.minor.concat(this.keys.major);

      allKeys.filter((_) => _.selected).forEach((_) => (_.selected = false));

      const selectedKey = this.keys[keyset].find((_) => _.note == key.note);
      selectedKey.selected = true;

      const octave = 4;
      this.synth.triggerAttackRelease(selectedKey.note + octave, '8n');
    },
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
