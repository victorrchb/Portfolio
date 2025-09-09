<template>
  <v-app>
    <DottedParallax />
  </v-app>
</template>

<script lang="ts" setup>
  import DottedParallax from '@/components/DottedParallax.vue'
</script>

<style scoped>
:deep(.v-application) { min-height: 100vh; background: transparent; }
</style>
