<template>
  <div>
    <div class="app-key" :class="{ sharp: sharp, placeholder: !note }">
      <div class="app-key-selector-area" class="fx-layout-row">
        <div class="app-key-selected-indicator" :class="{ on: selected }"></div>
      </div>
      <span class="app-key-note">{{ note }}</span>
    </div>
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

.app-key-selector-area {
  height: 4px;
  width: 80%;
  margin-top: 1px;
  margin-left: auto;
  margin-right: auto;
}

.app-key-selected-indicator.on {
  background-color: green;
  height: 100%;
  width: 100%;
}
</style>
