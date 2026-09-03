<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const scrolled = ref(false)
const menuOpen = ref(false)
const isDark = ref(true)

const links = [
  { label: 'Trang chủ', href: '#home' },
  { label: 'About', href: '#about' },
  { label: 'Skills', href: '#skills' },
  { label: 'Projects', href: '#projects' },
  { label: 'Contact', href: '#contact' },
]

function onScroll() {
  scrolled.value = window.scrollY > 30
}

function toggleTheme() {
  isDark.value = !isDark.value
  document.documentElement.setAttribute('data-theme', isDark.value ? 'dark' : 'light')
}

function toggleMenu() {
  menuOpen.value = !menuOpen.value
}

function closeMenu() {
  menuOpen.value = false
}

onMounted(() => {
  window.addEventListener('scroll', onScroll)
  // Apply saved theme
  const saved = localStorage.getItem('theme')
  if (saved) {
    isDark.value = saved === 'dark'
    document.documentElement.setAttribute('data-theme', saved)
  }
})

onBeforeUnmount(() => {
  window.removeEventListener('scroll', onScroll)
})
</script>

<template>
  <header class="header" :class="{ scrolled }">
    <div class="container header-inner">
      <a href="#home" class="logo" @click="closeMenu">
        <span class="logo-dot"></span>
        BÙI HOÀNG HIỆP / BLOGER
      </a>

      <nav class="nav" :class="{ open: menuOpen }">
        <a
          v-for="link in links"
          :key="link.href"
          :href="link.href"
          class="nav-link"
          @click="closeMenu"
        >
          {{ link.label }}
        </a>
      </nav>

      <div class="header-actions">
        <button class="theme-toggle" @click="toggleTheme" :aria-label="isDark ? 'Chuyển sang sáng' : 'Chuyển sang tối'">
          <svg v-if="isDark" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <circle cx="12" cy="12" r="4"></circle>
            <line x1="12" y1="2" x2="12" y2="4"></line>
            <line x1="12" y1="20" x2="12" y2="22"></line>
            <line x1="4.93" y1="4.93" x2="6.34" y2="6.34"></line>
            <line x1="17.66" y1="17.66" x2="19.07" y2="19.07"></line>
            <line x1="2" y1="12" x2="4" y2="12"></line>
            <line x1="20" y1="12" x2="22" y2="12"></line>
            <line x1="4.93" y1="19.07" x2="6.34" y2="17.66"></line>
            <line x1="17.66" y1="6.34" x2="19.07" y2="4.93"></line>
          </svg>
          <svg v-else width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"></path>
          </svg>
        </button>

        <button class="menu-toggle" @click="toggleMenu" :aria-expanded="menuOpen">
          <span></span>
          <span></span>
          <span></span>
        </button>
      </div>
    </div>
  </header>
</template>

<style scoped>
.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: var(--header-height);
  background: rgba(15, 17, 21, 0.85);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border-bottom: 1px solid transparent;
  z-index: 1000;
  transition: all var(--transition);
}

[data-theme='light'] .header {
  background: rgba(250, 251, 252, 0.85);
}

.header.scrolled {
  background: rgba(15, 17, 21, 0.95);
  box-shadow: var(--shadow);
  border-bottom: 1px solid var(--color-border);
}

[data-theme='light'] .header.scrolled {
  background: rgba(250, 251, 252, 0.95);
}

.header-inner {
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 24px;
}

.logo {
  display: flex;
  align-items: center;
  gap: 10px;
  font-weight: 700;
  font-size: 1.05rem;
  letter-spacing: 1px;
}

.logo-dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: var(--color-primary);
  box-shadow: 0 0 12px var(--color-primary);
}

.nav {
  display: flex;
  align-items: center;
  gap: 32px;
}

.nav-link {
  font-size: 0.92rem;
  font-weight: 500;
  color: var(--color-text-muted);
  position: relative;
  transition: color var(--transition);
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: -6px;
  left: 0;
  width: 0;
  height: 2px;
  background: var(--color-primary);
  transition: width var(--transition);
}

.nav-link:hover {
  color: var(--color-text);
}

.nav-link:hover::after {
  width: 100%;
}

.header-actions {
  display: flex;
  align-items: center;
  gap: 12px;
}

.theme-toggle {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  color: var(--color-text);
  border: 1px solid var(--color-border);
  transition: all var(--transition);
}

.theme-toggle:hover {
  border-color: var(--color-primary);
  color: var(--color-primary);
}

.menu-toggle {
  display: none;
  flex-direction: column;
  gap: 5px;
  width: 40px;
  height: 40px;
  align-items: center;
  justify-content: center;
}

.menu-toggle span {
  width: 22px;
  height: 2px;
  background: var(--color-text);
  transition: all 0.3s;
}

.menu-toggle[aria-expanded='true'] span:nth-child(1) {
  transform: translateY(7px) rotate(45deg);
}

.menu-toggle[aria-expanded='true'] span:nth-child(2) {
  opacity: 0;
}

.menu-toggle[aria-expanded='true'] span:nth-child(3) {
  transform: translateY(-7px) rotate(-45deg);
}

/* Responsive */
@media (max-width: 768px) {
  .menu-toggle {
    display: flex;
  }

  .nav {
    position: fixed;
    top: var(--header-height);
    left: 0;
    right: 0;
    flex-direction: column;
    align-items: flex-start;
    gap: 0;
    background: var(--color-bg-soft);
    border-bottom: 1px solid var(--color-border);
    padding: 0 24px;
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.4s ease;
  }

  .nav.open {
    max-height: 320px;
  }

  .nav-link {
    padding: 16px 0;
    width: 100%;
    border-bottom: 1px solid var(--color-border);
  }

  .nav-link::after {
    display: none;
  }
}
</style>
