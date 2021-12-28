<template>
  <div class="fx-layout-col">
    <div class="fx-layout-col">
      <div class="app-keyset fx-layout-row">
        <Key
          v-for="(key, index) in keys.minor"
          :note="key.note"
          :code="(index + 1).toString() + 'A'"
          :selected="key.selected"
          @click="select(key, 'minor')"
        />
      </div>
      <div class="app-keyset fx-layout-row">
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
.fx-layout-row {
  display: flex;
  flex-direction: row;
}

.fx-layout-col {
  display: flex;
  flex-direction: column;
}

.app-keyset:first-child .app-key {
  border-bottom: 0;
}
.app-keyset .app-key:not(:first-child) {
  border-left: 0;
}
</style>
