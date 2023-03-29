<template>
  <p class="py-4">{{ content }}</p>
</template>

<script>
export default {
  props: {
    content: {
      type: String
    }
  }
}
</script>