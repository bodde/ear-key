<template>
  <div class="app-key">
    <span class="app-key-code">{{ code }}</span>
    <small class="app-key-name">{{ name }}</small>
  </div>
</template>

<script>
export default {
  name: 'Key',
  props: {
    name: String,
    code: String,
  },
};
</script>

<style scoped>
.app-key {
  font-size: 14px;
  padding: 4px;
  width: 40px;
  height: 40px;
  border-color: black;
  border-style: solid;
  border-width: 0 1px 1px 1px;
  position: relative;
  cursor: pointer;
}

.app-key:hover {
  box-shadow: 0 0 5px black;
}

.app-key:first-child {
  border-width: 1px;
}

.app-key-code {
}

.app-key-name {
  color: gray;
  position: absolute;
  bottom: 4px;
  right: 4px;
}
</style>
