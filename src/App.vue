<template>
  <v-app>
    <a class="skip-link" href="#main">Skip to content</a>
    <DottedParallax />
    <CursorManager />
    <div class="controls">
      <button
        aria-label="Toggle day/night theme"
        :aria-pressed="isLight.toString()"
        class="theme-toggle"
        title="Toggle day/night theme"
        @click="toggleTheme"
      >
        <span aria-hidden="true">🌙/☀️</span>
      </button>
      <button
        aria-label="Enable voice synthesis"
        :aria-pressed="voiceEnabled.toString()"
        class="voice-toggle"
        title="Enable voice synthesis"
        @click="toggleVoice"
      >
        <span aria-hidden="true">🔈</span><span class="sr-only">Voice synthesis</span>
      </button>
    </div>
    <main id="main" aria-labelledby="site-title" class="content" role="main">
      <section class="section hero">
        <div class="container">
          <h1 id="site-title" class="title reveal" data-speed="0">Victor Chabeau</h1>
          <p class="subtitle reveal parallax" data-speed="0.25">Creative Front-End Developer</p>
          <p class="lead reveal parallax" data-speed="0.15">
            Web Development student at HETIC (2022 – 2026),<br>
            passionate about front-end development, UI/UX design.<br>
            I design fast, accessible and elegant interfaces with meticulous micro-interactions.
          </p>
        </div>
      </section>

      <section class="section projects">
        <div class="container">
          <h2 class="section-title reveal">Projects & Experience</h2>
          <div class="cards">
            <article class="card reveal project-left">
              <div class="card-media">
                <img alt="Full-Stack Developer - Freelance Project preview" draggable="false" src="/src/assets/img-project/Site-freelance.png">
              </div>
              <div class="card-body">
                <h3 class="card-title">Full-Stack Developer - Freelance Project</h3>
                <p class="card-text">Creation of a complete website from scratch for a client. Design and development of the front-end interface. Implementation of data management and back-end services with Firebase. Creation of a responsive and user-friendly design using Figma.</p>
                <ul class="bullets">
                  <li>Complete front-end and back-end development</li>
                  <li>Firebase integration for data management</li>
                  <li>Responsive and user-friendly design with Figma</li>
                </ul>
                <ul class="tags"><li>JavaScript</li><li>React</li><li>Firebase</li><li>HTML</li><li>CSS</li><li>Figma</li></ul>
              </div>
            </article>

            <article class="card reveal project-right">
              <div class="card-media">
                <img alt="Web Developer - Blockchain - Staky.io preview" draggable="false" src="/src/assets/img-project/Staky.io.jpg">
              </div>
              <div class="card-body">
                <h3 class="card-title">Web Developer - Blockchain - Staky.io</h3>
                <p class="card-text">Development of smart contracts in Solidity (Ethereum) and Rust (Solana). Complete learning of Rust and mastery of blockchain specificities. Contribution to the creation and deployment of decentralized applications (dApps).</p>
                <ul class="bullets">
                  <li>Solidity smart contracts for Ethereum</li>
                  <li>Rust development for Solana</li>
                  <li>Creation and deployment of decentralized applications</li>
                </ul>
                <ul class="tags"><li>Solidity</li><li>Rust</li><li>JavaScript</li><li>HTML</li><li>CSS</li></ul>
              </div>
            </article>

            <article class="card reveal project-left">
              <div class="card-media">
                <img alt="Back-end Developer - Airbnb Clone preview" draggable="false" src="/src/assets/img-project/Airbnb.png">
              </div>
              <div class="card-body">
                <h3 class="card-title">Back-end Developer - Airbnb Clone</h3>
                <p class="card-text">User interface design (design and code). Authentication system and reservation management. Development of a rental platform inspired by Airbnb with complete user and reservation management.</p>
                <ul class="bullets">
                  <li>Complete UI/UX design with Figma</li>
                  <li>Secure authentication system</li>
                  <li>User and reservation management</li>
                </ul>
                <ul class="tags"><li>PHP</li><li>HTML</li><li>CSS</li><li>Figma</li></ul>
              </div>
            </article>

            <article class="card reveal project-right">
              <div class="card-media">
                <div class="image-gallery" @click="openGallery('woodpicker')">
                  <div class="gallery-grid">
                    <img alt="WoodPicker project preview 1" draggable="false" src="/src/assets/img-project/Woodpicker-1.png">
                    <img alt="WoodPicker project preview 2" draggable="false" src="/src/assets/img-project/Woodpicker-2.png">
                    <img alt="WoodPicker project preview 3" draggable="false" src="/src/assets/img-project/Woodpicker-3.png">
                    <img alt="WoodPicker project preview 4" draggable="false" src="/src/assets/img-project/Woodpicker-4.png">
                  </div>
                </div>
              </div>
              <div class="card-body">
                <h3 class="card-title">Web Design - Design MarketPlace (WoodPicker)</h3>
                <p class="card-text">Creation of a design system. Mockup development. Implementation of interactions and Figma assets. Development of a marketplace platform with focus on user experience and visual consistency.</p>
                <ul class="bullets">
                  <li>Complete design system creation</li>
                  <li>Detailed mockup development</li>
                  <li>Implementation of interactions and Figma assets</li>
                </ul>
                <ul class="tags"><li>Figma</li><li>Design System</li><li>UI/UX</li></ul>
              </div>
            </article>
          </div>
        </div>
      </section>

      <section class="section skills">
        <div class="container">
          <h2 class="section-title reveal">Skills</h2>
          <div class="skills-grid reveal" data-speed="0.3">
            <div class="skills-row">
              <div class="skill-category">
                <h3 class="skill-title">Front‑end</h3>
                <div class="skill-tags">
                  <span class="skill-tag">HTML</span>
                  <span class="skill-tag">CSS</span>
                  <span class="skill-tag">JavaScript</span>
                  <span class="skill-tag">Vue.js</span>
                  <span class="skill-tag">React</span>
                </div>
              </div>
              <div class="skill-category">
                <h3 class="skill-title">Back‑end</h3>
                <div class="skill-tags">
                  <span class="skill-tag">PHP</span>
                  <span class="skill-tag">Python</span>
                  <span class="skill-tag">Firebase</span>
                  <span class="skill-tag">Rust</span>
                  <span class="skill-tag">Solidity</span>
                </div>
              </div>
            </div>
            <div class="skills-row">
              <div class="skill-category">
                <h3 class="skill-title">Tools</h3>
                <div class="skill-tags">
                  <span class="skill-tag">GitHub</span>
                  <span class="skill-tag">Notion</span>
                  <span class="skill-tag">Figma</span>
                </div>
              </div>
              <div class="skill-category">
                <h3 class="skill-title">Languages</h3>
                <div class="skill-tags">
                  <span class="skill-tag">French</span>
                  <span class="skill-tag">English</span>
                  <span class="skill-tag">Spanish</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <section class="section contact">
        <div class="container">
          <h2 class="section-title reveal">Contact</h2>
          <div class="contact-section reveal">
            <div class="contact-grid">
              <div class="contact-item">
                <i aria-hidden="true" class="mdi mdi-linkedin" />
                <a aria-label="LinkedIn" href="https://www.linkedin.com/in/victor-chabeau-b5ab91232/" rel="noopener" target="_blank">LinkedIn — Victor Chabeau</a>
              </div>
              <div class="contact-item">
                <i aria-hidden="true" class="mdi mdi-github" />
                <a aria-label="GitHub" href="https://github.com/victorrchb" rel="noopener" target="_blank">github.com/victorrchb</a>
              </div>
              <div class="contact-item">
                <i aria-hidden="true" class="mdi mdi-map-marker" />
                <a aria-label="Location" href="https://maps.google.com/?q=Paris+75012+France" rel="noopener" target="_blank">Paris 75012</a>
              </div>
              <div class="contact-item contact-center">
                <i aria-hidden="true" class="mdi mdi-phone" />
                <span class="contact-text">07.82.64.79.29</span>
                <button aria-label="Copy phone number" class="copy-btn" @click="copyToClipboard('+33782647929')">
                  <i aria-hidden="true" class="mdi mdi-content-copy" />
                </button>
              </div>
              <div class="contact-item contact-center">
                <i aria-hidden="true" class="mdi mdi-email-outline" />
                <span class="contact-text">victorchabeau03@gmail.com</span>
                <button aria-label="Copy email address" class="copy-btn" @click="copyToClipboard('victorchabeau03@gmail.com')">
                  <i aria-hidden="true" class="mdi mdi-content-copy" />
                </button>
              </div>
            </div>
          </div>
        </div>
      </section>
    </main>

    <!-- Fullscreen Image Gallery Modal -->
    <div v-if="galleryOpen" class="gallery-modal" @click="closeGallery">
      <div class="gallery-modal-content" @click.stop>
        <button aria-label="Close gallery" class="gallery-close" @click="closeGallery">
          <i class="mdi mdi-close" />
        </button>
        <div class="gallery-main-image">
          <img :alt="`WoodPicker project image ${currentImageIndex + 1}`" :src="currentImage">
        </div>
        <div class="gallery-navigation">
          <button aria-label="Previous image" class="gallery-nav gallery-prev" :disabled="currentImageIndex === 0" @click="previousImage">
            <i class="mdi mdi-chevron-left" />
          </button>
          <button aria-label="Next image" class="gallery-nav gallery-next" :disabled="currentImageIndex === galleryImages.length - 1" @click="nextImage">
            <i class="mdi mdi-chevron-right" />
          </button>
        </div>
        <div class="gallery-thumbnails">
          <img
            v-for="(image, index) in galleryImages"
            :key="index"
            :alt="`WoodPicker thumbnail ${index + 1}`"
            :class="{ active: index === currentImageIndex }"
            :src="image"
            @click="setCurrentImage(index)"
          >
        </div>
      </div>
    </div>
  </v-app>
</template>

<script lang="ts" setup>
  import { computed, onBeforeUnmount, onMounted, ref } from 'vue'
  import CursorManager from '@/components/CursorManager.vue'
  import DottedParallax from '@/components/DottedParallax.vue'
  const isLight = ref(false)
  const voiceEnabled = ref(false)

  // Gallery state
  const galleryOpen = ref(false)
  const currentImageIndex = ref(0)
  const galleryImages = ref([
    '/src/assets/img-project/Woodpicker-1.png',
    '/src/assets/img-project/Woodpicker-2.png',
    '/src/assets/img-project/Woodpicker-3.png',
    '/src/assets/img-project/Woodpicker-4.png',
  ])

  const currentImage = computed(() => galleryImages.value[currentImageIndex.value])
  function applyTheme (light: boolean) {
    const root = document.documentElement
    root.dataset.theme = light ? 'light' : 'dark'
  }
  function toggleTheme () {
    isLight.value = !isLight.value
    localStorage.setItem('theme', isLight.value ? 'light' : 'dark')
    applyTheme(isLight.value)
  }

  function speakOnce (text: string) {
    if (!voiceEnabled.value) return
    if (!('speechSynthesis' in window)) return
    try {
      const u = new SpeechSynthesisUtterance(text)
      u.lang = 'en-US'
      window.speechSynthesis.speak(u)
    } catch {}
  }

  function toggleVoice () {
    voiceEnabled.value = !voiceEnabled.value
    localStorage.setItem('voice-enabled', voiceEnabled.value ? '1' : '0')
    if (voiceEnabled.value) {
      speakOnce('Victor Chabeau — Creative Front End Developer. Projects and experience below.')
    } else {
      try {
        window.speechSynthesis.cancel()
      } catch {
        // noop
      }
    }
  }

  // Gallery functions
  function openGallery (project: string) {
    if (project === 'woodpicker') {
      currentImageIndex.value = 0
      galleryOpen.value = true
      document.body.style.overflow = 'hidden'
    }
  }

  function closeGallery () {
    galleryOpen.value = false
    document.body.style.overflow = ''
  }

  function nextImage () {
    if (currentImageIndex.value < galleryImages.value.length - 1) {
      currentImageIndex.value++
    }
  }

  function previousImage () {
    if (currentImageIndex.value > 0) {
      currentImageIndex.value--
    }
  }

  function setCurrentImage (index: number) {
    currentImageIndex.value = index
  }

  let io: IntersectionObserver | null = null
  let rafId = 0

  function onScrollParallax () {
    const items = document.querySelectorAll<HTMLElement>('.parallax')
    const scrollY = window.scrollY
    for (const el of items) {
      const speed = Number(el.dataset.speed || '0')
      const rect = el.getBoundingClientRect()
      const targetY = rect.top + rect.height / 2
      const center = window.innerHeight / 2
      const deltaToCenter = targetY - center
      const yOffset = (scrollY + deltaToCenter) * speed * 0.06
      const vh = window.innerHeight

      // Zone de visibilité très étendue pour rester visible plus longtemps
      const visibilityZone = vh * 0.8
      const distanceFromCenter = Math.abs(deltaToCenter)

      // Progression plus douce: commence à apparaître plus tôt
      let prog = 0
      if (distanceFromCenter < visibilityZone) {
        prog = Math.min(1, Math.max(0, 1 - (distanceFromCenter / visibilityZone) * 0.6))
      }

      const range = Number(el.dataset.xrange || String(Math.max(window.innerWidth, 320)))
      let xOffset = 0
      if (el.classList.contains('slide-left')) xOffset = (1 - prog) * -range
      else if (el.classList.contains('slide-right')) xOffset = (1 - prog) * range

      // Opacité très stable: visible longtemps au centre
      const opacity = Math.min(1, Math.max(0.1, 0.1 + prog * 0.9))
      el.style.transform = `translate3d(${xOffset.toFixed(2)}px, ${(-yOffset).toFixed(2)}px, 0)`
      el.style.opacity = String(opacity)
    }
  }

  function onScrollLoop () {
    onScrollParallax()
    rafId = requestAnimationFrame(onScrollLoop)
  }

  // Keyboard navigation for gallery
  function handleKeydown (e: KeyboardEvent) {
    if (!galleryOpen.value) return
    switch (e.key) {
      case 'Escape': {
        closeGallery()
        break
      }
      case 'ArrowLeft': {
        previousImage()
        break
      }
      case 'ArrowRight': {
        nextImage()
        break
      }
    }
  }

  function copyToClipboard (text: string) {
    navigator.clipboard.writeText(text).then(() => {
      // Optionnel : afficher une notification de succès
      console.log('Copied to clipboard:', text)
    }).catch(error => {
      console.error('Failed to copy:', error)
    })
  }

  onMounted(() => {
    const stored = localStorage.getItem('theme')
    if (stored) {
      isLight.value = stored === 'light'
      applyTheme(isLight.value)
    }
    voiceEnabled.value = localStorage.getItem('voice-enabled') === '1'
    io = new IntersectionObserver(
      entries => {
        for (const entry of entries) {
          if (entry.isIntersecting) {
            entry.target.classList.add('is-visible')
            if (io) io.unobserve(entry.target)
          }
        }
      },
      { root: null, rootMargin: '0px 0px -10% 0px', threshold: 0.15 },
    )
    const els = document.querySelectorAll('.reveal')
    for (const el of els) {
      io?.observe(el)
    }

    // Special handling for skills grid
    const skillsGrid = document.querySelector('.skills-grid')
    if (skillsGrid) {
      const skillsIO = new IntersectionObserver(
        entries => {
          for (const entry of entries) {
            if (entry.isIntersecting) {
              entry.target.classList.add('is-visible')
              skillsIO.unobserve(entry.target)
            }
          }
        },
        { root: null, rootMargin: '0px 0px -20% 0px', threshold: 0.3 },
      )
      skillsIO.observe(skillsGrid)
    }

    // Add keyboard listener
    document.addEventListener('keydown', handleKeydown)
    rafId = requestAnimationFrame(onScrollLoop)
  })

  onBeforeUnmount(() => {
    if (io) io.disconnect()
    if (rafId) cancelAnimationFrame(rafId)
    document.removeEventListener('keydown', handleKeydown)
  })
</script>

<style scoped>
  :deep(.v-application) { min-height: 100vh; background: transparent; }
  .content { position: relative; z-index: 1; pointer-events: auto; }

  /* Hide scrollbar but keep scrolling */
  :global(html) { scrollbar-width: none; }
  :global(body) { -ms-overflow-style: none; }
  :global(body::-webkit-scrollbar) { display: none; }

  /* Skip link */
  .skip-link { position: absolute; left: -9999px; top: 0; padding: .5rem .75rem; background: #fff; color: #000; border-radius: .375rem; }
  .skip-link:focus { left: .75rem; top: .75rem; z-index: 999; }

  /* Theme variables */
  /* Default (dark) */
  :global(:root) {
    --bg: #030301;           /* Fond sombre demandé */
    --ink: #e8ecef;          /* Texte clair pour contraste */
    --panel: #232A2F;        /* Panneaux/carte */
    --bg-canvas: #030301;    /* Fond du canvas à pois (nuit) */
    --dot-canvas: #C1BCAC;   /* Pois clairs (inversion) */
  }
  /* Light */
  :global(:root[data-theme='light']) {
    --bg: #C1BCAC;           /* Fond clair demandé */
    --ink: #030301;          /* Texte foncé pour contraste */
    --panel: #ffffff;
    --bg-canvas: #C1BCAC;    /* Fond du canvas à pois (jour) */
    --dot-canvas: #030301;   /* Pois foncés (inversion) */
  }
  :global(body) { background: var(--bg); color: var(--ink); padding-bottom: 2rem; }
  .controls { position: fixed; right: .75rem; top: .75rem; z-index: 20; display: flex; gap: .5rem; }
  .theme-toggle, .voice-toggle { border: 1px solid rgba(255,255,255,.2); background: var(--panel); color: var(--ink); border-radius: .5rem; padding: .35rem .5rem; cursor: pointer; }
  .theme-toggle:focus-visible, .voice-toggle:focus-visible { outline: 2px solid #fff; outline-offset: 2px; }
  .voice-toggle[aria-pressed='true'] { box-shadow: inset 0 0 0 2px rgba(255,255,255,.3); }
  .sr-only { position: absolute; width: 1px; height: 1px; padding: 0; margin: -1px; overflow: hidden; clip: rect(0,0,0,0); white-space: nowrap; border: 0; }

  :root { --ink: var(--ink); --panel: var(--panel); }
  .section { min-height: 90vh; display: grid; place-items: center; padding: 8rem 0 6rem; }
  .container { width: min(1100px, 92%); margin: 0 auto; }

  .hero .title { color: var(--ink); font-size: clamp(2rem, 6vw, 4rem); margin: 0 0 2.25rem; line-height: 1.05; }
  .hero .subtitle { color: var(--ink); opacity: .9; font-size: clamp(1.1rem, 2.8vw, 1.6rem); margin: 0 0 1.5rem; }
  .hero .lead { margin-top: .25rem; }
  .hero .lead { color: var(--ink); opacity: .8; max-width: 60ch; }

  .projects .container { padding-top: 2.5rem; }
  .section-title { color: var(--ink); font-size: clamp(1.6rem, 3.6vw, 2.6rem); margin: 0 0 6rem; line-height: 1.15; position: relative; z-index: 1; }
  .cards { display: grid; gap: 8rem; }
  .cards.stack { margin-top: 3rem; }
  .cards.stack { grid-template-columns: 1fr; }
  .project-left { margin-right: auto; max-width: 60%; }
  .project-right { margin-left: auto; max-width: 60%; }
  .card { background: var(--panel); border: 1px solid rgba(255,255,255,.08); border-radius: 16px; color: var(--ink); box-shadow: 0 24px 70px rgba(0,0,0,.28); display: flex; flex-direction: column; gap: 1.2rem; padding: 1.3rem 1.4rem; overflow: hidden; min-height: clamp(350px, 25vh, 450px); }
  .card-media { border-radius: 12px; overflow: hidden; margin: 0 0 1.6rem; height: clamp(150px, 12vh, 220px); }
  .card-media img { display: block; width: 100%; height: 100%; object-fit: contain; background: var(--panel); }
  .card-body { display: flex; flex-direction: column; align-items: flex-start; }
  .card-title { margin: 0 0 .6rem; font-size: 1.25rem; }
  .card-text { margin: 0 0 .9rem; opacity: .95; }
  .bullets { margin: 0 0 .9rem; padding-left: 1.1rem; }
  .bullets li { margin: .25rem 0; }
  .tags { list-style: none; display: flex; gap: .5rem; padding: 0; margin: 0; opacity: .9; flex-wrap: wrap; }
  .tags li { background: rgba(255,255,255,.06); border: 1px solid rgba(255,255,255,.08); border-radius: 999px; padding: .2rem .6rem; font-size: .85rem; }

  /* Skills grid */
  .skills-grid {
    display: flex;
    flex-direction: column;
    gap: 2rem;
    margin-top: 3rem;
    opacity: 0;
    transform: translateY(60px) scale(0.95);
    transition: all 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  }
  .skills-grid.is-visible {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
  .skills-row {
    display: flex;
    gap: 2rem;
    justify-content: center;
  }
  .skill-category {
    background: var(--panel);
    border: 1px solid rgba(255,255,255,.08);
    border-radius: 16px;
    padding: 1.5rem;
    text-align: center;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }
  .skill-category:hover {
    transform: translateY(-4px);
    box-shadow: 0 12px 40px rgba(0,0,0,.15);
  }
  .skill-title {
    color: var(--ink);
    font-size: 1.1rem;
    margin: 0 0 1rem;
    font-weight: 600;
  }
  .skill-tags {
    display: flex;
    flex-wrap: wrap;
    gap: .5rem;
    justify-content: center;
  }
  .skill-tag {
    background: linear-gradient(135deg, rgba(255,255,255,.08), rgba(255,255,255,.04));
    border: 1px solid rgba(255,255,255,.12);
    border-radius: 20px;
    padding: .4rem .8rem;
    font-size: .85rem;
    color: var(--ink);
    transition: all 0.2s ease;
    position: relative;
    overflow: hidden;
  }
  .skill-tag::before {
    content: '';
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255,255,255,.1), transparent);
    transition: left 0.5s ease;
  }
  .skill-tag:hover::before {
    left: 100%;
  }
  .skill-tag:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(0,0,0,.1);
  }

  /* Contact section */
  .contact-section { margin-bottom: 4rem; }
  .contact-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 2rem; margin-top: 3rem; }
  .contact-item:nth-child(4) { grid-column: 1 / 3; grid-row: 2; justify-self: center; }
  .contact-item:nth-child(5) { grid-column: 2 / 4; grid-row: 2; justify-self: center; }
  .contact-item { display: flex; align-items: center; gap: 1rem; padding: 1.5rem; background: var(--panel); border: 1px solid rgba(0,0,0,.1); border-radius: 16px; transition: transform 0.3s ease, box-shadow 0.3s ease; }
  .contact-item:hover { transform: translateY(-4px); box-shadow: 0 12px 40px rgba(0,0,0,.15); }
  .contact-item .mdi { color: var(--ink); opacity: .9; font-size: 1.5rem; }
  .contact-item a { color: var(--ink); text-decoration: none; position: relative; cursor: url('/src/assets/windows-11-black-and-white-/Link.cur'), pointer; font-weight: 500; }
  .contact-item a::after { content: ''; position: absolute; left: 0; right: 0; bottom: -2px; height: 1px; background: currentColor; transform: scaleX(0.2); transform-origin: left; transition: transform .25s ease; opacity: .6; }
  .contact-item a:hover::after { transform: scaleX(1); opacity: .9; }
  .contact-text { color: var(--ink); font-weight: 500; flex: 1; }
  .copy-btn { background: none; border: none; color: var(--ink); cursor: url('/src/assets/windows-11-black-and-white-/Link.cur'), pointer; padding: 0.5rem; border-radius: 8px; transition: background 0.3s ease; opacity: 0.7; }
  .copy-btn:hover { background: rgba(0,0,0,0.1); opacity: 1; }
  .copy-btn .mdi { font-size: 1.2rem; }

  /* Image Gallery */
  .image-gallery { position: relative; cursor: url('/src/assets/windows-11-black-and-white-/Link.cur'), pointer; height: clamp(120px, 15vh, 200px); }
  .gallery-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 4px; height: 100%; }
  .gallery-grid img { width: 100%; height: 100%; object-fit: cover; border-radius: 8px; }
  .gallery-overlay { display: none; }
  .gallery-text { display: none; }

  /* Gallery Modal */
  .gallery-modal { position: fixed; top: 0; left: 0; right: 0; bottom: 0; background: rgba(0,0,0,0.95); z-index: 1000; display: flex; align-items: center; justify-content: center; padding: 2rem; }
  .gallery-modal-content { position: relative; max-width: 90vw; max-height: 90vh; display: flex; flex-direction: column; align-items: center; }
  .gallery-close { position: fixed; top: 2rem; right: 2rem; background: rgba(255,255,255,0.1); border: none; color: white; width: 3rem; height: 3rem; border-radius: 50%; cursor: url('/src/assets/windows-11-black-and-white-/Link.cur'), pointer; display: flex; align-items: center; justify-content: center; font-size: 1.5rem; transition: background 0.3s ease; z-index: 1001; }
  .gallery-close:hover { background: rgba(255,255,255,0.2); }
  .gallery-main-image { margin-bottom: 2rem; }
  .gallery-main-image img { max-width: 100%; max-height: 70vh; object-fit: contain; border-radius: 12px; }
  .gallery-navigation { position: absolute; top: 50%; transform: translateY(-50%); display: flex; width: 100%; justify-content: space-between; pointer-events: none; }
  .gallery-nav { background: rgba(255,255,255,0.1); border: none; color: white; width: 3rem; height: 3rem; border-radius: 50%; cursor: url('/src/assets/windows-11-black-and-white-/Link.cur'), pointer; display: flex; align-items: center; justify-content: center; font-size: 1.5rem; transition: background 0.3s ease; pointer-events: auto; }
  .gallery-nav:hover:not(:disabled) { background: rgba(255,255,255,0.2); }
  .gallery-nav:disabled { opacity: 0.3; cursor: not-allowed; }
  .gallery-prev { margin-left: -4rem; }
  .gallery-next { margin-right: -4rem; }
  .gallery-thumbnails { display: flex; gap: 0.5rem; }
  .gallery-thumbnails img { width: 4rem; height: 4rem; object-fit: cover; border-radius: 8px; cursor: url('/src/assets/windows-11-black-and-white-/Link.cur'), pointer; opacity: 0.6; transition: opacity 0.3s ease; }
  .gallery-thumbnails img.active { opacity: 1; }
  .gallery-thumbnails img:hover { opacity: 0.8; }

  @media (max-width: 980px) {
    .cards { grid-template-columns: 1fr; }
    .section { min-height: auto; padding: 5rem 0 4rem; }
    .container { width: min(720px, 90%); }
    .project-left, .project-right { margin: 0; max-width: 100%; }
    .skills-row { flex-direction: column; gap: 1.5rem; }
    .contact-grid { grid-template-columns: 1fr; gap: 1.5rem; }
    .contact-item:nth-child(4), .contact-item:nth-child(5) { grid-column: 1; }
    .contact-item { padding: 1.25rem; }
    .gallery-modal { padding: 1rem; }
    .gallery-close { top: 1rem; right: 1rem; width: 2.5rem; height: 2.5rem; font-size: 1.2rem; }
    .gallery-nav { width: 2.5rem; height: 2.5rem; font-size: 1.2rem; }
    .gallery-prev { margin-left: -3rem; }
    .gallery-next { margin-right: -3rem; }
    .gallery-thumbnails img { width: 3rem; height: 3rem; }
  }
  @media (prefers-reduced-motion: reduce) { .parallax, .reveal, .slide-left, .slide-right { transform: none !important; opacity: 1 !important; transition: none !important; } }

  .reveal { opacity: 1; transform: translateY(0); transition: opacity .35s ease, transform .45s ease; will-change: transform, opacity; }
  .reveal.is-visible { opacity: 1; transform: translateY(0); }

</style>
