<template>
  <div
    class="app-scale-key"
    :class="{ selected: score == 5 }"
    :style="cssStyle(score)"
  >
    <span class="app-scale-key-code">{{ code }}</span>
    <small class="app-scale-key-note">{{ note }}</small>
    <small class="app-scale-key-score">{{ score }}</small>
  </div>
</template>

<script>
export default {
  name: 'ScaleKey',
  props: {
    note: String,
    code: String,
    selected: Boolean,
    score: Number,
  },
  methods: {
    cssStyle: function (score) {
      const a = (score * 2) / 10;
      return { backgroundColor: `rgba(5, 195, 221,${a})` };
    },
  },
};
</script>

<style>
.app-scale-key {
  font-size: 14px;
  padding: 4px;
  min-width: 40px;
  height: 40px;
  border: 1px solid black;
  position: relative;
  cursor: pointer;
}

.app-scale-key:hover {
  box-shadow: 0 0 10px black;
}

.app-scale-key.selected {
  box-shadow: 0 0 5px yellow;
}

.app-scale-key-code {
}

.app-scale-key-note {
  color: gray;
  position: absolute;
  bottom: 4px;
  right: 4px;
}

.app-scale-key-score {
  color: gray;
  position: absolute;
  bottom: 4px;
  left: 4px;
}
</style>
