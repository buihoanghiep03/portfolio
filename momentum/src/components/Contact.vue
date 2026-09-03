<script setup>
import { ref, onMounted } from 'vue'

const contacts = ref([
  {
    label: 'Email',
    value: 'hiep3919@gmail.com',
    href: 'mailto:hiep3919@gmail.com',
    icon: '✉️',
  },
  {
    label: 'GitHub',
    value: 'github.com/hiep-dev',
    href: 'https://github.com',
    icon: '🐙',
  },
  {
    label: 'Facebook',
    value: 'facebook.com/hiep',
    href: 'https://web.facebook.com/buihoanghiep.03?locale=vi_VN',
    icon: '📘',
  },
  {
    label: 'LinkedIn',
    value: 'linkedin.com/in/hiep',
    href: 'https://linkedin.com',
    icon: '💼',
  },
])

const reveal = ref(false)

onMounted(() => {
  const el = document.querySelector('.contact')
  const observer = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting) {
        reveal.value = true
        observer.disconnect()
      }
    },
    { threshold: 0.2 }
  )
  if (el) observer.observe(el)
})
</script>

<template>
  <section id="contact" class="contact section">
    <div class="container">
      <div class="section-header reveal" :class="{ visible: reveal }">
        <h2 class="section-title">Contact</h2>
        <p class="section-subtitle">Hãy kết nối với mình qua các kênh dưới đây</p>
      </div>

      <div class="contact-grid">
        <a
          v-for="contact in contacts"
          :key="contact.label"
          :href="contact.href"
          class="contact-card reveal"
          :class="{ visible: reveal }"
          target="_blank"
          rel="noopener"
        >
          <div class="contact-icon">{{ contact.icon }}</div>
          <h3 class="contact-label">{{ contact.label }}</h3>
          <p class="contact-value">{{ contact.value }}</p>
        </a>
      </div>
    </div>
  </section>
</template>

<style scoped>
.contact-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 24px;
}

.contact-card {
  background: var(--color-bg-card);
  border: 1px solid var(--color-border);
  border-radius: var(--radius);
  padding: 32px 20px;
  text-align: center;
  transition: all var(--transition);
}

.contact-card:hover {
  transform: translateY(-6px);
  border-color: var(--color-primary);
  box-shadow: var(--shadow);
}

.contact-icon {
  font-size: 2.2rem;
  margin-bottom: 12px;
}

.contact-label {
  font-size: 0.95rem;
  font-weight: 600;
  margin-bottom: 6px;
  color: var(--color-text);
}

.contact-value {
  font-size: 0.85rem;
  color: var(--color-text-muted);
  word-break: break-all;
}

@media (max-width: 768px) {
  .contact-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 480px) {
  .contact-grid {
    grid-template-columns: 1fr;
  }
}
</style>
