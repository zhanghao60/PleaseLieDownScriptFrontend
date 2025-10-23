<template>
  <div class="home-page">
    <!-- 头部导航 -->
    <header class="header">
      <nav class="nav-container">
        <div class="nav-brand">
          <div class="logo">
            <div class="logo-icon">PLD</div>
            <span class="logo-text">Script</span>
          </div>
        </div>
        
        <div class="nav-menu">
          <a href="#home" class="nav-link">首页</a>
          <a href="#docs" class="nav-link">开发文档</a>
          <a href="#download" class="nav-link">软件下载</a>
          <a href="#features" class="nav-link">功能介绍</a>
          <a href="#about" class="nav-link">关于我们</a>
        </div>
        
        <div class="nav-actions">
          <button v-if="!isLoggedIn" @click="showLogin = true" class="login-btn">登录</button>
          <div v-else class="user-profile">
            <img :src="userAvatar" alt="用户头像" class="avatar" @click="toggleUserMenu">
            <div v-if="showUserMenu" class="user-menu">
              <a href="#profile" class="menu-item">个人中心</a>
              <a href="#settings" class="menu-item">设置</a>
              <button @click="logout" class="menu-item logout">退出登录</button>
            </div>
          </div>
        </div>
      </nav>
    </header>

    <!-- 主内容区域 -->
    <main class="main-content">
      <!-- 英雄区域 -->
      <section id="home" class="hero-section">
        <div class="hero-background">
          <div class="floating-shapes">
            <div class="shape shape-1"></div>
            <div class="shape shape-2"></div>
            <div class="shape shape-3"></div>
            <div class="shape shape-4"></div>
          </div>
        </div>
        
        <div class="hero-content">
          <div class="hero-text">
            <h1 class="hero-title">
              <span class="title-line">强大的脚本开发平台</span>
              <span class="title-line highlight">PLD Script</span>
            </h1>
            <p class="hero-description">
              专业的脚本开发工具，让您的创意变为现实。支持多种编程语言，
              提供丰富的API接口，让脚本开发变得简单高效。
            </p>
            <div class="hero-actions">
              <button class="btn-primary" @click="scrollToDownload">立即下载</button>
              <button class="btn-secondary" @click="scrollToDocs">查看文档</button>
            </div>
          </div>
          
          <div class="hero-visual">
            <div class="code-window">
              <div class="window-header">
                <div class="window-controls">
                  <span class="control red"></span>
                  <span class="control yellow"></span>
                  <span class="control green"></span>
                </div>
                <span class="window-title">script.js</span>
              </div>
              <div class="code-content">
                <div class="code-line">
                  <span class="line-number">1</span>
                  <span class="code-text">const pldScript = require('pld-script');</span>
                </div>
                <div class="code-line">
                  <span class="line-number">2</span>
                  <span class="code-text"></span>
                </div>
                <div class="code-line">
                  <span class="line-number">3</span>
                  <span class="code-text">// 创建自动化脚本</span>
                </div>
                <div class="code-line">
                  <span class="line-number">4</span>
                  <span class="code-text">const script = pldScript.create({</span>
                </div>
                <div class="code-line">
                  <span class="line-number">5</span>
                  <span class="code-text">  name: 'my-automation',</span>
                </div>
                <div class="code-line">
                  <span class="line-number">6</span>
                  <span class="code-text">  version: '1.0.0'</span>
                </div>
                <div class="code-line">
                  <span class="line-number">7</span>
                  <span class="code-text">});</span>
                </div>
                <div class="cursor"></div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- 功能介绍区域 -->
      <section id="features" class="features-section">
        <div class="container">
          <h2 class="section-title">核心功能</h2>
          <div class="features-grid">
            <div class="feature-card" v-for="feature in features" :key="feature.id">
              <div class="feature-icon">
                <i :class="feature.icon"></i>
              </div>
              <h3 class="feature-title">{{ feature.title }}</h3>
              <p class="feature-description">{{ feature.description }}</p>
            </div>
          </div>
        </div>
      </section>

      <!-- 下载区域 -->
      <section id="download" class="download-section">
        <div class="container">
          <h2 class="section-title">下载 PLD Script</h2>
          <p class="section-subtitle">选择适合您操作系统的版本</p>
          <div class="download-grid">
            <div class="download-card" v-for="platform in platforms" :key="platform.name">
              <div class="platform-icon">
                <i :class="platform.icon"></i>
              </div>
              <h3 class="platform-name">{{ platform.name }}</h3>
              <p class="platform-version">{{ platform.version }}</p>
              <button class="download-btn" @click="download(platform)">
                <i class="fas fa-download"></i>
                下载 {{ platform.name }}
              </button>
            </div>
          </div>
        </div>
      </section>

      <!-- 文档区域 -->
      <section id="docs" class="docs-section">
        <div class="container">
          <h2 class="section-title">开发文档</h2>
          <p class="section-subtitle">快速上手，深入学习</p>
          <div class="docs-grid">
            <div class="doc-card" v-for="doc in docs" :key="doc.id">
              <div class="doc-icon">
                <i :class="doc.icon"></i>
              </div>
              <h3 class="doc-title">{{ doc.title }}</h3>
              <p class="doc-description">{{ doc.description }}</p>
              <a :href="doc.link" class="doc-link">查看文档 <i class="fas fa-arrow-right"></i></a>
            </div>
          </div>
        </div>
      </section>
    </main>

    <!-- 底部 -->
    <footer class="footer">
      <div class="container">
        <div class="footer-content">
          <div class="footer-section">
            <div class="footer-brand">
              <div class="logo">
                <div class="logo-icon">PLD</div>
                <span class="logo-text">Script</span>
              </div>
              <p class="footer-description">
                专业的脚本开发平台，让您的创意变为现实。
              </p>
            </div>
          </div>
          
          <div class="footer-section">
            <h4 class="footer-title">产品</h4>
            <ul class="footer-links">
              <li><a href="#features">功能介绍</a></li>
              <li><a href="#download">软件下载</a></li>
              <li><a href="#docs">开发文档</a></li>
              <li><a href="#api">API 接口</a></li>
            </ul>
          </div>
          
          <div class="footer-section">
            <h4 class="footer-title">支持</h4>
            <ul class="footer-links">
              <li><a href="#help">帮助中心</a></li>
              <li><a href="#community">社区论坛</a></li>
              <li><a href="#contact">联系我们</a></li>
              <li><a href="#feedback">意见反馈</a></li>
            </ul>
          </div>
          
          <div class="footer-section">
            <h4 class="footer-title">关注我们</h4>
            <div class="social-links">
              <a href="#" class="social-link"><i class="fab fa-github"></i></a>
              <a href="#" class="social-link"><i class="fab fa-twitter"></i></a>
              <a href="#" class="social-link"><i class="fab fa-discord"></i></a>
              <a href="#" class="social-link"><i class="fab fa-telegram"></i></a>
            </div>
          </div>
        </div>
        
        <div class="footer-bottom">
          <p>&copy; 2024 PLD Script. 保留所有权利。</p>
          <div class="footer-legal">
            <a href="#privacy">隐私政策</a>
            <a href="#terms">服务条款</a>
          </div>
        </div>
      </div>
    </footer>

    <!-- 登录模态框 -->
    <div v-if="showLogin" class="modal-overlay" @click="showLogin = false">
      <div class="modal" @click.stop>
        <div class="modal-header">
          <h3>登录 PLD Script</h3>
          <button class="modal-close" @click="showLogin = false">&times;</button>
        </div>
        <div class="modal-body">
          <form @submit.prevent="handleLogin">
            <div class="form-group">
              <label for="email">邮箱</label>
              <input type="email" id="email" v-model="loginForm.email" required>
            </div>
            <div class="form-group">
              <label for="password">密码</label>
              <input type="password" id="password" v-model="loginForm.password" required>
            </div>
            <button type="submit" class="btn-primary full-width">登录</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, onMounted } from 'vue'

// 响应式数据
const isLoggedIn = ref(false)
const showLogin = ref(false)
const showUserMenu = ref(false)
const userAvatar = ref('https://via.placeholder.com/40x40/4f46e5/ffffff?text=U')

const loginForm = reactive({
  email: '',
  password: ''
})

// 功能数据
const features = ref([
  {
    id: 1,
    icon: 'fas fa-code',
    title: '多语言支持',
    description: '支持 JavaScript、Python、TypeScript 等多种编程语言'
  },
  {
    id: 2,
    icon: 'fas fa-rocket',
    title: '高性能执行',
    description: '优化的执行引擎，提供快速稳定的脚本运行环境'
  },
  {
    id: 3,
    icon: 'fas fa-shield-alt',
    title: '安全可靠',
    description: '内置安全机制，保护您的代码和数据安全'
  },
  {
    id: 4,
    icon: 'fas fa-puzzle-piece',
    title: '丰富插件',
    description: '海量插件生态，扩展脚本功能无限可能'
  },
  {
    id: 5,
    icon: 'fas fa-cloud',
    title: '云端同步',
    description: '支持云端存储和同步，随时随地访问您的脚本'
  },
  {
    id: 6,
    icon: 'fas fa-users',
    title: '团队协作',
    description: '支持团队开发，实时协作，提高开发效率'
  }
])

const platforms = ref([
  {
    name: 'Windows',
    icon: 'fab fa-windows',
    version: 'v2.1.0',
    downloadUrl: '#'
  },
  {
    name: 'macOS',
    icon: 'fab fa-apple',
    version: 'v2.1.0',
    downloadUrl: '#'
  },
  {
    name: 'Linux',
    icon: 'fab fa-linux',
    version: 'v2.1.0',
    downloadUrl: '#'
  }
])

const docs = ref([
  {
    id: 1,
    icon: 'fas fa-book',
    title: '快速开始',
    description: '5分钟快速上手 PLD Script',
    link: '#'
  },
  {
    id: 2,
    icon: 'fas fa-code',
    title: 'API 参考',
    description: '完整的 API 接口文档',
    link: '#'
  },
  {
    id: 3,
    icon: 'fas fa-graduation-cap',
    title: '教程指南',
    description: '从基础到高级的完整教程',
    link: '#'
  },
  {
    id: 4,
    icon: 'fas fa-question-circle',
    title: '常见问题',
    description: '解答您在使用中遇到的问题',
    link: '#'
  }
])

// 方法
const scrollToDownload = () => {
  document.getElementById('download').scrollIntoView({ behavior: 'smooth' })
}

const scrollToDocs = () => {
  document.getElementById('docs').scrollIntoView({ behavior: 'smooth' })
}

const download = (platform) => {
  // 模拟下载
  alert(`开始下载 ${platform.name} 版本`)
}

const handleLogin = () => {
  // 模拟登录
  isLoggedIn.value = true
  showLogin.value = false
  loginForm.email = ''
  loginForm.password = ''
}

const logout = () => {
  isLoggedIn.value = false
  showUserMenu.value = false
}

const toggleUserMenu = () => {
  showUserMenu.value = !showUserMenu.value
}

// 生命周期
onMounted(() => {
  // 添加滚动效果
  window.addEventListener('scroll', () => {
    const header = document.querySelector('.header')
    if (window.scrollY > 100) {
      header.classList.add('scrolled')
    } else {
      header.classList.remove('scrolled')
    }
  })
})
</script>

<style scoped>
/* 全局样式重置 */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.home-page {
  min-height: 100vh;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: #333;
}

/* 头部样式 */
.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
  transition: all 0.3s ease;
}

.header.scrolled {
  background: rgba(255, 255, 255, 0.98);
  box-shadow: 0 2px 20px rgba(0, 0, 0, 0.1);
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 70px;
}

.logo {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-weight: bold;
  font-size: 1.5rem;
}

.logo-icon {
  width: 40px;
  height: 40px;
  background: linear-gradient(135deg, #667eea, #764ba2);
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 8px;
  font-weight: bold;
}

.logo-text {
  color: #333;
}

.nav-menu {
  display: flex;
  gap: 2rem;
}

.nav-link {
  text-decoration: none;
  color: #333;
  font-weight: 500;
  transition: color 0.3s ease;
  position: relative;
}

.nav-link:hover {
  color: #667eea;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 0;
  height: 2px;
  background: #667eea;
  transition: width 0.3s ease;
}

.nav-link:hover::after {
  width: 100%;
}

.nav-actions {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.login-btn {
  background: linear-gradient(135deg, #667eea, #764ba2);
  color: white;
  border: none;
  padding: 0.5rem 1.5rem;
  border-radius: 25px;
  font-weight: 500;
  cursor: pointer;
  transition: transform 0.3s ease;
}

.login-btn:hover {
  transform: translateY(-2px);
}

.user-profile {
  position: relative;
}

.avatar {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  cursor: pointer;
  border: 2px solid #667eea;
  transition: transform 0.3s ease;
}

.avatar:hover {
  transform: scale(1.1);
}

.user-menu {
  position: absolute;
  top: 50px;
  right: 0;
  background: white;
  border-radius: 8px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  padding: 0.5rem 0;
  min-width: 150px;
}

.menu-item {
  display: block;
  padding: 0.5rem 1rem;
  text-decoration: none;
  color: #333;
  transition: background 0.3s ease;
}

.menu-item:hover {
  background: #f5f5f5;
}

.menu-item.logout {
  border-top: 1px solid #eee;
  background: none;
  border: none;
  width: 100%;
  text-align: left;
  cursor: pointer;
}

/* 主内容样式 */
.main-content {
  margin-top: 70px;
}

/* 英雄区域样式 */
.hero-section {
  min-height: 100vh;
  display: flex;
  align-items: center;
  position: relative;
  overflow: hidden;
}

.hero-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}

.floating-shapes {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}

.shape {
  position: absolute;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.1);
  animation: float 6s ease-in-out infinite;
}

.shape-1 {
  width: 80px;
  height: 80px;
  top: 20%;
  left: 10%;
  animation-delay: 0s;
}

.shape-2 {
  width: 120px;
  height: 120px;
  top: 60%;
  right: 10%;
  animation-delay: 2s;
}

.shape-3 {
  width: 60px;
  height: 60px;
  top: 40%;
  left: 80%;
  animation-delay: 4s;
}

.shape-4 {
  width: 100px;
  height: 100px;
  bottom: 20%;
  left: 20%;
  animation-delay: 1s;
}

@keyframes float {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  50% { transform: translateY(-20px) rotate(180deg); }
}

.hero-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
  position: relative;
  z-index: 2;
}

.hero-text {
  color: white;
}

.hero-title {
  font-size: 3.5rem;
  font-weight: bold;
  line-height: 1.2;
  margin-bottom: 1.5rem;
}

.title-line {
  display: block;
}

.title-line.highlight {
  background: linear-gradient(45deg, #ffd700, #ffed4e);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-description {
  font-size: 1.2rem;
  line-height: 1.6;
  margin-bottom: 2rem;
  opacity: 0.9;
}

.hero-actions {
  display: flex;
  gap: 1rem;
}

.btn-primary, .btn-secondary {
  padding: 1rem 2rem;
  border-radius: 50px;
  font-weight: 600;
  font-size: 1.1rem;
  cursor: pointer;
  transition: all 0.3s ease;
  border: none;
}

.btn-primary {
  background: linear-gradient(45deg, #ffd700, #ffed4e);
  color: #333;
}

.btn-primary:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 30px rgba(255, 215, 0, 0.3);
}

.btn-secondary {
  background: transparent;
  color: white;
  border: 2px solid white;
}

.btn-secondary:hover {
  background: white;
  color: #667eea;
  transform: translateY(-3px);
}

/* 代码窗口样式 */
.hero-visual {
  display: flex;
  justify-content: center;
}

.code-window {
  background: #1e1e1e;
  border-radius: 12px;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
  overflow: hidden;
  width: 100%;
  max-width: 500px;
}

.window-header {
  background: #2d2d2d;
  padding: 1rem;
  display: flex;
  align-items: center;
  gap: 1rem;
}

.window-controls {
  display: flex;
  gap: 0.5rem;
}

.control {
  width: 12px;
  height: 12px;
  border-radius: 50%;
}

.control.red { background: #ff5f56; }
.control.yellow { background: #ffbd2e; }
.control.green { background: #27ca3f; }

.window-title {
  color: #ccc;
  font-size: 0.9rem;
}

.code-content {
  padding: 1.5rem;
  font-family: 'Monaco', 'Menlo', monospace;
  position: relative;
}

.code-line {
  display: flex;
  margin-bottom: 0.5rem;
  align-items: center;
}

.line-number {
  color: #666;
  margin-right: 1rem;
  width: 20px;
  text-align: right;
  font-size: 0.9rem;
}

.code-text {
  color: #f8f8f2;
  font-size: 0.9rem;
}

.cursor {
  position: absolute;
  bottom: 1.5rem;
  left: 2.5rem;
  width: 2px;
  height: 20px;
  background: #ffd700;
  animation: blink 1s infinite;
}

@keyframes blink {
  0%, 50% { opacity: 1; }
  51%, 100% { opacity: 0; }
}

/* 通用容器样式 */
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

.section-title {
  font-size: 2.5rem;
  font-weight: bold;
  text-align: center;
  margin-bottom: 1rem;
  color: #333;
}

.section-subtitle {
  text-align: center;
  font-size: 1.2rem;
  color: #666;
  margin-bottom: 3rem;
}

/* 功能区域样式 */
.features-section {
  padding: 6rem 0;
  background: white;
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
}

.feature-card {
  background: white;
  padding: 2rem;
  border-radius: 16px;
  text-align: center;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.feature-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
}

.feature-icon {
  width: 80px;
  height: 80px;
  background: linear-gradient(135deg, #667eea, #764ba2);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 1.5rem;
  color: white;
  font-size: 2rem;
}

.feature-title {
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 1rem;
  color: #333;
}

.feature-description {
  color: #666;
  line-height: 1.6;
}

/* 下载区域样式 */
.download-section {
  padding: 6rem 0;
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
}

.download-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
}

.download-card {
  background: white;
  padding: 2rem;
  border-radius: 16px;
  text-align: center;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.download-card:hover {
  transform: translateY(-5px);
}

.platform-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
  color: #667eea;
}

.platform-name {
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 0.5rem;
  color: #333;
}

.platform-version {
  color: #666;
  margin-bottom: 1.5rem;
}

.download-btn {
  background: linear-gradient(135deg, #667eea, #764ba2);
  color: white;
  border: none;
  padding: 1rem 2rem;
  border-radius: 50px;
  font-weight: 600;
  cursor: pointer;
  transition: transform 0.3s ease;
  width: 100%;
}

.download-btn:hover {
  transform: translateY(-2px);
}

/* 文档区域样式 */
.docs-section {
  padding: 6rem 0;
  background: white;
}

.docs-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 2rem;
}

.doc-card {
  background: white;
  padding: 2rem;
  border-radius: 16px;
  border: 1px solid #eee;
  transition: all 0.3s ease;
}

.doc-card:hover {
  border-color: #667eea;
  box-shadow: 0 8px 30px rgba(102, 126, 234, 0.1);
}

.doc-icon {
  width: 60px;
  height: 60px;
  background: linear-gradient(135deg, #667eea, #764ba2);
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 1.5rem;
  color: white;
  font-size: 1.5rem;
}

.doc-title {
  font-size: 1.3rem;
  font-weight: bold;
  margin-bottom: 1rem;
  color: #333;
}

.doc-description {
  color: #666;
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

.doc-link {
  color: #667eea;
  text-decoration: none;
  font-weight: 600;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  transition: color 0.3s ease;
}

.doc-link:hover {
  color: #764ba2;
}

/* 底部样式 */
.footer {
  background: #1a1a1a;
  color: white;
  padding: 4rem 0 2rem;
}

.footer-content {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 3rem;
  margin-bottom: 3rem;
}

.footer-brand .logo {
  margin-bottom: 1rem;
}

.footer-description {
  color: #ccc;
  line-height: 1.6;
}

.footer-title {
  font-size: 1.2rem;
  font-weight: bold;
  margin-bottom: 1rem;
  color: white;
}

.footer-links {
  list-style: none;
}

.footer-links li {
  margin-bottom: 0.5rem;
}

.footer-links a {
  color: #ccc;
  text-decoration: none;
  transition: color 0.3s ease;
}

.footer-links a:hover {
  color: #667eea;
}

.social-links {
  display: flex;
  gap: 1rem;
}

.social-link {
  width: 40px;
  height: 40px;
  background: #333;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  text-decoration: none;
  transition: all 0.3s ease;
}

.social-link:hover {
  background: #667eea;
  transform: translateY(-2px);
}

.footer-bottom {
  border-top: 1px solid #333;
  padding-top: 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: #ccc;
}

.footer-legal {
  display: flex;
  gap: 2rem;
}

.footer-legal a {
  color: #ccc;
  text-decoration: none;
  transition: color 0.3s ease;
}

.footer-legal a:hover {
  color: #667eea;
}

/* 模态框样式 */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 2000;
}

.modal {
  background: white;
  border-radius: 16px;
  width: 90%;
  max-width: 400px;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
}

.modal-header {
  padding: 2rem 2rem 1rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid #eee;
}

.modal-header h3 {
  font-size: 1.5rem;
  font-weight: bold;
  color: #333;
}

.modal-close {
  background: none;
  border: none;
  font-size: 2rem;
  cursor: pointer;
  color: #666;
}

.modal-body {
  padding: 2rem;
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: 600;
  color: #333;
}

.form-group input {
  width: 100%;
  padding: 0.75rem;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-size: 1rem;
  transition: border-color 0.3s ease;
}

.form-group input:focus {
  outline: none;
  border-color: #667eea;
}

.full-width {
  width: 100%;
}

/* 响应式设计 */
@media (max-width: 768px) {
  .nav-menu {
    display: none;
  }
  
  .hero-content {
    grid-template-columns: 1fr;
    text-align: center;
  }
  
  .hero-title {
    font-size: 2.5rem;
  }
  
  .hero-actions {
    justify-content: center;
  }
  
  .features-grid,
  .download-grid,
  .docs-grid {
    grid-template-columns: 1fr;
  }
  
  .footer-bottom {
    flex-direction: column;
    gap: 1rem;
    text-align: center;
  }
  
  .footer-legal {
    justify-content: center;
  }
}

@media (max-width: 480px) {
  .nav-container {
    padding: 0 1rem;
  }
  
  .container {
    padding: 0 1rem;
  }
  
  .hero-title {
    font-size: 2rem;
  }
  
  .hero-actions {
    flex-direction: column;
  }
  
  .btn-primary,
  .btn-secondary {
    width: 100%;
  }
}
</style>
