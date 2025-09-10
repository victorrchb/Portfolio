<template>
  <!-- Composant sans UI: gère le curseur via document.body.style.cursor -->
  <div aria-hidden="true" style="display:none"></div>
</template>

<script lang="ts" setup>
  import { onBeforeUnmount, onMounted } from 'vue'

  type CursorState =
    | 'default'
    | 'pointer'
    | 'text'
    | 'help'
    | 'not-allowed'
    | 'move'
    | 'precision'
    | 'ew-resize'
    | 'ns-resize'
    | 'nwse-resize'
    | 'nesw-resize'

  function asset (path: string): string {
    return new URL(`../assets/windows-11-black-and-white-/${path}`, import.meta.url).toString()
}

  // Hotspot (x y) en pixels pour les .cur (0,0 par défaut). Ajustable si besoin.
const HS = { x: 0, y: 0 }

  const map: Record<CursorState, string> = {
    'default': `url(${asset('Pointer.cur')}) ${HS.x} ${HS.y}, auto`,
    'pointer': `url(${asset('Link.cur')}) ${HS.x} ${HS.y}, pointer`,
    'text': `url(${asset('Text.cur')}) ${HS.x} ${HS.y}, text`,
    'help': `url(${asset('Help.cur')}) ${HS.x} ${HS.y}, help`,
    'not-allowed': `url(${asset('Unavailable.cur')}) ${HS.x} ${HS.y}, not-allowed`,
    'move': `url(${asset('Move.cur')}) ${HS.x} ${HS.y}, move`,
    'precision': `url(${asset('Precision.cur')}) ${HS.x} ${HS.y}, crosshair`,
    'ew-resize': `url(${asset('horz.cur')}) ${HS.x} ${HS.y}, ew-resize`,
    'ns-resize': `url(${asset('Vert.cur')}) ${HS.x} ${HS.y}, ns-resize`,
    'nwse-resize': `url(${asset('Dgn1.cur')}) ${HS.x} ${HS.y}, nwse-resize`,
    'nesw-resize': `url(${asset('Dgn2.cur')}) ${HS.x} ${HS.y}, nesw-resize`,
}

function setCursor(state: CursorState) {
  document.body.style.cursor = map[state]
}

function inferCursorFromTarget(target: Element): CursorState {
    // data-cursor override
    const data = (target as HTMLElement).dataset.cursor as CursorState | undefined
    if (data && map[data]) return data

    const tag = target.tagName.toLowerCase()
    const role = (target as HTMLElement).getAttribute('role')
    const disabled = (target as HTMLButtonElement).disabled === true

    if (disabled) return 'not-allowed'
    if (tag === 'a' || tag === 'button' || role === 'button') return 'pointer'
    if (
      tag === 'input' ||
      tag === 'textarea' ||
      (target as HTMLElement).isContentEditable ||
      role === 'textbox'
    ) {
      return 'text'
    }
    // Resize hints via CSS cursor sur l'élément
    const style = getComputedStyle(target as HTMLElement)
    const cssCursor = style.cursor
    if (cssCursor.includes('ew-resize')) return 'ew-resize'
    if (cssCursor.includes('ns-resize')) return 'ns-resize'
    if (cssCursor.includes('nwse-resize')) return 'nwse-resize'
    if (cssCursor.includes('nesw-resize')) return 'nesw-resize'
    if (cssCursor.includes('move') || (target as HTMLElement).draggable) return 'move'

    return 'default'
}

function handlePointerOver(e: PointerEvent) {
  const t = e.target as Element | null
  if (!t) return
  const tag = t.tagName.toLowerCase()
  if (tag === 'img' || tag === 'figure') {
    // Ne change pas le curseur sur les images pour éviter move/drag
    return
  }
  setCursor(inferCursorFromTarget(t))
}

function handlePointerDown() {
  // accentuer certains états au press, si besoin
}

function handlePointerUp(e: PointerEvent) {
  const t = e.target as Element | null
  if (!t) return
  setCursor(inferCursorFromTarget(t))
}

function handleLeaveWindow() {
  setCursor('default')
}

onMounted(() => {
  setCursor('default')
  window.addEventListener('pointerover', handlePointerOver)
  window.addEventListener('pointerdown', handlePointerDown)
  window.addEventListener('pointerup', handlePointerUp)
  window.addEventListener('blur', handleLeaveWindow)
  document.addEventListener('visibilitychange', handleLeaveWindow)
})

onBeforeUnmount(() => {
  window.removeEventListener('pointerover', handlePointerOver)
  window.removeEventListener('pointerdown', handlePointerDown)
  window.removeEventListener('pointerup', handlePointerUp)
  window.removeEventListener('blur', handleLeaveWindow)
  document.removeEventListener('visibilitychange', handleLeaveWindow)
})
</script>

<style scoped>
  /* rien à afficher */
</style>


