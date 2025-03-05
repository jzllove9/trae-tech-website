<script setup lang="ts">
// 页面初始化逻辑（如有需要可后续补充）
</script>

<template>
  <main class="page-container">
    <section class="content-section">
      <h2>关于我们</h2>
      <p>专业的技术团队创造卓越数字体验</p>
    </section>

    <section class="content-section">
      <h3>核心价值</h3>
      <div class="grid-container">
        <div v-for="n in 3" class="value-card">
          创新技术方案 {{n}}
        </div>
      </div>
    </section>

    <section class="content-section">
      <h3>发展历程</h3>
      <div class="timeline">
        <div v-for="year in [2019,2021,2023]" class="milestone">
          里程碑 {{year}}
        </div>
      </div>
    </section>
  </main>
</template>

<style scoped>
.page-container {
  padding: 80px 24px 120px;
  max-width: 1200px;
  margin: 0 auto;
}

.content-section {
  margin-bottom: 80px;
  padding: 40px;
  background: rgba(255,255,255,0.9);
  border-radius: 16px;
  box-shadow: 0 8px 32px rgba(0,0,0,0.1);
}

.grid-container {
  display: grid;
  gap: 24px;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
}

.value-card {
  padding: 20px;
  border: 1px solid #e5e6eb;
  border-radius: 8px;
}
</style>