<template>
  <div>
    <div
      v-if="sharp"
      class="app-key-selected-indicator"
      :class="{ on: selected }"
    ></div>
    <div class="app-key" :class="{ sharp: sharp, placeholder: !note }">
      <span class="app-key-note">{{ note }}</span>
    </div>
    <div
      v-if="!sharp"
      class="app-key-selected-indicator"
      :class="{ on: selected }"
    ></div>
  </div>
</template>

<script>
export default {
  name: 'Key',
  props: {
    note: String,
    sharp: Boolean,
    selected: Boolean,
  },
};
</script>

<style>
.app-key {
  font-size: 14px;
  min-width: 40px;
  height: 40px;
  border: 1px solid black;
  position: relative;
  cursor: pointer;
}

.app-key.placeholder {
  visibility: hidden;
}

.app-key:hover {
  box-shadow: 0 0 5px black;
}

.app-key.sharp {
  background-color: #222;
  color: white;
}

.app-key-note {
  position: absolute;
  bottom: 4px;
  text-align: center;
  width: 100%;
}

.app-key-selected-indicator {
  border: 2px solid white;
}

.app-key-selected-indicator.on {
  border-color: green;
}
</style>
