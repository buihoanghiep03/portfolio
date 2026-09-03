<script setup>
import { ref, onMounted } from 'vue'

const projects = ref([
  {
    title: 'Personnel Management System',
    description:
      'Hệ thống quản lý nhân sự đầy đủ tính năng, xây dựng với Vue 3 và Pinia.',
    tech: ['Vue', 'Pinia', 'Axios', 'Vite'],
    github: '#',
    demo: '#',
    color: '#4f8cff',
  },
  {
    title: 'E-commerce Store',
    description:
      'Trang thương mại điện tử với giỏ hàng, thanh toán và quản lý sản phẩm.',
    tech: ['Vue', 'Vuex', 'Bootstrap', 'Node.js'],
    github: '#',
    demo: '#',
    color: '#22d3ee',
  },
  {
    title: 'Portfolio Website',
    description:
      'Website portfolio cá nhân hiện đại, tối giản với animation mượt mà.',
    tech: ['Vue', 'Vite', 'CSS Grid', 'Flexbox'],
    github: '#',
    demo: '#',
    color: '#a78bfa',
  },
])

const reveal = ref(false)

onMounted(() => {
  const el = document.querySelector('.projects')
  const observer = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting) {
        reveal.value = true
        observer.disconnect()
      }
    },
    { threshold: 0.1 }
  )
  if (el) observer.observe(el)
})
</script>

<template>
  <section id="projects" class="projects section">
    <div class="container">
      <div class="section-header reveal" :class="{ visible: reveal }">
        <h2 class="section-title">Projects</h2>
        <p class="section-subtitle">Một số dự án mình đã thực hiện</p>
      </div>

      <div class="projects-grid">
        <article
          v-for="project in projects"
          :key="project.title"
          class="project-card reveal"
          :class="{ visible: reveal }"
        >
          <!-- Preview -->
          <div class="project-preview" :style="{ '--card-color': project.color }">
            <div class="preview-dots">
              <span></span><span></span><span></span>
            </div>
            <div class="preview-content">
              <div class="preview-lines">
                <span></span><span></span><span></span>
              </div>
            </div>
          </div>

          <!-- Body -->
          <div class="project-body">
            <h3 class="project-title">{{ project.title }}</h3>
            <p class="project-desc">{{ project.description }}</p>
            <div class="project-tech">
              <span v-for="t in project.tech" :key="t" class="tech-tag">
                {{ t }}
              </span>
            </div>
            <div class="project-links">
              <a :href="project.github" class="project-link" target="_blank" rel="noopener">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M12 0C5.37 0 0 5.37 0 12c0 5.3 3.438 9.8 8.205 11.387.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61-.546-1.387-1.333-1.756-1.333-1.756-1.09-.745.083-.73.083-.73 1.205.084 1.84 1.237 1.84 1.237 1.07 1.834 2.807 1.304 3.492.997.108-.775.418-1.305.762-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.468-2.38 1.235-3.22-.123-.303-.535-1.523.117-3.176 0 0 1.008-.322 3.3 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.29-1.552 3.297-1.23 3.297-1.23.653 1.653.24 2.873.118 3.176.77.84 1.233 1.91 1.233 3.22 0 4.61-2.805 5.625-5.475 5.92.43.37.81 1.102.81 2.222 0 1.606-.015 2.898-.015 3.293 0 .32.216.694.825.577C20.565 21.796 24 17.3 24 12c0-6.63-5.37-12-12-12z"/>
                </svg>
                GitHub
              </a>
              <a :href="project.demo" class="project-link primary" target="_blank" rel="noopener">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                  <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"></path>
                  <polyline points="15 3 21 3 21 9"></polyline>
                  <line x1="10" y1="14" x2="21" y2="3"></line>
                </svg>
                Demo
              </a>
            </div>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<style scoped>
.projects {
  background: var(--color-bg-soft);
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 28px;
}

.project-card {
  background: var(--color-bg-card);
  border: 1px solid var(--color-border);
  border-radius: var(--radius);
  overflow: hidden;
  transition: all var(--transition);
}

.project-card:hover {
  transform: translateY(-8px);
  box-shadow: var(--shadow);
  border-color: var(--card-color);
}

/* Preview */
.project-preview {
  height: 170px;
  background: linear-gradient(135deg, var(--card-color), transparent 80%);
  opacity: 0.9;
  position: relative;
  padding: 16px;
}

.preview-dots {
  display: flex;
  gap: 6px;
  margin-bottom: 20px;
}

.preview-dots span {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.4);
}

.preview-lines {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.preview-lines span {
  height: 8px;
  border-radius: 4px;
  background: rgba(255, 255, 255, 0.5);
}

.preview-lines span:nth-child(2) {
  width: 80%;
}

.preview-lines span:nth-child(3) {
  width: 60%;
}

/* Body */
.project-body {
  padding: 24px;
}

.project-title {
  font-size: 1.15rem;
  font-weight: 700;
  margin-bottom: 10px;
}

.project-desc {
  color: var(--color-text-muted);
  font-size: 0.92rem;
  margin-bottom: 16px;
}

.project-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-bottom: 20px;
}

.tech-tag {
  padding: 4px 12px;
  border-radius: 50px;
  background: var(--color-bg-soft);
  border: 1px solid var(--color-border);
  font-size: 0.78rem;
  color: var(--color-text-muted);
}

.project-links {
  display: flex;
  gap: 16px;
}

.project-link {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-size: 0.88rem;
  font-weight: 500;
  color: var(--color-text-muted);
  transition: color var(--transition);
}

.project-link:hover {
  color: var(--color-text);
}

.project-link.primary {
  color: var(--color-primary);
}

.project-link.primary:hover {
  color: var(--color-primary-hover);
}

@media (max-width: 900px) {
  .projects-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 600px) {
  .projects-grid {
    grid-template-columns: 1fr;
  }
}
</style>
