<script setup lang="ts">
import { onMounted } from "vue";

// 组件挂载时初始化动画
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

  // 观察联系区域元素
  const contactSection = document.querySelector(".contact-section");
  if (contactSection) {
    observerAnimations.observe(contactSection);
  }
});
</script>

<template>
  <!-- 联系区域 -->
  <section class="contact-section" id="contact">
    <div class="contact-background-shapes">
      <div class="shape shape-1"></div>
      <div class="shape shape-2"></div>
      <div class="shape shape-3"></div>
    </div>

    <div class="contact-container">
      <div class="contact-card">
        <div class="contact-header">
          <h2>Get in touch</h2>
          <p class="contact-subtitle">
            We are looking for mobile games to publish
          </p>
        </div>

        <div class="contact-content">
          <div class="contact-info-card">
            <div class="contact-icon">
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
                <path
                  d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"
                  stroke="currentColor"
                  stroke-width="2"
                />
                <polyline
                  points="22,6 12,13 2,6"
                  stroke="currentColor"
                  stroke-width="2"
                />
              </svg>
            </div>
            <div class="contact-details">
              <h4>Email Us</h4>
              <a href="mailto:summer@octopusgame.net" class="contact-email"
                >summer@octopusgame.net</a
              >
            </div>
          </div>

          <div class="contact-info-card">
            <div class="contact-icon">
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
                <path
                  d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"
                  stroke="currentColor"
                  stroke-width="2"
                />
                <circle
                  cx="12"
                  cy="10"
                  r="3"
                  stroke="currentColor"
                  stroke-width="2"
                />
              </svg>
            </div>
            <div class="contact-details">
              <h4>Location</h4>
              <p>Hong Kong</p>
            </div>
          </div>
        </div>

        <div class="company-brand">
          <h3>OCTOPUS</h3>
          <p>Mobile Game Publisher</p>
          <div class="brand-decoration"></div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
/* 联系区域样式 */
.contact-section {
  padding: 6rem 0;
  background: linear-gradient(135deg, #2c3e50 0%, #34495e 100%);
  color: white;
  width: 100%;
  margin: 0;
  max-width: 100vw;
  overflow: hidden !important;
  position: relative;
  opacity: 0;
  transform: translateY(30px);
  transition: all 1s ease;
}

.contact-section.animate-in {
  opacity: 1;
  transform: translateY(0);
}

.contact-background-shapes {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  overflow: hidden;
  z-index: 1;
}

.shape {
  position: absolute;
  background: rgba(52, 152, 219, 0.1);
  border-radius: 50%;
  animation: floatShape 8s ease-in-out infinite;
}

.shape-1 {
  width: 300px;
  height: 300px;
  top: 10%;
  left: -150px;
  animation-delay: 0s;
}

.shape-2 {
  width: 200px;
  height: 200px;
  top: 60%;
  right: -100px;
  animation-delay: 2s;
}

.shape-3 {
  width: 150px;
  height: 150px;
  top: 30%;
  left: 50%;
  animation-delay: 4s;
  background: rgba(46, 204, 113, 0.1);
}

.contact-container {
  margin: 0 auto;
  padding: 0 2rem;
  width: 100%;
  box-sizing: border-box;
  position: relative;
  z-index: 2;
}

.contact-card {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(10px);
  border-radius: 30px;
  padding: 4rem 3rem;
  border: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
  animation: slideInUp 1s ease-out;
  transition: transform 0.3s ease;
}

.contact-card:hover {
  transform: translateY(-10px);
}

.contact-header {
  text-align: center;
  margin-bottom: 3rem;
}

.contact-header h2 {
  font-size: 3rem;
  margin-bottom: 1rem;
  font-weight: 300;
  background: linear-gradient(45deg, #fff, #3498db);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.contact-subtitle {
  font-size: 1.3rem;
  color: #bdc3c7;
}

.contact-content {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  margin-bottom: 3rem;
}

.contact-info-card {
  background: rgba(255, 255, 255, 0.08);
  border-radius: 20px;
  padding: 2rem;
  text-align: center;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  border: 1px solid rgba(255, 255, 255, 0.1);
  will-change: transform;
}

.contact-info-card:hover {
  background: rgba(255, 255, 255, 0.12);
  transform: translateY(-8px) scale(1.02);
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.25);
  border-color: rgba(52, 152, 219, 0.3);
}

.contact-icon {
  width: 60px;
  height: 60px;
  background: linear-gradient(45deg, #3498db, #2ecc71);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 1.5rem;
  color: white;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  will-change: transform;
}

.contact-icon:hover,
.contact-info-card:hover .contact-icon {
  transform: scale(1.15) rotate(15deg);
  box-shadow: 0 8px 20px rgba(52, 152, 219, 0.4);
}

.contact-details h4 {
  font-size: 1.2rem;
  margin-bottom: 0.5rem;
  color: #ecf0f1;
}

.contact-email {
  color: #3498db;
  text-decoration: none;
  font-size: 1.1rem;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  display: inline-block;
}

.contact-email::after {
  content: "";
  position: absolute;
  bottom: -2px;
  left: 50%;
  width: 0;
  height: 2px;
  background: linear-gradient(45deg, #3498db, #2ecc71);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  transform: translateX(-50%);
}

.contact-email:hover {
  color: #2ecc71;
  text-shadow: 0 0 10px rgba(46, 204, 113, 0.5);
  transform: translateY(-2px);
}

.contact-email:hover::after {
  width: 100%;
}

.contact-details p {
  color: #bdc3c7;
  font-size: 1rem;
}

.company-brand {
  text-align: center;
  position: relative;
}

.company-brand h3 {
  font-size: 2.5rem;
  margin-bottom: 0.5rem;
  letter-spacing: 3px;
  background: linear-gradient(45deg, #fff, #3498db, #2ecc71);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.company-brand p {
  font-size: 1.1rem;
  color: #bdc3c7;
  margin-bottom: 1rem;
}

.brand-decoration {
  width: 60px;
  height: 3px;
  background: linear-gradient(45deg, #3498db, #2ecc71);
  margin: 0 auto;
  border-radius: 2px;
  animation: pulse 2s ease-in-out infinite;
}

/* 动画关键帧 */
@keyframes floatShape {
  0%,
  100% {
    transform: translateY(0) rotate(0deg);
  }
  50% {
    transform: translateY(-20px) rotate(180deg);
  }
}

@keyframes slideInUp {
  from {
    opacity: 0;
    transform: translateY(50px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes pulse {
  0%,
  100% {
    opacity: 1;
    transform: scale(1);
  }
  50% {
    opacity: 0.7;
    transform: scale(1.05);
  }
}

/* 响应式设计 */
@media (max-width: 1024px) {
  .contact-container {
    padding: 0 1rem;
    width: 100%;
  }

  .contact-card {
    padding: 2.5rem 1.5rem;
    border-radius: 20px;
  }

  .contact-content {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }

  .contact-info-card {
    padding: 1.5rem;
    border-radius: 15px;
  }
}

@media (max-width: 768px) {
  .contact-section {
    padding: 4rem 0;
  }

  .contact-header h2 {
    font-size: 2rem;
  }

  .contact-icon {
    width: 50px;
    height: 50px;
  }

  .company-brand h3 {
    font-size: 2rem;
  }

  .shape {
    display: none; /* 移动端隐藏背景形状 */
  }
}
</style>
