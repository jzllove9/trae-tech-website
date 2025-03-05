<script setup lang="ts">
</script>

<template>
  <main class="services-container">
    <section class="service-section">
      <h2>核心服务</h2>
      <div class="service-grid">
        <div 
          v-for="n in 3"
          :key="n"
          class="service-card"
        >
          数字化解决方案 #{{n}}
        </div>
      </div>
    </section>

    <section class="tech-stack">
      <h3>技术栈展示</h3>
      <div class="tech-icons">
        <div 
          v-for="tech in ['AI', '区块链', '物联网']"
          :key="tech"
          class="tech-item"
        >
          {{tech}}
        </div>
      </div>
    </section>
  </main>
</template>

<style scoped>
.services-container {
  padding: 100px 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.service-section {
  margin-bottom: 4rem;
  padding: 2rem;
  background: rgba(255,255,255,0.92);
  border-radius: 1rem;
}

.service-grid {
  display: grid;
  gap: 2rem;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
}

.service-card {
  padding: 1.5rem;
  border: 2px solid #0ff;
  border-radius: 8px;
  background: rgba(0, 255, 255, 0.05);
}

.tech-stack {
  padding: 3rem 2rem;
  background: linear-gradient(45deg, #1a1a2f, #0f0f1a);
  color: #0ff;
}

.tech-icons {
  display: flex;
  justify-content: center;
  gap: 2rem;
  margin-top: 2rem;
}

.tech-item {
  padding: 1rem 2rem;
  border: 1px solid #0ff;
  border-radius: 4px;
  box-shadow: 0 0 8px #0ff;
}
</style>