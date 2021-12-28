<template>
  <div class="fx-layout-col fx-vertical-gap">
    <div class="fx-layout-col">
      <div class="app-black-keys fx-layout-row">
        <template v-for="(note, index) in sharpNotes">
          <key :note="note" :sharp="true" @click="play(note)" />
        </template>
      </div>
      <div class="fx-layout-row">
        <key v-for="(note, index) in notes" :note="note" @click="play(note)" />
      </div>
    </div>
    <div class="fx-layout-col">
      <div class="app-scale fx-layout-row">
        <scale-key
          v-for="(key, index) in scales.minor"
          :note="key.note"
          :code="(index + 1).toString() + 'A'"
          :selected="key.selected"
          @click="select(key)"
        />
      </div>
      <div class="app-scale fx-layout-row">
        <scale-key
          v-for="(key, index) in scales.major"
          :key="key"
          :note="key.note"
          :code="(index + 1).toString() + 'B'"
          :selected="key.selected"
          @click="select(key)"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Key from './Key.vue';
import ScaleKey from './ScaleKey.vue';
import { Sampler, Transport, Synth, PolySynth } from 'tone';

export default {
  name: 'Keyboard',
  components: {
    Key,
    ScaleKey,
  },
  created: function () {
    this.synth = new Synth().toDestination();
    console.log(this.synth);
  },
  data: function () {
    return {
      notes: ['C', 'D', 'E', 'F', 'G', 'A', 'B'],
      sharpNotes: ['C#', 'D#', null, 'F#', 'G#', 'A#'],
      scales: {
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
    select: function (scaleKey) {
      const allKeys = [...this.scales.minor, ...this.scales.major];

      allKeys.filter((_) => _.selected).forEach((_) => (_.selected = false));

      scaleKey.selected = true;
    },
    play: function (note) {
      const octave = 4;
      this.synth.triggerAttackRelease(note + octave, '8n');
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

.fx-vertical-gap > *:not(:first-child) {
  margin-top: 8px;
}

.app-key:not(:first-child) {
  border-left: 0;
}

.app-black-keys {
  margin-left: 20px;
}

.app-scale:first-child .app-scale-key,
.app-black-keys .app-key {
  border-bottom: 0;
}

.app-scale .app-scale-key:not(:first-child) {
  border-left: 0;
}
</style>
