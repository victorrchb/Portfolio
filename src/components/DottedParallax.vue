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
      color: '',
      background: '',
      radius: 180,
      strength: 28,
    },
  )

  const canvasEl = ref<HTMLCanvasElement | null>(null)
  let ctx: CanvasRenderingContext2D | null = null
  let rafId = 0
  let mouseX = window.innerWidth / 2
  let mouseY = window.innerHeight / 2
  let dpr = Math.max(1, window.devicePixelRatio || 1)
  let ro: ResizeObserver | null = null

  function onPointerMove (e: MouseEvent) {
    // Position absolue sur la page (et pas uniquement dans le viewport)
    mouseX = e.clientX + window.scrollX
    mouseY = e.clientY + window.scrollY
  }

  function resizeCanvas () {
    const c = canvasEl.value
    if (!c) return
    dpr = Math.max(1, window.devicePixelRatio || 1)
    const doc = document.documentElement
    const w = Math.max(window.innerWidth, doc.scrollWidth)
    const h = Math.max(window.innerHeight, doc.scrollHeight)
    c.width = Math.floor(w * dpr)
    c.height = Math.floor(h * dpr)
    c.style.width = `${w}px`
    c.style.height = `${h}px`
    ctx = c.getContext('2d')
    if (ctx) ctx.setTransform(dpr, 0, 0, dpr, 0, 0)
  }

  function resolveCanvasColors () {
    // Read from CSS variables to sync with theme; fallback to props if provided
    const cs = getComputedStyle(document.documentElement)
    const bgVar = cs.getPropertyValue('--bg-canvas').trim()
    const dotVar = cs.getPropertyValue('--dot-canvas').trim()
    const background = props.background || bgVar || '#0b0d10'
    const color = props.color || dotVar || 'rgba(255,255,255,0.12)'
    return { background, color }
  }

  function draw () {
    if (!ctx) return
    const { gap, dotSize, radius, strength } = props
    const { background, color } = resolveCanvasColors()
    const c = canvasEl.value
    if (!c) return
    const w = c.width / dpr
    const h = c.height / dpr
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
    // Observe content size changes to keep the background covering the full page
    ro = new ResizeObserver(() => resizeCanvas())
    ro.observe(document.body)
    rafId = requestAnimationFrame(draw)
  })

  onBeforeUnmount(() => {
    window.removeEventListener('resize', resizeCanvas)
    window.removeEventListener('mousemove', onPointerMove)
    if (ro) ro.disconnect()
    if (rafId) cancelAnimationFrame(rafId)
  })
</script>

<style scoped>
  .dots-canvas {
    position: absolute;
    left: 0;
    top: 0;
    z-index: 0;
    display: block;
    width: 100vw;
    height: 200vh; /* plus long pour tester le scroll du fond */
    pointer-events: none;
  }
</style>
