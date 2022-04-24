<template>
  <button class="calculator--btn" @click="onClick(content)">
    {{ content }}
  </button>
</template>

<script>
export default {
  name: "NumberButton",
  props: {
    onClick: Function,
    content: Number
  }
}
</script>