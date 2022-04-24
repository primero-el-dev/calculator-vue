<template>
  <button class="calculator--btn" @click="onClick()">
    {{ content }}
  </button>
</template>

<script>
export default {
  name: "ActionButton",
  props: {
    onClick: Function,
    content: String
  }
}
</script>

<style scoped>

</style>