<script setup lang="ts">
import { ref, onMounted, onUnmounted, nextTick } from 'vue'

// 响应式变量
const heroSection = ref<HTMLElement | null>(null)
const showScrollIndicator = ref(true)
let heroObserver: IntersectionObserver | null = null

// 滚动到下一个区域的函数
const scrollToNext = () => {
  const featuresSection = document.querySelector('.features-section')
  if (featuresSection) {
    featuresSection.scrollIntoView({ behavior: 'smooth' })
  }
}

// 初始化粒子位置的函数
const initParticles = () => {
  const particles = document.querySelectorAll('.particle')
  const heroContainer = heroSection.value

  if (heroContainer && particles.length > 0) {
    // 确保容器已经有正确的尺寸
    const containerHeight = heroContainer.offsetHeight || window.innerHeight
    const containerWidth = heroContainer.offsetWidth || window.innerWidth

    particles.forEach((particle: Element) => {
      const htmlParticle = particle as HTMLElement
      // 确保粒子位置在容器范围内
      const randomX = Math.random() * Math.max(containerWidth - 20, 100) // 留出更多边距
      const randomY = Math.random() * Math.max(containerHeight - 20, 100) // 留出更多边距
      const randomSize = Math.random() * 6 + 2

      htmlParticle.style.left = randomX + 'px'
      htmlParticle.style.top = randomY + 'px'
      htmlParticle.style.width = randomSize + 'px'
      htmlParticle.style.height = randomSize + 'px'
      htmlParticle.style.animationDelay = Math.random() * 6 + 's'
      htmlParticle.style.animationDuration = Math.random() * 8 + 6 + 's'
    })
  }
}

// 组件挂载时的初始化
onMounted(async () => {
  // 等待DOM完全渲染
  await nextTick()

  // 延迟一点时间确保样式完全应用
  setTimeout(() => {
    initParticles()
  }, 100)

  // 创建 Hero 容器观察器来控制滚动指示器的显示
  const heroContent = document.querySelector('.hero-container')
  if (heroContent) {
    heroObserver = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          // 当 hero-container 大部分还在视口内时显示滚动指示器
          // 当 hero-container 大部分离开视口时隐藏滚动指示器
          showScrollIndicator.value = entry.intersectionRatio >= 0.5
        })
      },
      {
        threshold: [0, 0.3, 0.5, 0.7, 1],
        rootMargin: '0px',
      }
    )

    heroObserver.observe(heroContent)
  }
})

// 窗口大小变化时重新初始化粒子
const handleResize = () => {
  initParticles()
}

onMounted(() => {
  window.addEventListener('resize', handleResize)
})

// 组件卸载时清理观察器和事件监听器
onUnmounted(() => {
  if (heroObserver) {
    heroObserver.disconnect()
  }
  window.removeEventListener('resize', handleResize)
})
</script>

<template>
  <!-- Hero 区域 -->
  <section class="hero-section" ref="heroSection">
    <!-- 背景动画粒子 -->
    <div class="particles">
      <div class="particle" v-for="n in 50" :key="n"></div>
    </div>

    <div class="hero-container">
      <h1 class="company-name">Octopus Interactive Technology Limited</h1>
      <h2 class="subtitle">
        Mobile game publisher <span class="highlight">focusing on global market</span>
      </h2>

      <div class="hero-brand">
        <h3 class="brand-title">OCTOPUS</h3>
        <p class="brand-subtitle">mobile game publisher</p>
        <p class="brand-description">
          We love bring excellent game to global players and working with developers all over the
          word.<br />
          We know you are the one who have the best idea. Contact us and let us learn more about
          you!
        </p>
      </div>
    </div>

    <!-- 滚动指示器 -->
    <div class="scroll-indicator" @click="scrollToNext" v-show="showScrollIndicator">
      <div class="scroll-arrow"></div>
    </div>
  </section>
</template>

<style scoped>
/* Hero 区域样式 */
.hero-section {
  height: 100vh; /* 使用固定高度而不是最小高度 */
  width: 100vw; /* 确保宽度占满视口 */
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  position: relative;
  overflow: hidden !important; /* 确保内容不会溢出 */
  animation: backgroundShift 10s ease-in-out infinite;
  margin: 0;
  padding: 0;
  box-sizing: border-box; /* 确保盒模型正确 */
  /* 确保容器立即占满视口 */
  min-height: 100vh;
  max-height: 100vh;
}

/* 背景动态切换动画 */
@keyframes backgroundShift {
  0% {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  }
  20% {
    background: linear-gradient(135deg, #667eea 30%, #f093fb 100%);
  }
  40% {
    background: linear-gradient(135deg, #764ba2 0%, #667eea 70%);
  }
  60% {
    background: linear-gradient(135deg, #f093fb 20%, #764ba2 80%);
  }
  80% {
    background: linear-gradient(135deg, #667eea 40%, #764ba2 60%);
  }
  100% {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  }
}

.hero-container {
  padding: 0 2rem;
  animation: fadeInUp 1s ease-out;
  width: 100%;
  box-sizing: border-box;
  position: relative;
  z-index: 2; /* 确保内容在粒子之上 */
}

.company-name {
  font-size: 3rem;
  font-weight: 300;
  margin-bottom: 1rem;
  letter-spacing: 3px;
  opacity: 0;
  animation: fadeInUp 1s ease-out 0.2s forwards;
}

.subtitle {
  font-size: 1.5rem;
  font-weight: 400;
  margin-bottom: 3rem;
  opacity: 0;
  animation: fadeInUp 1s ease-out 0.4s forwards;
}

.highlight {
  color: #ffd700;
  font-weight: 600;
}

.hero-brand {
  margin-top: 3rem;
  opacity: 0;
  animation: fadeInUp 1s ease-out 0.6s forwards;
}

.brand-title {
  font-size: 4rem;
  font-weight: bold;
  margin-bottom: 0.5rem;
  letter-spacing: 5px;
}

.brand-subtitle {
  font-size: 1.2rem;
  color: #e8e8e8;
  margin-bottom: 2rem;
}

.brand-description {
  font-size: 1.1rem;
  line-height: 1.8;
  max-width: 800px;
  margin: 0 auto;
}

/* 粒子动画背景 */
.particles {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden !important; /* 防止粒子溢出 */
  z-index: 1;
  pointer-events: none; /* 确保不影响其他交互 */
  /* 确保粒子容器不会超出父容器 */
  max-width: 100%;
  max-height: 100%;
}

.particle {
  position: absolute;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 50%;
  pointer-events: none;
  animation: float 6s ease-in-out infinite;
}

.particle:nth-child(odd) {
  width: 4px;
  height: 4px;
  animation-delay: 0s;
  animation-duration: 8s;
}

.particle:nth-child(even) {
  width: 2px;
  height: 2px;
  animation-delay: 2s;
  animation-duration: 12s;
}

.particle:nth-child(3n) {
  width: 6px;
  height: 6px;
  animation-delay: 4s;
  animation-duration: 10s;
}

/* 滚动指示器 */
.scroll-indicator {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  z-index: 10;
  cursor: pointer;
  transition: opacity 0.3s ease, visibility 0.3s ease;
}

.scroll-arrow {
  width: 50px;
  height: 50px;
  border: 2px solid rgba(255, 255, 255, 0.6);
  border-radius: 50%;
  position: relative;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  transition: all 0.3s ease;
  animation: scrollPulse 2s ease-in-out infinite;
  display: flex;
  align-items: center;
  justify-content: center;
}

.scroll-arrow:hover {
  border-color: rgba(255, 255, 255, 0.9);
  background: rgba(255, 255, 255, 0.2);
  transform: translateY(-3px);
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
}

.scroll-arrow::before {
  content: '';
  width: 12px;
  height: 12px;
  border-right: 2px solid rgba(255, 255, 255, 0.8);
  border-bottom: 2px solid rgba(255, 255, 255, 0.8);
  transform: rotate(45deg);
  margin-top: -3px;
  transition: all 0.3s ease;
}

.scroll-arrow:hover::before {
  border-color: rgba(255, 255, 255, 1);
  transform: rotate(45deg) scale(1.1);
}

/* 动画关键帧 */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes float {
  0%,
  100% {
    transform: translateY(0) rotate(0deg);
    opacity: 0.4;
  }
  50% {
    transform: translateY(-30px) rotate(180deg); /* 增加浮动范围但确保不溢出 */
    opacity: 0.8;
  }
}

@keyframes scrollPulse {
  0%,
  100% {
    transform: scale(1);
    opacity: 0.8;
  }
  50% {
    transform: scale(1.1);
    opacity: 1;
  }
}

/* 响应式设计 */
@media (max-width: 768px) {
  .company-name {
    font-size: 2rem;
    letter-spacing: 1px;
  }

  .subtitle {
    font-size: 1.2rem;
  }

  .brand-title {
    font-size: 2.5rem;
    letter-spacing: 3px;
  }

  .brand-description {
    font-size: 1rem;
  }

  .hero-container {
    padding: 1rem;
  }
}
</style>
