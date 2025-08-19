<script setup lang="ts">
import { onMounted } from "vue";

// 组件挂载时初始化动画观察器
onMounted(() => {
  const observerAnimations = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add("animate-in");
        }
      });
    },
    {
      threshold: 0.1,
      rootMargin: "0px 0px -50px 0px",
    },
  );

  // 观察特色功能卡片
  const featureCards = document.querySelectorAll(".feature-card");
  featureCards.forEach((card) => {
    observerAnimations.observe(card);
  });
});
</script>

<template>
  <!-- 特色功能区域 -->
  <section class="features-section">
    <div class="features-container">
      <div class="feature-card">
        <h3>More user</h3>
        <p>
          Thanks to our user acquisition system and team, they will help you
          game reach every corner of the world
        </p>
      </div>

      <div class="feature-card">
        <h3>More income</h3>
        <p>
          How to balance the IAP and Ad revenue?<br />
          How to maximize the revenue without affecting players' experience?<br />
          …<br />
          We will guide you through out the whole process of monetization.
        </p>
      </div>

      <div class="feature-card">
        <h3>More fun</h3>
        <p>Be together, let's create more fun now!</p>
      </div>
    </div>
  </section>
</template>

<style scoped>
/* 特色功能区域样式 */
.features-section {
  padding: 6rem 0;
  background: linear-gradient(
    to bottom,
    rgba(102, 126, 234, 0.08) 0%,
    #f8f9fa 15%,
    #f8f9fa 85%,
    rgba(45, 55, 72, 0.05) 100%
  );
  width: 100%;
  margin: 0;
  max-width: 100vw;
  overflow: hidden !important;
  position: relative;
}

/* 顶部过渡层 - 与Hero同步变化 */
.features-section::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 120px;
  background: linear-gradient(
    to bottom,
    rgba(102, 126, 234, 0.15) 0%,
    rgba(118, 75, 162, 0.08) 40%,
    transparent 100%
  );
  animation: backgroundSync 10s ease-in-out infinite;
  z-index: 1;
}

/* 底部过渡层 - 向Contact区域过渡 */
.features-section::after {
  content: "";
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 120px;
  background: linear-gradient(
    to bottom,
    transparent 0%,
    rgba(45, 55, 72, 0.03) 40%,
    rgba(45, 55, 72, 0.08) 100%
  );
  z-index: 1;
}

/* 与Hero背景同步的动画 */
@keyframes backgroundSync {
  0% {
    background: linear-gradient(
      to bottom,
      rgba(102, 126, 234, 0.15) 0%,
      rgba(118, 75, 162, 0.08) 40%,
      transparent 100%
    );
  }
  20% {
    background: linear-gradient(
      to bottom,
      rgba(102, 126, 234, 0.18) 0%,
      rgba(240, 147, 251, 0.08) 40%,
      transparent 100%
    );
  }
  40% {
    background: linear-gradient(
      to bottom,
      rgba(118, 75, 162, 0.15) 0%,
      rgba(102, 126, 234, 0.08) 40%,
      transparent 100%
    );
  }
  60% {
    background: linear-gradient(
      to bottom,
      rgba(240, 147, 251, 0.16) 0%,
      rgba(118, 75, 162, 0.08) 40%,
      transparent 100%
    );
  }
  80% {
    background: linear-gradient(
      to bottom,
      rgba(102, 126, 234, 0.16) 0%,
      rgba(118, 75, 162, 0.09) 40%,
      transparent 100%
    );
  }
  100% {
    background: linear-gradient(
      to bottom,
      rgba(102, 126, 234, 0.15) 0%,
      rgba(118, 75, 162, 0.08) 40%,
      transparent 100%
    );
  }
}

.features-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 3rem;
  width: 100%;
  box-sizing: border-box;
  position: relative;
  z-index: 2;
}

.feature-card {
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(20px);
  padding: 3.5rem 2.5rem;
  border-radius: 20px;
  box-shadow:
    0 8px 32px rgba(0, 0, 0, 0.1),
    0 2px 8px rgba(0, 0, 0, 0.05);
  text-align: center;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  border: 1px solid rgba(255, 255, 255, 0.3);
  opacity: 0;
  transform: translateY(40px);
  position: relative;
  overflow: hidden;
}

.feature-card.animate-in {
  opacity: 1;
  transform: translateY(0);
}

.feature-card::before {
  content: "";
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    90deg,
    transparent,
    rgba(255, 255, 255, 0.4),
    transparent
  );
  transition: left 0.6s ease;
}

.feature-card:hover {
  transform: translateY(-12px) scale(1.03);
  box-shadow:
    0 20px 40px rgba(0, 0, 0, 0.15),
    0 8px 16px rgba(0, 0, 0, 0.1);
  border-radius: 24px;
  background: rgba(255, 255, 255, 0.98);
  border-color: rgba(102, 126, 234, 0.3);
}

.feature-card:hover::before {
  left: 100%;
}

.feature-card h3 {
  font-size: 2.2rem;
  color: #2c3e50;
  margin-bottom: 1.8rem;
  font-weight: 700;
  letter-spacing: -0.5px;
  position: relative;
}

.feature-card h3::after {
  content: "";
  position: absolute;
  bottom: -8px;
  left: 50%;
  transform: translateX(-50%);
  width: 60px;
  height: 3px;
  background: linear-gradient(135deg, #667eea, #764ba2);
  border-radius: 2px;
  opacity: 0.8;
}

.feature-card p {
  font-size: 1.15rem;
  color: #4a5568;
  line-height: 1.7;
  font-weight: 400;
}

/* 响应式设计 */
@media (max-width: 1024px) {
  .features-container {
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
  }
}

@media (max-width: 768px) {
  .features-section {
    padding: 3rem 0;
  }

  .features-container {
    padding: 0 1rem;
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }

  .feature-card {
    padding: 2rem 1.5rem;
    border-radius: 20px;
  }

  .feature-card h3 {
    font-size: 1.5rem;
  }

  .feature-card p {
    font-size: 1rem;
  }
}
</style>
