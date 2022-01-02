<template>
  <div>{{ selectedScale && selectedScale.note }}</div>
  <div class="fx-layout-col fx-vertical-gap">
    <div class="fx-layout-col">
      <div class="app-black-keys fx-layout-row">
        <template v-for="(note, index) in sharpNotes">
          <key
            :note="note"
            :sharp="true"
            :selected="selectedNotes.includes(note)"
            @click="play(note)"
            @contextmenu.prevent="toggleNote(note)"
          />
        </template>
      </div>
      <div class="fx-layout-row">
        <key
          v-for="(note, index) in notes"
          :note="note"
          :selected="selectedNotes.includes(note)"
          @click="play(note)"
          @contextmenu.prevent="toggleNote(note)"
        />
      </div>
    </div>
    <div class="fx-layout-col">
      <div class="app-scale fx-layout-row">
        <scale-key
          v-for="(key, index) in scales.minor"
          :note="key.note"
          :code="(index + 1).toString() + 'A'"
          :selected="key === selectedScale"
          :score="key.score || 0"
          @click="select(key)"
        />
      </div>
      <div class="app-scale fx-layout-row">
        <scale-key
          v-for="(key, index) in scales.major"
          :key="key"
          :note="key.note"
          :code="(index + 1).toString() + 'B'"
          :selected="key === selectedScale"
          :score="key.score || 0"
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
      selectedNotes: [],
      selectedScale: null,
      scales: {
        minor: [
          { note: 'G#', scale: ['G#', 'B', 'C#', 'D#', 'F#'] },
          { note: 'D#', scale: ['D#', 'F#', 'G#', 'A#', 'C#'] },
          { note: 'A#', scale: ['A#', 'C#', 'D#', 'F', 'G#'] },
          { note: 'F', scale: ['F', 'G#', 'A#', 'C', 'D#'] },
          { note: 'C', scale: ['C', 'D#', 'F', 'G', 'A#'] },
          { note: 'G', scale: ['G', 'A#', 'C', 'D', 'F'] },
          { note: 'D', scale: ['D', 'F', 'G', 'A', 'C'] },
          { note: 'A', scale: ['A', 'C', 'D', 'E', 'G'] },
          { note: 'E', scale: ['E', 'G', 'A', 'B', 'D'] },
          { note: 'B', scale: ['B', 'D', 'E', 'F#', 'A'] },
          { note: 'F#', scale: ['F#', 'A', 'B', 'C#', 'E'] },
          { note: 'C#', scale: ['C#', 'E', 'F#', 'G#', 'B'] },
        ],
        major: [
          { note: 'B', scale: ['B', 'C#', 'D#', 'F#', 'G#'] },
          { note: 'F#', scale: ['F#', 'G#', 'A#', 'C#', 'D#'] },
          { note: 'C#', scale: ['C#', 'D#', 'F', 'G#', 'A#'] },
          { note: 'G#', scale: ['G#', 'A#', 'C', 'D#', 'F'] },
          { note: 'D#', scale: ['D#', 'F', 'G', 'A#', 'C'] },
          { note: 'A#', scale: ['A#', 'C', 'D', 'F', 'G'] },
          { note: 'F', scale: ['F', 'G', 'A', 'C', 'D'] },
          { note: 'C', scale: ['C', 'D', 'E', 'G', 'A'] },
          { note: 'G', scale: ['G', 'A', 'B', 'D', 'E'] },
          { note: 'D', scale: ['D', 'E', 'F#', 'A', 'B'] },
          { note: 'A', scale: ['A', 'B', 'C#', 'E', 'F#'] },
          { note: 'E', scale: ['E', 'F#', 'G#', 'B', 'C#'] },
        ],
      },
    };
  },
  methods: {
    select: function (scaleKey) {
      this.selectedScale = scaleKey;
    },
    play: function (note) {
      const octave = 4;
      this.synth.triggerAttackRelease(note + octave, '8n');
    },
    toggleNote: function (note) {
      const selectedNoteIndex = this.selectedNotes.indexOf(note);
      if (selectedNoteIndex >= 0) {
        this.selectedNotes.splice(selectedNoteIndex, 1);
      } else {
        this.selectedNotes.push(note);
      }

      const allKeys = [...this.scales.minor, ...this.scales.major];
      allKeys.forEach(
        (scaleKey) =>
          (scaleKey.score = scaleKey.scale.filter((note) =>
            this.selectedNotes.includes(note)
          ).length)
      );
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
