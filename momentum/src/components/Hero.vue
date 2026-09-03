<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import img1 from '@/assets/image/1.jpg'
import img2 from '@/assets/image/2.jpeg'
import img3 from '@/assets/image/3.jpg'

// Typing effect
const typed = ref('')
const phrases = ['Overthinking', 'Handsome', 'Shy']
const phraseIndex = ref(0)
const charIndex = ref(0)
const deleting = ref(false)
let typeTimer = null

function type() {
  const current = phrases[phraseIndex.value]
  if (!deleting.value) {
    typed.value = current.slice(0, charIndex.value + 1)
    charIndex.value++
    if (charIndex.value === current.length) {
      deleting.value = true
      typeTimer = setTimeout(type, 1800)
      return
    }
    typeTimer = setTimeout(type, 90)
  } else {
    typed.value = current.slice(0, charIndex.value - 1)
    charIndex.value--
    if (charIndex.value === 0) {
      deleting.value = false
      phraseIndex.value = (phraseIndex.value + 1) % phrases.length
    }
    typeTimer = setTimeout(type, 45)
  }
}

// Carousel
const slides = [
  { src: img1, title: 'Ảnh 1', alt: 'Ảnh cá nhân 1' },
  { src: img2, title: 'Ảnh 2', alt: 'Ảnh cá nhân 2' },
  { src: img3, title: 'Ảnh 3', alt: 'Ảnh cá nhân 3' },
]

const current = ref(0)
let slideTimer = null

function nextSlide() {
  current.value = (current.value + 1) % slides.length
}

function prevSlide() {
  current.value = (current.value - 1 + slides.length) % slides.length
}

function goTo(index) {
  current.value = index
}

function startAuto() {
  slideTimer = setInterval(nextSlide, 3500)
}

function stopAuto() {
  clearInterval(slideTimer)
}

onMounted(() => {
  type()
  startAuto()
})

onBeforeUnmount(() => {
  clearTimeout(typeTimer)
  clearInterval(slideTimer)
})
</script>

<template>
  <section id="home" class="hero">
    <div class="container hero-inner">
      <!-- Carousel -->
      <div class="hero-carousel reveal" @mouseenter="stopAuto" @mouseleave="startAuto">
        <div class="carousel-track" :style="{ transform: `translateX(-${current * 100}%)` }">
          <div class="carousel-slide" v-for="(slide, i) in slides" :key="i">
            <img :src="slide.src" :alt="slide.alt" loading="lazy" />
            <div class="slide-caption">{{ slide.title }}</div>
          </div>
        </div>

        <!-- Arrows -->
        <button class="carousel-arrow prev" @click="prevSlide" aria-label="Ảnh trước">❮</button>
        <button class="carousel-arrow next" @click="nextSlide" aria-label="Ảnh sau">❯</button>

        <!-- Dots -->
        <div class="carousel-dots">
          <button
            v-for="(slide, i) in slides"
            :key="'dot' + i"
            class="dot"
            :class="{ active: i === current }"
            @click="goTo(i)"
            :aria-label="'Ảnh ' + (i + 1)"
          ></button>
        </div>

        <div class="photo-badge">
          <span class="badge-dot"></span>
          Open to work
        </div>
      </div>

      <!-- Text -->
      <div class="hero-text reveal">
        <p class="hero-greeting">Xin chào, mình là</p>
        <h1 class="hero-name">Bùi Hoàng Hiệp</h1>
        <h2 class="hero-role">
          <span class="typed-text">{{ typed }}</span><span class="cursor">|</span>
        </h2>
        <p class="hero-desc">
          Hi! Mình là Hiệp 👋
          Mình thích công nghệ, mê AI và là một overthinker có bằng danh dự. 
          Trong khi người khác ngủ, não mình vẫn đang mở cuộc họp để phân tích một câu nói từ ba ngày trước.
          À mà yên tâm, mình chỉ overthinking trong cuộc sống thôi. 
          Còn khi làm việc, mình gọi đó là "đánh giá rủi ro". 😎
        </p>
        <div class="hero-actions">
          <a href="#projects" class="btn btn-primary">Xem Projects</a>
          <a href="#contact" class="btn btn-outline">Liên hệ</a>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  padding-top: var(--header-height);
  background: var(--color-bg);
  position: relative;
  overflow: hidden;
}

.hero::before {
  content: '';
  position: absolute;
  top: -20%;
  right: -10%;
  width: 500px;
  height: 500px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(79, 140, 255, 0.15), transparent 70%);
  pointer-events: none;
}

.hero-inner {
  display: grid;
  grid-template-columns: 40% 60%;
  align-items: center;
  gap: 60px;
  width: 100%;
}

/* Carousel */
.hero-carousel {
  position: relative;
  width: 100%;
  max-width: 420px;
  border-radius: 24px;
  overflow: hidden;
  box-shadow: 0 20px 60px rgba(79, 140, 255, 0.3);
  background: var(--color-bg-soft);
}

.carousel-track {
  display: flex;
  transition: transform 0.6s cubic-bezier(0.4, 0, 0.2, 1);
  width: 100%;
}

.carousel-slide {
  min-width: 100%;
  position: relative;
  aspect-ratio: 1 / 1;
}

.carousel-slide img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.slide-caption {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 12px 16px;
  background: linear-gradient(transparent, rgba(0, 0, 0, 0.6));
  color: #fff;
  font-size: 0.9rem;
  font-weight: 500;
  text-align: center;
}

/* Arrows */
.carousel-arrow {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  width: 40px;
  height: 40px;
  border-radius: 50%;
  border: none;
  background: rgba(255, 255, 255, 0.85);
  color: #333;
  font-size: 1.1rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  transition: all 0.3s;
  z-index: 2;
}

.carousel-arrow:hover {
  background: var(--color-primary);
  color: #fff;
}

.carousel-arrow.prev {
  left: 12px;
}

.carousel-arrow.next {
  right: 12px;
}

/* Dots */
.carousel-dots {
  position: absolute;
  bottom: 50px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 8px;
  z-index: 2;
}

.dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  border: none;
  background: rgba(255, 255, 255, 0.6);
  cursor: pointer;
  transition: all 0.3s;
  padding: 0;
}

.dot.active {
  background: #fff;
  width: 26px;
  border-radius: 5px;
}

.photo-badge {
  position: absolute;
  top: 14px;
  left: 14px;
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 8px 16px;
  border-radius: 50px;
  background: rgba(255, 255, 255, 0.9);
  border: 1px solid var(--color-border);
  font-size: 0.85rem;
  color: var(--color-text-muted);
  z-index: 2;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.badge-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: #22c55e;
  box-shadow: 0 0 8px #22c55e;
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.4; }
}

/* Text */
.hero-greeting {
  color: var(--color-primary);
  font-size: 1.1rem;
  font-weight: 500;
  margin-bottom: 8px;
  animation: fadeUp 0.7s ease forwards;
}

.hero-name {
  font-size: clamp(2.4rem, 6vw, 4rem);
  font-weight: 800;
  letter-spacing: -1px;
  line-height: 1.1;
  margin-bottom: 12px;
  animation: fadeUp 0.7s 0.1s ease forwards;
}

.hero-role {
  font-size: clamp(1.2rem, 3vw, 1.8rem);
  font-weight: 600;
  color: var(--color-text-muted);
  margin-bottom: 20px;
  min-height: 2em;
  animation: fadeUp 0.7s 0.2s ease forwards;
}

.typed-text {
  color: var(--color-accent);
}

.cursor {
  color: var(--color-primary);
  animation: blink 1s step-end infinite;
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0; }
}

.hero-desc {
  color: var(--color-text-muted);
  max-width: 520px;
  margin-bottom: 32px;
  font-size: 1.05rem;
  animation: fadeUp 0.7s 0.3s ease forwards;
}

.hero-actions {
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
  animation: fadeUp 0.7s 0.4s ease forwards;
}

/* Responsive */
@media (max-width: 768px) {
  .hero-inner {
    grid-template-columns: 1fr;
    text-align: center;
    gap: 40px;
    padding-top: 40px;
  }

  .hero-carousel {
    margin: 0 auto;
    max-width: 320px;
  }

  .hero-desc {
    margin-left: auto;
    margin-right: auto;
  }

  .hero-actions {
    justify-content: center;
  }
}
</style>
