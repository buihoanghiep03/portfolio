<script setup>
import { ref, onMounted } from 'vue'

const info = ref([
  { label: 'Tên', value: 'Bùi Hoàng Hiệp' },
  { label: 'Vai trò', value: 'Frontend Developer' },
  { label: 'Địa điểm', value: 'Việt Nam' },
  { label: 'Email', value: 'hiep3919@gmail.com' },
])

const interests = ['Vue', 'AI', 'UI/UX', 'Web Development', 'IELTS']

const reveal = ref(false)

onMounted(() => {
  const el = document.querySelector('.about')
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
  <section id="about" class="about section">
    <div class="container">
      <div class="section-header reveal" :class="{ visible: reveal }">
        <h2 class="section-title">About</h2>
        <p class="section-subtitle">Tìm hiểu về mình và hành trình Frontend</p>
      </div>

      <div class="about-grid">
        <div class="about-text reveal" :class="{ visible: reveal }">
          <p>
            Xin chào! Mình là <strong>Bùi Hoàng Hiệp</strong>, hiện đang là
            <strong>Frontend Developer</strong>. Mình đam mê xây dựng những
            giao diện web hiện đại, tối giản và giàu trải nghiệm.
          </p>
          <p>
            Mình quan tâm đến <strong>Vue</strong>, <strong>UI/UX</strong>,
            và <strong>Web Development</strong>. Mình luôn tìm cách tối ưu
            hiệu năng và code sạch, rõ ràng.
          </p>
          <div class="about-interests">
            <span
              v-for="interest in interests"
              :key="interest"
              class="interest-tag"
            >
              {{ interest }}
            </span>
          </div>
        </div>

        <div class="about-info reveal" :class="{ visible: reveal }">
          <div v-for="item in info" :key="item.label" class="info-item">
            <span class="info-label">{{ item.label }}</span>
            <span class="info-value">{{ item.value }}</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about {
  background: var(--color-bg-soft);
}

.about-grid {
  display: grid;
  grid-template-columns: 1.2fr 0.8fr;
  gap: 60px;
  align-items: start;
}

.about-text p {
  color: var(--color-text-muted);
  margin-bottom: 16px;
  font-size: 1.05rem;
}

.about-text strong {
  color: var(--color-text);
}

.about-interests {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-top: 24px;
}

.interest-tag {
  padding: 8px 16px;
  border-radius: 50px;
  background: var(--color-bg-card);
  border: 1px solid var(--color-border);
  font-size: 0.88rem;
  color: var(--color-text);
  transition: all var(--transition);
}

.interest-tag:hover {
  border-color: var(--color-primary);
  color: var(--color-primary);
  transform: translateY(-2px);
}

.about-info {
  background: var(--color-bg-card);
  border: 1px solid var(--color-border);
  border-radius: var(--radius);
  padding: 32px;
  box-shadow: var(--shadow);
}

.info-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 14px 0;
  border-bottom: 1px solid var(--color-border);
}

.info-item:last-child {
  border-bottom: none;
}

.info-label {
  color: var(--color-text-muted);
  font-size: 0.9rem;
}

.info-value {
  font-weight: 500;
  color: var(--color-text);
}

@media (max-width: 768px) {
  .about-grid {
    grid-template-columns: 1fr;
    gap: 40px;
  }
}
</style>
