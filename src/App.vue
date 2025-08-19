<script setup lang="ts">
import HeroSection from './components/HeroSection.vue'
import FeaturesSection from './components/FeaturesSection.vue'
import ContactSection from './components/ContactSection.vue'
import FooterSection from './components/FooterSection.vue'
</script>

<template>
  <div class="app">
    <!-- 主要内容区域 -->
    <main class="main-content">
      <HeroSection />
      <FeaturesSection />
      <ContactSection />
      <FooterSection />
    </main>
  </div>
</template>

<style>
/* 全局样式 - 不使用scoped */
html,
body,
#app {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  max-width: 100vw !important;
  box-sizing: border-box !important;
}

body {
  font-family: 'Inter', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  line-height: 1.6;
  color: #333;
  background-color: #fff;
}

/* 确保所有元素不超出视口宽度 */
* {
  box-sizing: border-box;
}

.app {
  width: 100%;
  margin: 0;
  padding: 0;
  max-width: 100vw;
}
.main-content {
  padding-top: 0;
  width: 100%;
  max-width: 100vw;
  box-sizing: border-box;
}
</style>
