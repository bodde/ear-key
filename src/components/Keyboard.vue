<template>
  <button @click="reset()">Reset</button>
  <hr />
  <div class="fx-layout-col fx-vertical-gap">
    <div class="fx-layout-col" @keydown.prevent="playKey($event)" tabindex="0">
      <div class="app-black-keys fx-layout-row">
        <template v-for="(note, index) in sharpNotes">
          <key
            :note="note"
            :sharp="true"
            :selected="selectedNotes.includes(note)"
            :matchesScale="
              selectedScaleKey && selectedScaleKey.scale.includes(note)
            "
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
          :matchesScale="
            selectedScaleKey && selectedScaleKey.scale.includes(note)
          "
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
          :minor="true"
          :code="key.code"
          :selected="key === selectedScaleKey"
          :score="key.score || 0"
          @click="select(key)"
        />
      </div>
      <div class="app-scale fx-layout-row">
        <scale-key
          v-for="(key, index) in scales.major"
          :key="key"
          :note="key.note"
          :minor="false"
          :code="key.code"
          :selected="key === selectedScaleKey"
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
      selectedScaleKey: null,
      scales: {
        minor: [
          { code: '01A', note: 'G#', scale: ['G#', 'B', 'C#', 'D#', 'F#'] },
          { code: '02A', note: 'D#', scale: ['D#', 'F#', 'G#', 'A#', 'C#'] },
          { code: '03A', note: 'A#', scale: ['A#', 'C#', 'D#', 'F', 'G#'] },
          { code: '04A', note: 'F', scale: ['F', 'G#', 'A#', 'C', 'D#'] },
          { code: '05A', note: 'C', scale: ['C', 'D#', 'F', 'G', 'A#'] },
          { code: '06A', note: 'G', scale: ['G', 'A#', 'C', 'D', 'F'] },
          { code: '07A', note: 'D', scale: ['D', 'F', 'G', 'A', 'C'] },
          { code: '08A', note: 'A', scale: ['A', 'C', 'D', 'E', 'G'] },
          { code: '09A', note: 'E', scale: ['E', 'G', 'A', 'B', 'D'] },
          { code: '10A', note: 'B', scale: ['B', 'D', 'E', 'F#', 'A'] },
          { code: '11A', note: 'F#', scale: ['F#', 'A', 'B', 'C#', 'E'] },
          { code: '12A', note: 'C#', scale: ['C#', 'E', 'F#', 'G#', 'B'] },
        ],
        major: [
          { code: '01B', note: 'B', scale: ['B', 'C#', 'D#', 'F#', 'G#'] },
          { code: '02B', note: 'F#', scale: ['F#', 'G#', 'A#', 'C#', 'D#'] },
          { code: '03B', note: 'C#', scale: ['C#', 'D#', 'F', 'G#', 'A#'] },
          { code: '04B', note: 'G#', scale: ['G#', 'A#', 'C', 'D#', 'F'] },
          { code: '05B', note: 'D#', scale: ['D#', 'F', 'G', 'A#', 'C'] },
          { code: '06B', note: 'A#', scale: ['A#', 'C', 'D', 'F', 'G'] },
          { code: '07B', note: 'F', scale: ['F', 'G', 'A', 'C', 'D'] },
          { code: '08B', note: 'C', scale: ['C', 'D', 'E', 'G', 'A'] },
          { code: '09B', note: 'G', scale: ['G', 'A', 'B', 'D', 'E'] },
          { code: '10B', note: 'D', scale: ['D', 'E', 'F#', 'A', 'B'] },
          { code: '11B', note: 'A', scale: ['A', 'B', 'C#', 'E', 'F#'] },
          { code: '12B', note: 'E', scale: ['E', 'F#', 'G#', 'B', 'C#'] },
        ],
      },
      keyNotesMap: {
        KeyA: 'C',
        KeyW: 'C#',
        KeyS: 'D',
        KeyE: 'D#',
        KeyD: 'E',
        KeyF: 'F',
        KeyT: 'F#',
        KeyG: 'G',
        KeyY: 'G#',
        KeyH: 'A',
        KeyU: 'A#',
        KeyJ: 'B',
      },
    };
  },
  methods: {
    reset: function () {
      this.selectedScaleKey = null;
      this.selectedNotes = [];
      const allKeys = [...this.scales.minor, ...this.scales.major];
      allKeys.forEach((scaleKey) => (scaleKey.score = 0));
    },
    select: function (scaleKey) {
      this.selectedScaleKey = scaleKey;
    },
    play: function (note) {
      const octave = 4;
      this.synth.triggerAttackRelease(note + octave, '8n');
    },
    playKey: function (event) {
      console.log(event);
      const note = this.keyNotesMap[event.code];
      if (note) {
        this.play(note);
      }
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

.app-scalekey-selected-indicator {
  border: 2px solid white;
}

.app-scalekey-selected-indicator.on {
  border-color: yellow;
}
</style>
