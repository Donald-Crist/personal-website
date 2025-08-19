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

  // 观察页脚元素
  const footerSection = document.querySelector(".footer");
  if (footerSection) {
    observerAnimations.observe(footerSection);
  }
});
</script>

<template>
  <!-- 页脚 -->
  <footer class="footer">
    <div class="footer-background">
      <div class="footer-wave"></div>
    </div>

    <div class="footer-container">
      <div class="footer-content">
        <div class="footer-card">
          <div class="footer-icon">
            <svg width="32" height="32" viewBox="0 0 24 24" fill="none">
              <path
                d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"
                stroke="currentColor"
                stroke-width="2"
              />
              <polyline
                points="9,22 9,12 15,12 15,22"
                stroke="currentColor"
                stroke-width="2"
              />
            </svg>
          </div>
          <h4>Our Studio</h4>
          <div class="footer-address">
            <p>ROOM 1003 10/F TOWER 1</p>
            <p>LIPPO CENTRE 89 QUEENSWAY</p>
            <p>ADMIRALTY HK, China</p>
          </div>
          <div class="contact-phone">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none">
              <path
                d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"
                stroke="currentColor"
                stroke-width="2"
              />
            </svg>
            <span>+852 61143505</span>
          </div>
        </div>

        <div class="footer-card">
          <div class="footer-icon">
            <svg width="32" height="32" viewBox="0 0 24 24" fill="none">
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
          <h4>Stay Connected</h4>
          <p>Thank you for your visiting!</p>
          <p>Let's create amazing games together.</p>
          <div class="social-links">
            <div class="social-link">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
                <circle
                  cx="12"
                  cy="12"
                  r="10"
                  stroke="currentColor"
                  stroke-width="2"
                />
                <path
                  d="M8.56 2.75c4.37 6.03 6.02 9.42 8.03 17.72m2.54-15.38c-3.72 4.35-8.94 5.66-16.88 4.85"
                  stroke="currentColor"
                  stroke-width="2"
                />
              </svg>
            </div>
            <div class="social-link">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
                <rect
                  x="2"
                  y="3"
                  width="20"
                  height="14"
                  rx="2"
                  ry="2"
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
          </div>
        </div>
      </div>

      <div class="copyright-section">
        <div class="copyright-line"></div>
        <p class="copyright">
          Copyright © 2022 Octopus Interactive Technology Limited
        </p>
      </div>
    </div>
  </footer>
</template>

<style scoped>
/* 页脚样式 */
.footer {
  background: linear-gradient(135deg, #1a252f 0%, #2c3e50 100%);
  color: white;
  padding: 4rem 0 2rem;
  width: 100%;
  margin: 0;
  max-width: 100vw;
  overflow: hidden !important;
  position: relative;
  opacity: 0;
  transform: translateY(30px);
  transition: all 1s ease;
}

.footer.animate-in {
  opacity: 1;
  transform: translateY(0);
}

.footer-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  overflow: hidden;
}

.footer-wave {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 60px;
  background: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 1200 120' preserveAspectRatio='none'%3E%3Cpath d='M985.66,92.83C906.67,72,823.78,31,743.84,14.19c-82.26-17.34-168.06-16.33-250.45.39-57.84,11.73-114,31.07-172,41.86A600.21,600.21,0,0,1,0,27.35V120H1200V95.8C1132.19,118.92,1055.71,111.31,985.66,92.83Z' fill='%2334495e'/%3E%3C/svg%3E")
    repeat-x;
  background-size: 1200px 60px;
  animation: waveMove 10s ease-in-out infinite;
}

.footer-container {
  margin: 0 auto;
  padding: 0 2rem;
  width: 100%;
  box-sizing: border-box;
  position: relative;
  z-index: 2;
}

.footer-content {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 3rem;
  margin-bottom: 3rem;
}

.footer-card {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(10px);
  border-radius: 25px;
  padding: 2.5rem 2rem;
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.footer-card::before {
  content: "";
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    90deg,
    transparent,
    rgba(255, 255, 255, 0.1),
    transparent
  );
  transition: left 0.8s ease;
}

.footer-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.3);
}

.footer-card:hover::before {
  left: 100%;
}

.footer-icon {
  width: 60px;
  height: 60px;
  background: linear-gradient(45deg, #3498db, #2ecc71);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 1.5rem;
  color: white;
  transition: transform 0.3s ease;
}

.footer-icon:hover,
.footer-card:hover .footer-icon {
  transform: scale(1.1) rotate(5deg);
}

.footer-card h4 {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  color: #ecf0f1;
  font-weight: 600;
}

.footer-address {
  margin: 1rem 0;
}

.footer-address p {
  color: #bdc3c7;
  line-height: 1.6;
  margin-bottom: 0.3rem;
}

.contact-phone {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: #3498db;
  font-weight: 500;
  margin-top: 1rem;
}

.contact-phone svg {
  color: #2ecc71;
}

.footer-card p {
  color: #bdc3c7;
  line-height: 1.6;
  margin-bottom: 0.5rem;
}

.social-links {
  display: flex;
  gap: 1rem;
  margin-top: 1.5rem;
}

.social-link {
  width: 40px;
  height: 40px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #bdc3c7;
  transition: all 0.3s ease;
  cursor: pointer;
}

.social-link:hover {
  background: linear-gradient(45deg, #3498db, #2ecc71);
  color: white;
  transform: translateY(-3px);
}

.copyright-section {
  text-align: center;
  position: relative;
}

.copyright-line {
  width: 100px;
  height: 2px;
  background: linear-gradient(45deg, #3498db, #2ecc71);
  margin: 0 auto 2rem;
  border-radius: 1px;
  animation: pulse 2s ease-in-out infinite;
}

.copyright {
  color: #7f8c8d;
  font-size: 0.9rem;
}

/* 动画关键帧 */
@keyframes waveMove {
  0%,
  100% {
    transform: translateX(0);
  }
  50% {
    transform: translateX(-50px);
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
  .footer-container {
    padding: 0 1rem;
    width: 100%;
  }

  .footer-content {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .footer-card {
    padding: 2rem 1.5rem;
    border-radius: 20px;
  }
}

@media (max-width: 768px) {
  .footer {
    padding: 3rem 0 1.5rem;
  }

  .footer-icon {
    width: 50px;
    height: 50px;
  }

  .footer-card h4 {
    font-size: 1.3rem;
  }

  .social-links {
    justify-content: center;
  }
}
</style>
