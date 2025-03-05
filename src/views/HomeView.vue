<script setup lang="ts">
import { onMounted } from 'vue'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

onMounted(() => {
    document.body.classList.add('cyber-background')

    // Hero section animation
    gsap.from('.hero', {
        opacity: 0,
        y: 50,
        duration: 1,
        scrollTrigger: {
            trigger: '.hero',
            start: 'top center',
            end: 'bottom center',
            toggleActions: 'play none none reverse',
            markers: false
        }
    })

    // Content section animation
    gsap.from('.content-section', {
        opacity: 0,
        scale: 0.95,
        duration: 0.8,
        scrollTrigger: {
            trigger: '.content-section',
            start: 'top 80%',
            end: 'bottom center',
            toggleActions: 'play none none reverse',
            markers: false
        }
    })


    // Tech section animation
    gsap.from('.tech-section', {
        opacity: 0,
        x: -50,
        duration: 1,
        scrollTrigger: {
            trigger: '.tech-section',
            start: 'top 80%',
            end: 'bottom center',
            toggleActions: 'play none none reverse',
            markers: false
        }
    })

})
</script>

<template>
    <div class="cyber-main">
        <div class="hero parallax-section">
            <h2 class="neon-heading">欢迎来到赛博空间</h2>
            <p class="glow-text">探索未来科技的无限可能</p>
            <div class="scroll-indicator"></div>
        </div>

        <div class="featured-products">
            <h3 class="section-title">精选产品</h3>
            <div class="product-grid">
                <div v-for="n in 4" :key="n" class="product-card">
                    <div class="product-image">
                        <img :src="`https://picsum.photos/400/500?random=${n}`" :alt="`产品${n}`">
                        <div class="product-overlay">
                            <button class="quick-view">快速查看</button>
                        </div>
                    </div>
                    <div class="product-info">
                        <h4>产品名称 #{{ n }}</h4>
                        <p class="price">¥{{ 199 + n * 100 }}.00</p>
                    </div>
                </div>
            </div>
        </div>

        <div class="content-section parallax-section">
            <h3 class="section-title">核心服务</h3>
            <div class="service-grid">
                <div v-for="n in 3" :key="n" class="service-card">
                    <div class="progress-ring">
                        <svg width="120" height="120" viewBox="0 0 120 120">
                            <circle class="progress-ring-circle-bg" stroke="rgba(0, 255, 255, 0.1)" stroke-width="8"
                                fill="transparent" r="52" cx="60" cy="60" />
                            <circle class="progress-ring-circle"
                                :style="{ strokeDashoffset: 326.726 * (1 - (n * 25) / 100) }" stroke="#0ff"
                                stroke-width="8" fill="transparent" r="52" cx="60" cy="60" />
                            <text x="60" y="60" text-anchor="middle" dominant-baseline="middle" class="progress-text">{{
                    n * 25 }}%</text>
                        </svg>
                    </div>
                    <h4>智能解决方案 #{{ n }}</h4>
                    <p>提供专业的技术支持和创新解决方案</p>
                </div>
            </div>
        </div>

        <div class="tech-section parallax-section">
            <h3 class="section-title">技术优势</h3>
            <div class="tech-grid">
                <div v-for="tech in ['AI推理引擎', '区块链共识', '边缘计算']" :key="tech" class="tech-card">
                    <div class="tech-icon">
                        <i :class="{
                            'fas fa-brain': tech === 'AI推理引擎',
                            'fas fa-link': tech === '区块链共识',
                            'fas fa-microchip': tech === '边缘计算'
                        }"></i>
                    </div>
                    <h4>{{ tech }}</h4>
                    <p>领先的技术创新能力</p>
                    <div class="tech-stats">
                        <div class="stat-item">
                            <span class="stat-value">99%</span>
                            <span class="stat-label">准确率</span>
                        </div>
                        <div class="stat-item">
                            <span class="stat-value">10x</span>
                            <span class="stat-label">性能提升</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.hero {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 0 1rem;
    position: relative;
    z-index: 1;
}

.neon-heading {
    color: #0ff;
    text-shadow: 0 0 10px #0ff;
    font-family: 'Orbitron', sans-serif;
    font-size: 4.5rem;
    font-weight: 700;
    animation: neonPulse 1.5s infinite alternate;
    margin-bottom: 2rem;
    text-align: center;
    letter-spacing: 2px;
    line-height: 1.2;
}

.glow-text {
    color: #9d9dff;
    text-shadow: 0 0 8px rgba(157, 157, 255, 0.8);
    font-size: 1.8rem;
    text-align: center;
    margin-bottom: 4rem;
    font-weight: 500;
    letter-spacing: 1px;
    line-height: 1.4;
}

.scroll-indicator {
    position: absolute;
    bottom: 3rem;
    left: 50%;
    transform: translateX(-50%);
    width: 30px;
    height: 50px;
    border: 2px solid #0ff;
    border-radius: 15px;
    opacity: 0.8;

    &::before {
        content: '';
        position: absolute;
        top: 6px;
        left: 50%;
        width: 6px;
        height: 6px;
        background: #0ff;
        border-radius: 50%;
        transform: translateX(-50%);
        animation: scrollIndicator 2s infinite;
    }
}

.cyber-main {
    padding-top: 56px;
    padding-bottom: 0;
    overflow-x: hidden;
    position: relative;
    z-index: 1;
}

.featured-products {
    padding: 4rem 2rem;
    max-width: 1400px;
    margin: 0 auto;
    background: rgba(26, 26, 47, 0.8);
    border-radius: 24px;
    border: 2px solid rgba(0, 255, 255, 0.3);
    box-shadow: 0 0 30px rgba(0, 255, 255, 0.1);
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
}

.product-grid {
    display: grid;
    gap: 2rem;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
}

.product-card {
    position: relative;
    background: rgba(26, 26, 47, 0.9);
    border: 1px solid rgba(0, 255, 255, 0.3);
    border-radius: 12px;
    overflow: hidden;
    transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    box-shadow: 0 0 20px rgba(0, 255, 255, 0.1);

    &:hover {
        transform: translateY(-10px);
        border-color: #0ff;
        box-shadow: 0 0 30px rgba(0, 255, 255, 0.3);

        .product-overlay {
            opacity: 1;
        }

        img {
            transform: scale(1.05);
        }
    }
}

.product-image {
    position: relative;
    padding-top: 125%;
    overflow: hidden;

    img {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        object-fit: cover;
        transition: transform 0.3s ease;
    }
}

.product-overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(26, 26, 47, 0.7);
    display: flex;
    justify-content: center;
    align-items: center;
    opacity: 0;
    transition: opacity 0.4s ease;
}

.quick-view {
    padding: 12px 24px;
    background: transparent;
    border: 2px solid #0ff;
    border-radius: 4px;
    color: #0ff;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
    text-shadow: 0 0 8px rgba(0, 255, 255, 0.5);

    &:hover {
        background: #0ff;
        color: #1a1a2f;
        box-shadow: 0 0 15px rgba(0, 255, 255, 0.5);
    }
}

.product-info {
    padding: 1.5rem;
    text-align: center;

    h4 {
        margin: 0 0 0.5rem;
        font-size: 1.1rem;
        color: #0ff;
        text-shadow: 0 0 8px rgba(0, 255, 255, 0.5);
    }

    .price {
        color: #9d9dff;
        font-weight: 600;
        margin: 0;
        text-shadow: 0 0 8px rgba(157, 157, 255, 0.5);
    }
}

.content-section {
    margin: 4rem auto;
    padding: 4rem 2rem;
    max-width: 1200px;
    border-radius: 24px;
    border: 2px solid rgba(0, 255, 255, 0.3);
    box-shadow: 0 0 30px rgba(0, 255, 255, 0.1);
    position: relative;
    z-index: 1;
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
}

.tech-section {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 3rem 2rem;
    max-width: 1200px;
    margin: 0 auto;
    position: relative;
    z-index: 1;
}

.tech-grid {
    display: grid;
    gap: 2rem;
    grid-template-columns: repeat(3, 1fr);
}

.tech-card {
    padding: 2rem;
    background: rgba(26, 26, 47, 0.9);
    border: 1px solid #00ffff;
    border-radius: 12px;
    text-align: center;
    color: #0ff;
    box-shadow: 0 0 20px rgba(0, 255, 255, 0.2);
    transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    position: relative;
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
}

.tech-icon {
    width: 80px;
    height: 80px;
    margin: 0 auto 1.5rem;
    background: rgba(0, 255, 255, 0.1);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    border: 2px solid rgba(0, 255, 255, 0.3);
}

.tech-icon i {
    font-size: 2.5rem;
    color: #0ff;
    text-shadow: 0 0 10px rgba(0, 255, 255, 0.5);
}

.tech-card h4 {
    margin: 1rem 0;
    font-size: 1.5rem;
    font-weight: 600;
    letter-spacing: 1px;
    text-shadow: 0 0 10px rgba(0, 255, 255, 0.5);
}

.tech-card p {
    color: #9d9dff;
    margin: 0 0 1.5rem;
    font-size: 1rem;
    line-height: 1.6;
}

.tech-stats {
    display: flex;
    justify-content: space-around;
    margin-top: 1.5rem;
    padding-top: 1.5rem;
    border-top: 1px solid rgba(0, 255, 255, 0.2);
}

.stat-item {
    text-align: center;
}

.stat-value {
    display: block;
    font-size: 1.8rem;
    font-weight: 700;
    color: #0ff;
    text-shadow: 0 0 10px rgba(0, 255, 255, 0.5);
    margin-bottom: 0.5rem;
}

.stat-label {
    display: block;
    font-size: 0.9rem;
    color: #9d9dff;
}

.tech-card:hover {
    transform: translateY(-10px);
    box-shadow: 0 0 30px rgba(0, 255, 255, 0.4);
    border-color: #0ff;
}

@media (max-width: 768px) {
    .tech-grid {
        grid-template-columns: 1fr;
        gap: 1.5rem;
    }

    .tech-card {
        padding: 1.5rem;
    }

    .tech-icon {
        width: 60px;
        height: 60px;
    }

    .tech-icon i {
        font-size: 2rem;
    }
}

.section-title {
    color: #0ff;
    font-family: 'Orbitron', sans-serif;
    text-align: center;
    margin-bottom: 3rem;
    font-size: 2rem;
}

.service-grid {
    display: grid;
    gap: 2.5rem;
    grid-template-columns: repeat(3, 1fr);
    padding: 1rem;
}

.service-card {
    padding: 2.5rem 2rem;
    background: rgba(255, 255, 255, 0.03);
    border: 1px solid rgba(0, 255, 255, 0.2);
    border-radius: 16px;
    text-align: center;
    color: #9d9dff;
    transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    position: relative;
    backdrop-filter: blur(12px);
    -webkit-backdrop-filter: blur(12px);
    display: flex;
    flex-direction: column;
    align-items: center;

    h4 {
        color: #0ff;
        margin: 1.2rem 0;
        font-size: 1.4rem;
        font-weight: 600;
        letter-spacing: 1px;
        text-shadow: 0 0 10px rgba(0, 255, 255, 0.5);
    }

    p {
        margin: 0;
        opacity: 0.9;
        font-size: 1.1rem;
        line-height: 1.6;
        color: rgba(157, 157, 255, 0.9);
    }

    &::before {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        border-radius: 16px;
        padding: 2px;
        background: linear-gradient(45deg, rgba(0, 255, 255, 0.5), rgba(0, 255, 255, 0.2));
        -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
        mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
        -webkit-mask-composite: xor;
        mask-composite: exclude;
        opacity: 0;
        transition: opacity 0.4s ease;
    }
}

.progress-ring {
    margin-bottom: 1.5rem;
}

.progress-ring-circle {
    transition: stroke-dashoffset 0.35s;
    transform: rotate(-90deg);
    transform-origin: 50% 50%;
    stroke-dasharray: 326.726;
}

.progress-text {
    fill: #0ff;
    font-size: 1.5rem;
    font-weight: bold;
    text-shadow: 0 0 8px rgba(0, 255, 255, 0.8);
}

.service-card:hover {
    transform: translateY(-8px);
    box-shadow: 0 8px 32px rgba(0, 255, 255, 0.15);
    background: rgba(255, 255, 255, 0.05);

    &::before {
        opacity: 1;
    }

    h4 {
        text-shadow: 0 0 15px rgba(0, 255, 255, 0.8);
    }
}

.tech-grid {
    display: grid;
    gap: 2rem;
    grid-template-columns: repeat(3, 1fr);
}

.tech-card {
    padding: 1.5rem;
    background: rgba(26, 26, 47, 0.8);
    border: 1px solid #00ffff;
    border-radius: 8px;
    text-align: center;
    color: #0ff;
    box-shadow: 0 0 12px rgba(0, 255, 255, 0.2);
    transition: all 0.3s ease;
    position: relative;

    h4 {
        margin: 1rem 0;
    }

    p {
        color: #9d9dff;
        margin: 0;
        font-size: 0.9rem;
    }
}

.tech-card:hover {
    box-shadow: 0 0 20px rgba(0, 255, 255, 0.4);
    transform: scale(1.05);
}

.neon-heading {
    color: #0ff;
    text-shadow: 0 0 10px #0ff;
    font-family: 'Orbitron', sans-serif;
    font-size: 3rem;
    animation: neonPulse 1.5s infinite alternate;
    margin-bottom: 1.5rem;
    text-align: center;
}

.glow-text {
    color: #9d9dff;
    text-shadow: 0 0 8px rgba(157, 157, 255, 0.8);
    font-size: 1.5rem;
    text-align: center;
    margin-bottom: 3rem;
}

@keyframes scrollIndicator {
    0% {
        transform: translate(-50%, 0);
        opacity: 1;
    }

    50% {
        transform: translate(-50%, 10px);
        opacity: 0.5;
    }

    100% {
        transform: translate(-50%, 0);
        opacity: 1;
    }
}

@keyframes neonPulse {
    from {
        text-shadow: 0 0 10px #0ff;
    }

    to {
        text-shadow: 0 0 20px #0ff, 0 0 30px #0ff;
    }
}

@media (max-width: 1024px) {
    .service-grid {
        grid-template-columns: repeat(2, 1fr);
        gap: 2rem;
    }
}

@media (max-width: 768px) {
    .tech-grid {
        grid-template-columns: 1fr;
    }

    .neon-heading {
        font-size: 2rem;
    }

    .glow-text {
        font-size: 1.2rem;
    }

    .product-grid {
        grid-template-columns: 1fr;
    }
}

.progress-ring {
    margin-bottom: 2rem;
    position: relative;
}

.progress-ring-circle-bg {
    stroke-width: 12px;
    opacity: 0.2;
}

.progress-ring-circle {
    stroke-dasharray: 326.726;
    transform: rotate(-90deg);
    transform-origin: 50% 50%;
    transition: stroke-dashoffset 0.8s ease;
    stroke-width: 12px;
}

.progress-text {
    font-family: 'Orbitron', sans-serif;
    font-size: 24px;
    fill: #0ff;
    font-weight: 600;
    text-shadow: 0 0 8px rgba(0, 255, 255, 0.8);
}
</style>