<template>
  <div>
    <!-- Header -->
    <app-header />

    <!-- Main content -->
    <router-view />

  </div>
</template>

<script>
import AppHeader from '../../frontend/src/components/global/AppHeader'

export default {
  components: {
    AppHeader,
  }
}
</script>