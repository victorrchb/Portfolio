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
  let isLowPerformance = false
  let lastFrameTime = 0

  // Variables locales pour l'optimisation de performance
  let optimizedGap = props.gap
  let optimizedDotSize = props.dotSize

  function onPointerMove (e: MouseEvent) {
    // Position absolue sur la page (et pas uniquement dans le viewport)
    mouseX = e.clientX + window.scrollX
    mouseY = e.clientY + window.scrollY
  }

  function detectPerformance () {
    // Détection basique de performance pour les appareils mobiles
    const isMobile = /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent)
    const isLowEnd = navigator.hardwareConcurrency && navigator.hardwareConcurrency < 4

    // Vérification sécurisée de la connexion
    let isSlowConnection = false
    if ('connection' in navigator) {
      const connection = (navigator as any).connection
      isSlowConnection = connection && connection.effectiveType
        && ['slow-2g', '2g', '3g'].includes(connection.effectiveType)
    }

    return isMobile || isLowEnd || isSlowConnection
  }

  function optimizeForPerformance () {
    isLowPerformance = detectPerformance()

    // Vérifier si l'utilisateur préfère la réduction de mouvement
    const prefersReducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches

    // Initialiser avec les valeurs des props
    optimizedGap = props.gap
    optimizedDotSize = props.dotSize

    if (isLowPerformance) {
      // Réduire la densité des points sur les appareils moins performants
      optimizedGap = Math.max(optimizedGap, 32)
      optimizedDotSize = Math.max(optimizedDotSize, 1.5)
    }

    if (prefersReducedMotion) {
      // Désactiver l'animation pour les utilisateurs qui préfèrent la réduction de mouvement
      isLowPerformance = true
      optimizedGap = Math.max(optimizedGap, 40)
    }
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

    // Gestion de performance - limiter le framerate sur les appareils moins performants
    const now = performance.now()
    if (isLowPerformance && now - lastFrameTime < 16) {
      rafId = requestAnimationFrame(draw)
      return
    }
    lastFrameTime = now

    const { radius, strength } = props
    const gap = optimizedGap
    const dotSize = optimizedDotSize
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
    const time = Date.now() * (isLowPerformance ? 0.0005 : 0.0008) // Vitesse adaptée à la performance

    // Optimisation : réduire le nombre de calculs sur les appareils moins performants
    const animationIntensity = isLowPerformance ? 0.6 : 1

    for (let y = startY; y <= h + gap; y += gap) {
      for (let x = startX; x <= w + gap; x += gap) {
        const dx = x - mouseX
        const dy = y - mouseY
        const dist = Math.hypot(dx, dy)
        let offX = 0
        let offY = 0

        // Animation de flottement plus naturelle avec plusieurs couches
        const baseFloatX = Math.sin(time * 0.4 + x * 0.008) * 1.2 * animationIntensity
        const baseFloatY = Math.cos(time * 0.3 + y * 0.008) * 1.2 * animationIntensity

        // Ajout d'une couche de micro-mouvement pour plus de réalisme (réduit sur mobile)
        const microFloatX = Math.sin(time * 1.2 + x * 0.02) * 0.3 * animationIntensity
        const microFloatY = Math.cos(time * 0.8 + y * 0.02) * 0.3 * animationIntensity

        // Combinaison des mouvements pour un effet plus organique
        const floatX = baseFloatX + microFloatX
        const floatY = baseFloatY + microFloatY

        if (dist < radius) {
          const t = 1 - dist / radius
          const bend = (t * t) * (3 - 2 * t)
          const normX = dx / (dist || 1)
          const normY = dy / (dist || 1)
          const amp = strength * bend
          offX = -normY * amp + floatX
          offY = normX * amp + floatY
        } else {
          // Appliquer le flottement même en dehors du rayon de la souris
          offX = floatX
          offY = floatY
        }

        // Ajout d'une légère variation de taille pour plus de dynamisme (réduite sur mobile)
        const sizeVariation = isLowPerformance ? 1 : (1 + Math.sin(time * 0.6 + x * 0.01 + y * 0.01) * 0.1)
        const currentDotSize = dotSize * sizeVariation

        ctx.beginPath()
        ctx.arc(x + offX, y + offY, currentDotSize, 0, Math.PI * 2)
        ctx.fill()
      }
    }
    rafId = requestAnimationFrame(draw)
  }

  onMounted(() => {
    optimizeForPerformance()
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
    /* Optimisations pour la performance */
    will-change: transform;
    transform: translateZ(0); /* Force l'accélération matérielle */
    backface-visibility: hidden;
    /* Amélioration de la qualité de rendu */
    image-rendering: -webkit-optimize-contrast;
    image-rendering: crisp-edges;
    image-rendering: pixelated;
  }

  /* Optimisations pour les appareils mobiles */
  @media (max-width: 768px) {
    .dots-canvas {
      /* Réduction de la hauteur sur mobile pour économiser les ressources */
      height: 150vh;
    }
  }

  /* Optimisations pour les appareils très petits */
  @media (max-width: 480px) {
    .dots-canvas {
      height: 120vh;
    }
  }

  /* Désactivation de l'animation sur les appareils qui préfèrent la réduction de mouvement */
  @media (prefers-reduced-motion: reduce) {
    .dots-canvas {
      animation: none;
    }
  }
</style>
