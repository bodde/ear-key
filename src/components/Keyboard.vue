<template>
  <div class="fx-layout-col">
    <div class="fx-layout-col"></div>

    <div class="fx-layout-col">
      <div class="app-scale fx-layout-row">
        <scale-key
          v-for="(key, index) in keys.minor"
          :note="key.note"
          :code="(index + 1).toString() + 'A'"
          :selected="key.selected"
          @click="select(key, 'minor')"
        />
      </div>
      <div class="app-scale fx-layout-row">
        <scale-key
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
import ScaleKey from './ScaleKey.vue';
import { Sampler, Transport, Synth, PolySynth } from 'tone';

export default {
  name: 'Keyboard',
  components: {
    ScaleKey,
  },
  created: function () {
    this.synth = new Synth().toDestination();
    console.log(this.synth);
  },
  data: function () {
    return {
      notes: ['C', 'D', 'E', 'F', 'G', 'A', 'B'],
      sharpNotes: ['C#', 'D#', 'F#', 'G#', 'A#'],
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
    select: function (key, scale) {
      const allKeys = this.keys.minor.concat(this.keys.major);

      allKeys.filter((_) => _.selected).forEach((_) => (_.selected = false));

      const selectedKey = this.keys[scale].find((_) => _.note == key.note);
      selectedKey.selected = true;

      const octave = 4;
      this.synth.triggerAttackRelease(selectedKey.note + octave, '8n');
    },
  },
};
</script>

<style>
.fx-layout-row {
  display: flex;
  flex-direction: row;
}

.fx-layout-col {
  display: flex;
  flex-direction: column;
}

.app-scale:first-child .app-scale-key {
  border-bottom: 0;
}
.app-scale .app-scale-key:not(:first-child) {
  border-left: 0;
}
</style>
