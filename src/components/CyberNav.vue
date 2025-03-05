<script setup lang="ts">
import { ref } from 'vue'
const isMenuOpen = ref(false)
const menuItems = [
    { name: '首页', link: '/' },
    { name: '产品', link: '/products' },
    { name: '服务', link: '/services' },
    { name: '关于', link: '/about' }
]
</script>

<template>
    <nav class="cyber-nav">
        <div class="logo-container">
            <a href="/" class="brand-logo">
                <span class="logo-text">WELCOME</span>
            </a>
        </div>
        <div class="desktop-menu">
            <a v-for="item in menuItems" :key="item.name" :href="item.link">{{ item.name }}</a>
        </div>
        <div class="nav-actions">
            <button class="icon-btn">
                <i class="fas fa-search"></i>
            </button>
            <button class="icon-btn">
                <i class="fas fa-shopping-cart"></i>
                <span class="cart-badge">0</span>
            </button>
        </div>
        <div class="mobile-menu" @click="isMenuOpen = !isMenuOpen">
            <div class="hamburger"></div>
        </div>
        <Transition name="slide">
            <div v-show="isMenuOpen" class="drawer">
                <a v-for="item in menuItems" :key="item.name" :href="item.link">{{ item.name }}</a>
            </div>
        </Transition>
    </nav>
</template>

<style scoped>
.cyber-nav {
    --nav-bg: rgba(26, 26, 47, 0.8);
    --nav-border: rgba(0, 255, 255, 0.2);
    --color-primary: #0ff;
    --spacing-md: 16px;

    position: fixed;
    top: 0;
    width: 100%;
    height: 80px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 var(--spacing-md);
    background: var(--nav-bg);
    border-bottom: 1px solid var(--nav-border);
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
    z-index: 1000;
}

.logo-container {
    flex: 0 0 auto;
}

.brand-logo {
    text-decoration: none;
}

.logo-text {
    font-size: 28px;
    font-weight: 700;
    color: var(--color-primary);
    letter-spacing: 2px;
    text-shadow: 0 0 10px var(--color-primary);
    font-family: 'Orbitron', sans-serif;
}

.desktop-menu {
    flex: 1;
    display: flex;
    justify-content: center;
    gap: 32px;
}

.desktop-menu a {
    text-decoration: none;
    color: var(--color-primary);
    font-size: 16px;
    font-weight: 500;
    position: relative;
    padding: 8px 0;
    text-shadow: 0 0 8px rgba(0, 255, 255, 0.5);
    transition: text-shadow 0.3s ease;
}

.desktop-menu a::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 2px;
    background: var(--color-primary);
    transform: scaleX(0);
    transition: transform 0.3s ease;
    box-shadow: 0 0 8px var(--color-primary);
}

.desktop-menu a:hover {
    text-shadow: 0 0 15px var(--color-primary);
}

.desktop-menu a:hover::after {
    transform: scaleX(1);
}

.nav-actions {
    display: flex;
    gap: 16px;
    align-items: center;
    flex: 0 0 136px;
}

.icon-btn {
    background: none;
    border: none;
    padding: 8px;
    cursor: pointer;
    position: relative;
    transition: transform 0.3s ease;
}

.icon-btn:hover {
    transform: scale(1.1);
}

.icon-btn i {
    font-size: 20px;
    color: var(--color-primary);
    text-shadow: 0 0 8px var(--color-primary);
}

.cart-badge {
    position: absolute;
    top: 0;
    right: 0;
    background: #ff4d4d;
    color: white;
    font-size: 12px;
    width: 18px;
    height: 18px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: 0 0 8px rgba(255, 77, 77, 0.5);
}

.mobile-menu {
    display: none;
}

.hamburger {
    width: 24px;
    height: 2px;
    background: var(--color-primary);
    position: relative;
    box-shadow: 0 0 8px var(--color-primary);
}

.hamburger::before,
.hamburger::after {
    content: '';
    position: absolute;
    width: 24px;
    height: 2px;
    background: var(--color-primary);
    transition: all 0.3s ease;
    box-shadow: 0 0 8px var(--color-primary);
}

.hamburger::before {
    top: -6px;
}

.hamburger::after {
    bottom: -6px;
}

.drawer {
    position: fixed;
    top: 80px;
    right: 0;
    width: 240px;
    background: var(--nav-bg);
    box-shadow: -2px 0 10px rgba(0, 255, 255, 0.2);
    transform: translateX(100%);
    transition: transform 0.3s ease;
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
    border-left: 1px solid var(--nav-border);
}

.drawer a {
    display: block;
    padding: 16px;
    color: var(--color-primary);
    text-decoration: none;
    border-bottom: 1px solid var(--nav-border);
    transition: all 0.3s ease;
    text-shadow: 0 0 8px rgba(0, 255, 255, 0.5);
}

.drawer a:hover {
    background: rgba(0, 255, 255, 0.1);
    text-shadow: 0 0 15px var(--color-primary);
}

.slide-enter-active,
.slide-leave-active {
    transition: transform 0.3s ease;
}

.slide-enter-from,
.slide-leave-to {
    transform: translateX(100%);
}

.slide-enter-to,
.slide-leave-from {
    transform: translateX(0);
}

@media (max-width: 768px) {
    .desktop-menu,
    .nav-actions {
        display: none;
    }

    .mobile-menu {
        display: block;
    }

    .drawer {
        display: block;
    }

    .cyber-nav {
        height: 64px;
    }
}
</style>