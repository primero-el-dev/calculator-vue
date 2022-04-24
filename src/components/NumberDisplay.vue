<template>
  <div class="display">
    {{ content }}
  </div>
</template>

<script>
export default {
  name: "NumberDisplay",
  props: {
    content: String
  }
}
</script>