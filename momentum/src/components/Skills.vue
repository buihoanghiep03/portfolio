<script setup>
import { ref, onMounted } from 'vue'

const skills = ref([
  { name: 'HTML', level: 90, icon: '🏷️' },
  { name: 'CSS', level: 85, icon: '🎨' },
  { name: 'JavaScript', level: 80, icon: '⚡' },
  { name: 'Vue', level: 85, icon: '💚' },
  { name: 'Vite', level: 80, icon: '⚡' },
  { name: 'Git', level: 75, icon: '🌿' },
  { name: 'Pinia', level: 80, icon: '🍍' },
  { name: 'Axios', level: 75, icon: '🔗' },
  { name: 'Bootstrap', level: 70, icon: '🎯' },
])

const reveal = ref(false)

onMounted(() => {
  const el = document.querySelector('.skills')
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
  <section id="skills" class="skills section">
    <div class="container">
      <div class="section-header reveal" :class="{ visible: reveal }">
        <h2 class="section-title">Skills</h2>
        <p class="section-subtitle">Công nghệ và công cụ mình sử dụng</p>
      </div>

      <div class="skills-grid">
        <div
          v-for="skill in skills"
          :key="skill.name"
          class="skill-card reveal"
          :class="{ visible: reveal }"
        >
          <div class="skill-icon">{{ skill.icon }}</div>
          <h3 class="skill-name">{{ skill.name }}</h3>
          <div class="skill-bar">
            <div class="skill-bar-fill" :style="{ width: reveal ? skill.level + '%' : '0%' }"></div>
          </div>
          <span class="skill-level">{{ skill.level }}%</span>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.skills-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
}

.skill-card {
  background: var(--color-bg-card);
  border: 1px solid var(--color-border);
  border-radius: var(--radius);
  padding: 28px;
  text-align: center;
  transition: all var(--transition);
}

.skill-card:hover {
  transform: translateY(-6px);
  border-color: var(--color-primary);
  box-shadow: var(--shadow);
}

.skill-icon {
  font-size: 2.4rem;
  margin-bottom: 12px;
}

.skill-name {
  font-size: 1.1rem;
  font-weight: 600;
  margin-bottom: 16px;
}

.skill-bar {
  height: 8px;
  border-radius: 10px;
  background: var(--color-bg-soft);
  overflow: hidden;
  margin-bottom: 8px;
}

.skill-bar-fill {
  height: 100%;
  border-radius: 10px;
  background: linear-gradient(90deg, var(--color-primary), var(--color-accent));
  transition: width 1.2s ease;
}

.skill-level {
  font-size: 0.85rem;
  color: var(--color-text-muted);
}

@media (max-width: 768px) {
  .skills-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 480px) {
  .skills-grid {
    grid-template-columns: 1fr;
  }
}
</style>
