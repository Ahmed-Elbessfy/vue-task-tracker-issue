<template>
  <button class="btn" :style="{ background: color }" @click="onClick()">
    {{ txt }}
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    txt: {
      type: String,
    },
    color: {
      type: String,
    },
  },
  methods: {
    onClick() {
      this.$emit("btn-click");
    },
  },
};
</script>

<style scoped>
</style>