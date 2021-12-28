<template>
  <div class="app-key" :class="{ selected: selected }">
    <span class="app-key-code">{{ code }}</span>
    <small class="app-key-note">{{ note }}</small>
  </div>
</template>

<script>
export default {
  name: 'Key',
  props: {
    note: String,
    code: String,
    selected: Boolean,
  },
};
</script>

<style scoped>
.app-key {
  font-size: 14px;
  padding: 4px;
  min-width: 40px;
  height: 40px;
  border: 1px solid black;
  position: relative;
  cursor: pointer;
}

.app-key:hover {
  box-shadow: 0 0 5px black;
}

.app-key.selected {
  background-color: aqua;
}

.app-key:first-child {
  border-width: 1px;
}

.app-key-code {
}

.app-key-note {
  color: gray;
  position: absolute;
  bottom: 4px;
  right: 4px;
}
</style>
