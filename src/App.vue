<template>
  <v-app>
    <DottedParallax />
    <CursorManager />
    <div class="content"></div>
  </v-app>
</template>

<script lang="ts" setup>
  import CursorManager from '@/components/CursorManager.vue'
  import DottedParallax from '@/components/DottedParallax.vue'
</script>

<style scoped>
:deep(.v-application) { min-height: 100vh; background: transparent; }
.content { position: relative; z-index: 1; min-height: 100vh; pointer-events: auto; }
</style>
