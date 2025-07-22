<template>
  <div class="about">
    <div class="container">
      <!-- 个人简介 -->
      <section class="hero-section">
        <div class="hero-content">
          <div class="avatar">
            <img src="../assets/2D5101503CB6CB30B2FD2643F3FA8368.jpg" alt="我的头像" />
          </div>
          <div class="hero-text">
            <h1>你好，我是 <span class="highlight">Lin</span></h1>
            <p class="subtitle">前端开发工程师 & 技术博主</p>
            <p class="description">
              热爱编程，专注于前端技术的学习与实践。
              喜欢分享技术心得，帮助更多人成长。
            </p>
          </div>
        </div>
      </section>

      <!-- 技能展示 -->
      <section class="skills-section">
        <h2 class="section-title">技能专长</h2>
        <div class="skills-grid">
          <div class="skill-card" v-for="skill in skills" :key="skill.name">
            <div class="skill-icon">{{ skill.icon }}</div>
            <h3>{{ skill.name }}</h3>
            <p>{{ skill.description }}</p>
            <div class="skill-level">
              <div class="level-bar">
                <div 
                  class="level-fill" 
                  :style="{ width: skill.level + '%' }"
                ></div>
              </div>
              <span class="level-text">{{ skill.level }}%</span>
            </div>
          </div>
        </div>
      </section>

      <!-- 经历时间线 -->
      <section class="experience-section">
        <h2 class="section-title">学习经历</h2>
        <div class="timeline">
          <div 
            class="timeline-item" 
            v-for="(item, index) in experiences" 
            :key="index"
          >
            <div class="timeline-marker"></div>
            <div class="timeline-content">
              <div class="timeline-date">{{ item.date }}</div>
              <h3>{{ item.title }}</h3>
              <p>{{ item.description }}</p>
            </div>
          </div>
        </div>
      </section>

      <!-- 兴趣爱好 -->
      <section class="interests-section">
        <h2 class="section-title">兴趣爱好</h2>
        <div class="interests-grid">
          <div 
            class="interest-card" 
            v-for="interest in interests" 
            :key="interest.name"
            @click="goToInterestPage(interest.route)"
          >
            <div class="interest-icon">{{ interest.icon }}</div>
            <h3>{{ interest.name }}</h3>
            <p>{{ interest.description }}</p>
            <div class="view-more">点击查看更多 →</div>
          </div>
        </div>
      </section>

      <!-- 联系方式 -->
      <section class="contact-section">
        <h2 class="section-title">联系我</h2>
        <p class="contact-intro">欢迎与我交流技术或合作机会</p>
        <div class="contact-links">
          <a href="mailto:2911793994@qq.com" class="contact-link">
            📧 2911793994@qq.com
          </a>
          <a href="https://github.com" target="_blank" class="contact-link">
            🐙 GitHub
          </a>
          <a href="https://weibo.com" target="_blank" class="contact-link">
            🐦 微博
          </a>
          <a href="https://zhihu.com" target="_blank" class="contact-link">
            📚 知乎
          </a>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'About',
  data() {
    return {
      skills: [
        {
          name: 'Vue.js',
          description: '熟练掌握Vue 2/3，包括Composition API、Vuex、Vue Router等',
          level: 90,
          icon: '⚡'
        },
        {
          name: 'JavaScript',
          description: '深入理解ES6+语法，异步编程，函数式编程等概念',
          level: 85,
          icon: '🚀'
        },
        {
          name: 'CSS/SCSS',
          description: '熟悉现代CSS技术，Grid、Flexbox、动画等',
          level: 80,
          icon: '🎨'
        },
        {
          name: 'Node.js',
          description: '具备后端开发能力，熟悉Express、Koa等框架',
          level: 70,
          icon: '⚙️'
        },
        {
          name: 'TypeScript',
          description: '类型安全的JavaScript开发，提高代码质量',
          level: 75,
          icon: '📘'
        },
        {
          name: 'Git',
          description: '版本控制，团队协作，CI/CD流程',
          level: 85,
          icon: '🔧'
        }
      ],
      experiences: [
        {
          date: '2023年',
          title: '开始技术博客写作',
          description: '开始在个人博客分享技术文章，累计发布文章50+篇，获得良好反馈。'
        },
        {
          date: '2022年',
          title: '深入学习Vue 3',
          description: '系统学习Vue 3新特性，包括Composition API、Teleport等，并在实际项目中应用。'
        },
        {
          date: '2021年',
          title: '前端开发之路',
          description: '开始专注前端开发，学习HTML、CSS、JavaScript等基础技术。'
        },
        {
          date: '2020年',
          title: '编程启蒙',
          description: '第一次接触编程，被代码的魅力所吸引，决定投身技术行业。'
        }
      ],
      interests: [
        {
          name: '阅读',
          description: '喜欢阅读技术书籍和文学作品',
          icon: '📚',
          route: '/interests/reading'
        },
        {
          name: '摄影',
          description: '用镜头记录生活的美好瞬间',
          icon: '📷',
          route: '/interests/photography'
        },
        {
          name: '旅行',
          description: '探索不同的城市和文化',
          icon: '✈️',
          route: '/interests/travel'
        },
        {
          name: '音乐',
          description: '在音乐中寻找编程的灵感',
          icon: '🎵',
          route: '/interests/music'
        }
      ]
    }
  },
  methods: {
    goToInterestPage(route) {
      this.$router.push(route);
    }
  }
}
</script>

<style scoped>
.about {
  padding: 80px 0;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

/* 英雄区域 */
.hero-section {
  margin-bottom: 80px;
}

.hero-content {
  display: grid;
  grid-template-columns: 200px 1fr;
  gap: 40px;
  align-items: center;
}

.avatar {
  text-align: center;
}

.avatar img {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  object-fit: cover;
  border: 4px solid #007bff;
}

.hero-text h1 {
  font-size: 2.5rem;
  color: #333;
  margin-bottom: 10px;
}

.highlight {
  color: #007bff;
}

.subtitle {
  font-size: 1.2rem;
  color: #666;
  margin-bottom: 15px;
}

.description {
  font-size: 1.1rem;
  line-height: 1.6;
  color: #555;
}

/* 通用区域样式 */
.section-title {
  font-size: 2.2rem;
  text-align: center;
  color: #333;
  margin-bottom: 50px;
  position: relative;
}

.section-title::after {
  content: '';
  position: absolute;
  bottom: -10px;
  left: 50%;
  transform: translateX(-50%);
  width: 50px;
  height: 3px;
  background: #007bff;
}

/* 技能区域 */
.skills-section {
  margin-bottom: 80px;
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 30px;
}

.skill-card {
  background: white;
  padding: 30px;
  border-radius: 10px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  text-align: center;
  transition: transform 0.3s;
}

.skill-card:hover {
  transform: translateY(-5px);
}

.skill-icon {
  font-size: 3rem;
  margin-bottom: 15px;
}

.skill-card h3 {
  font-size: 1.3rem;
  color: #333;
  margin-bottom: 10px;
}

.skill-card p {
  color: #666;
  line-height: 1.6;
  margin-bottom: 20px;
}

.skill-level {
  display: flex;
  align-items: center;
  gap: 10px;
}

.level-bar {
  flex: 1;
  height: 8px;
  background: #e9ecef;
  border-radius: 4px;
  overflow: hidden;
}

.level-fill {
  height: 100%;
  background: linear-gradient(90deg, #007bff, #28a745);
  transition: width 0.3s;
}

.level-text {
  font-weight: 600;
  color: #007bff;
  font-size: 0.9rem;
}

/* 经历时间线 */
.experience-section {
  margin-bottom: 80px;
}

.timeline {
  max-width: 800px;
  margin: 0 auto;
  position: relative;
}

.timeline::before {
  content: '';
  position: absolute;
  left: 30px;
  top: 0;
  bottom: 0;
  width: 2px;
  background: #007bff;
}

.timeline-item {
  position: relative;
  margin-bottom: 40px;
  padding-left: 80px;
}

.timeline-marker {
  position: absolute;
  left: 20px;
  top: 5px;
  width: 20px;
  height: 20px;
  background: #007bff;
  border-radius: 50%;
  border: 4px solid white;
  box-shadow: 0 0 0 2px #007bff;
}

.timeline-content {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1);
}

.timeline-date {
  color: #007bff;
  font-weight: 600;
  font-size: 0.9rem;
  margin-bottom: 5px;
}

.timeline-content h3 {
  color: #333;
  margin-bottom: 10px;
}

.timeline-content p {
  color: #666;
  line-height: 1.6;
}

/* 兴趣爱好 */
.interests-section {
  margin-bottom: 80px;
}

.interests-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 30px;
}

.interest-card {
  background: white;
  padding: 30px;
  border-radius: 10px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  text-align: center;
  transition: all 0.3s;
  cursor: pointer;
  position: relative;
  overflow: hidden;
}

.interest-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 25px rgba(0, 123, 255, 0.2);
}

.interest-card:active {
  transform: translateY(-2px);
}

.interest-icon {
  font-size: 3rem;
  margin-bottom: 15px;
}

.interest-card h3 {
  color: #333;
  margin-bottom: 10px;
}

.interest-card p {
  color: #666;
  line-height: 1.6;
  margin-bottom: 15px;
}

.view-more {
  color: #007bff;
  font-size: 0.9rem;
  font-weight: 600;
  opacity: 0;
  transform: translateY(10px);
  transition: all 0.3s;
}

.interest-card:hover .view-more {
  opacity: 1;
  transform: translateY(0);
}

/* 联系方式 */
.contact-section {
  text-align: center;
  background: #f8f9fa;
  padding: 50px;
  border-radius: 15px;
}

.contact-intro {
  font-size: 1.1rem;
  color: #666;
  margin-bottom: 30px;
}

.contact-links {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 20px;
}

.contact-link {
  display: inline-block;
  padding: 12px 24px;
  background: white;
  color: #333;
  text-decoration: none;
  border-radius: 25px;
  box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1);
  transition: all 0.3s;
  font-weight: 500;
}

.contact-link:hover {
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
  color: #007bff;
}

@media (max-width: 768px) {
  .hero-content {
    grid-template-columns: 1fr;
    text-align: center;
    gap: 20px;
  }
  
  .skills-grid,
  .interests-grid {
    grid-template-columns: 1fr;
  }
  
  .timeline {
    padding-left: 0;
  }
  
  .timeline::before {
    left: 15px;
  }
  
  .timeline-item {
    padding-left: 50px;
  }
  
  .timeline-marker {
    left: 5px;
  }
  
  .contact-links {
    flex-direction: column;
    align-items: center;
  }
}
</style>
