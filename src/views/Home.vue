<template>
  <div class="home">
    <!-- 英雄区域 -->
    <section class="hero">
      <div class="hero-content">
        <h1 class="hero-title">欢迎来到我的博客</h1>
        <p class="hero-subtitle">分享技术心得，记录生活点滴</p>
        <router-link to="/blog" class="hero-button">浏览博客</router-link>
      </div>
    </section>

    <!-- 最新文章 -->
    <section class="latest-posts">
      <div class="container">
        <h2 class="section-title">最新文章</h2>
        <div class="posts-grid">
          <BlogCard 
            v-for="post in latestPosts" 
            :key="post.id" 
            :post="post"
          />
        </div>
        <div class="text-center">
          <router-link to="/blog" class="view-all">查看更多文章</router-link>
        </div>
      </div>
    </section>

    <!-- 关于我简介 -->
    <section class="about-preview">
      <div class="container">
        <div class="about-content">
          <div class="about-text">
            <h2>关于我</h2>
            <p>
              我是一名热爱技术的开发者，专注于前端开发和用户体验设计。
              在这个博客中，我会分享我的技术学习心得、项目经验以及生活感悟。
            </p>
            <router-link to="/about" class="learn-more">了解更多</router-link>
          </div>
          <div class="about-image">
            <img src="../assets/25685BA5B1324BFE89628223741426F4.gif" alt="关于我" />
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import BlogCard from '../components/BlogCard.vue'

export default {
  name: 'Home',
  components: {
    BlogCard
  },
  data() {
    return {
      latestPosts: [
        {
          id: 1,
          title: 'Vue 3 Composition API 实践指南',
          excerpt: '深入了解Vue 3的Composition API，学习如何在实际项目中使用这个强大的新特性...',
          date: '2024-01-15',
          category: '前端开发',
          tags: ['Vue3', 'JavaScript', 'Composition API'],
          image: '/image/Screenshot_2024-11-26-23-55-33-852_com.ss.android.ugc.aweme.jpg'
        },
        {
          id: 2,
          title: 'CSS Grid 布局完全指南',
          excerpt: 'CSS Grid是现代网页布局的强大工具，本文将带你从基础到高级全面掌握Grid布局...',
          date: '2024-01-10',
          category: '前端开发',
          tags: ['CSS', 'Grid', '布局'],
          image: '/image/Screenshot_2024-11-26-23-55-33-852_com.ss.android.ugc.aweme.jpg'
        },
        {
          id: 3,
          title: 'JavaScript 异步编程最佳实践',
          excerpt: '探讨JavaScript中的异步编程模式，包括Promise、async/await的使用技巧...',
          date: '2024-01-05',
          category: '前端开发',
          tags: ['JavaScript', '异步编程', 'Promise'],
          image: '/image/Screenshot_2024-11-26-23-55-33-852_com.ss.android.ugc.aweme.jpg'
        }
      ]
    }
  }
}
</script>

<style scoped>
.hero {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 120px 0 80px;
  text-align: center;
}

.hero-content {
  max-width: 800px;
  margin: 0 auto;
  padding: 0 20px;
}

.hero-title {
  font-size: 3rem;
  margin-bottom: 20px;
  font-weight: 700;
}

.hero-subtitle {
  font-size: 1.3rem;
  margin-bottom: 30px;
  opacity: 0.9;
}

.hero-button {
  display: inline-block;
  background: white;
  color: #667eea;
  padding: 15px 30px;
  border-radius: 30px;
  text-decoration: none;
  font-weight: 600;
  transition: transform 0.3s, box-shadow 0.3s;
}

.hero-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
}

.latest-posts {
  padding: 80px 0;
  background: #f8f9fa;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.section-title {
  text-align: center;
  font-size: 2.5rem;
  margin-bottom: 50px;
  color: #333;
}

.posts-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 30px;
  margin-bottom: 50px;
}

.text-center {
  text-align: center;
}

.view-all {
  color: #007bff;
  text-decoration: none;
  font-weight: 600;
  font-size: 1.1rem;
  transition: color 0.3s;
}

.view-all:hover {
  color: #0056b3;
}

.about-preview {
  padding: 80px 0;
}

.about-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 50px;
  align-items: center;
}

.about-text h2 {
  font-size: 2.5rem;
  margin-bottom: 20px;
  color: #333;
}

.about-text p {
  font-size: 1.1rem;
  line-height: 1.8;
  color: #666;
  margin-bottom: 30px;
}

.learn-more {
  color: #007bff;
  text-decoration: none;
  font-weight: 600;
  transition: color 0.3s;
}

.learn-more:hover {
  color: #0056b3;
}

.about-image {
  text-align: center;
}

.about-image img {
  max-width: 100%;
  height: auto;
  border-radius: 10px;
}

@media (max-width: 768px) {
  .hero-title {
    font-size: 2rem;
  }
  
  .posts-grid {
    grid-template-columns: 1fr;
  }
  
  .about-content {
    grid-template-columns: 1fr;
    text-align: center;
  }
}
</style>
