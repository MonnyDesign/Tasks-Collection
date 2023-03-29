<template>
  <div class="tab-content" v-if="isActive">
    <slot />
  </div>
</template>

<script>

export default{
  data:() => ({
    isActive: false
  })
}
</script>
