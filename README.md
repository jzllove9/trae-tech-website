
# 赛博空间 - Cyber Space

![赛博空间](https://via.placeholder.com/1200x630/1a1a2f/0ff?text=赛博空间)

## 项目简介

赛博空间是一个融合现代科技与未来感设计的前端展示项目，由 Trae 生成，采用赛博朋克风格打造沉浸式用户体验。项目使用 Vue 3 构建，结合 GSAP 动画库实现流畅的滚动效果和交互体验。

## 特色功能

- 🌟 沉浸式赛博朋克视觉体验
- 🔮 Three.js 粒子背景动画
- ✨ GSAP 驱动的滚动动画效果
- 📱 全响应式设计，适配各种设备
- 🎨 霓虹灯效果和现代 UI 组件

## 技术栈

- Vue 3 + TypeScript
- GSAP (GreenSock Animation Platform)
- Three.js
- CSS3 高级特性 (动画、过渡、变形等)
- 响应式设计

## 安装与运行

### 环境要求

- Node.js 16.0+
- npm 或 yarn

### 安装依赖

```bash
# 使用 npm
npm install

# 或使用 yarn
yarn install
```

### 开发模式运行

```bash
# 使用 npm
npm run dev

# 或使用 yarn
yarn dev
```

### 构建生产版本

```bash
# 使用 npm
npm run build

# 或使用 yarn
yarn build
```

## 项目结构

```
src/
├── assets/         # 静态资源
├── components/     # 组件
│   └── CyberNav.vue  # 导航组件
├── views/          # 页面
│   └── HomeView.vue  # 首页
├── App.vue         # 根组件
└── main.ts         # 入口文件
```

## 核心功能展示

### 粒子背景效果

使用 Three.js 创建动态粒子背景，增强沉浸式体验。

### 滚动动画

通过 GSAP 和 ScrollTrigger 实现元素随滚动出现的动画效果：

- 渐入渐出
- 缩放效果
- 位移动画

### 进度环展示

使用 SVG 创建动态进度环，展示核心服务的完成度。

### 产品展示区

响应式产品网格布局，带有悬停效果和快速查看功能。

## 自定义与配置

项目提供了多种自定义选项，可以根据需要调整：

- 颜色主题：修改 CSS 变量
- 动画持续时间：调整 GSAP 配置
- 响应式断点：根据目标设备调整媒体查询

## 贡献指南

欢迎提交 Pull Request 或创建 Issue 来改进项目。

## 许可证

[MIT License](LICENSE)
