<template>
  <canvas ref="canvasEl" aria-hidden="true" class="dots-canvas" />
</template>

<script lang="ts" setup>
  import { onBeforeUnmount, onMounted, ref } from 'vue'

  const props = withDefaults(
    defineProps<{
      gap?: number
      dotSize?: number
      color?: string
      background?: string
      radius?: number
      strength?: number
    }>(),
    {
      gap: 24,
      dotSize: 2,
      color: 'rgba(255,255,255,0.12)',
      background: '#0b0d10',
      radius: 180,
      strength: 28,
    },
  )

  const canvasEl = ref<HTMLCanvasElement | null>(null)
  let ctx: CanvasRenderingContext2D | null = null
  let rafId = 0
  let mouseX = window.innerWidth / 2
  let mouseY = window.innerHeight / 2

  function onPointerMove (e: MouseEvent) {
    mouseX = e.clientX
    mouseY = e.clientY
  }

  function resizeCanvas () {
    const c = canvasEl.value
    if (!c) return
    const dpr = Math.max(1, window.devicePixelRatio || 1)
    c.width = Math.floor(window.innerWidth * dpr)
    c.height = Math.floor(window.innerHeight * dpr)
    c.style.width = `${window.innerWidth}px`
    c.style.height = `${window.innerHeight}px`
    ctx = c.getContext('2d')
    if (ctx) ctx.setTransform(dpr, 0, 0, dpr, 0, 0)
  }

  function draw () {
    if (!ctx) return
    const { gap, dotSize, color, background, radius, strength } = props
    const w = window.innerWidth
    const h = window.innerHeight
    ctx.clearRect(0, 0, w, h)
    ctx.fillStyle = background
    ctx.fillRect(0, 0, w, h)

    ctx.fillStyle = color
    const startX = -((w % gap) / 2)
    const startY = -((h % gap) / 2)

    for (let y = startY; y <= h + gap; y += gap) {
      for (let x = startX; x <= w + gap; x += gap) {
        const dx = x - mouseX
        const dy = y - mouseY
        const dist = Math.hypot(dx, dy)
        let offX = 0
        let offY = 0
        if (dist < radius) {
          const t = 1 - dist / radius
          const bend = (t * t) * (3 - 2 * t)
          const normX = dx / (dist || 1)
          const normY = dy / (dist || 1)
          const amp = strength * bend
          offX = -normY * amp
          offY = normX * amp
        }
        ctx.beginPath()
        ctx.arc(x + offX, y + offY, dotSize, 0, Math.PI * 2)
        ctx.fill()
      }
    }
    rafId = requestAnimationFrame(draw)
  }

  onMounted(() => {
    resizeCanvas()
    window.addEventListener('resize', resizeCanvas)
    window.addEventListener('mousemove', onPointerMove, { passive: true })
    rafId = requestAnimationFrame(draw)
  })

  onBeforeUnmount(() => {
    window.removeEventListener('resize', resizeCanvas)
    window.removeEventListener('mousemove', onPointerMove)
    if (rafId) cancelAnimationFrame(rafId)
  })
</script>

<style scoped>
  .dots-canvas {
    position: fixed;
    inset: 0;
    z-index: 0;
    display: block;
    width: 100vw;
    height: 100vh;
    pointer-events: none;
  }
</style>
