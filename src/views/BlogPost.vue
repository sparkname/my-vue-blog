<template>
  <div class="blog-post" v-if="post">
    <div class="container">
      <!-- 文章头部 -->
      <div class="post-header">
        <div class="post-meta">
          <span class="post-category">{{ post.category }}</span>
          <span class="post-date">{{ formatDate(post.date) }}</span>
        </div>
        <h1 class="post-title">{{ post.title }}</h1>
        <div class="post-tags">
          <span v-for="tag in post.tags" :key="tag" class="tag">{{ tag }}</span>
        </div>
      </div>

      <!-- 文章图片 -->
      <div class="post-image" v-if="post.image">
        <img :src="post.image" :alt="post.title" />
      </div>

      <!-- 文章内容 -->
      <div class="post-content">
        <div v-html="post.content"></div>
      </div>

      <!-- 导航按钮 -->
      <div class="post-navigation">
        <router-link to="/blog" class="back-btn">← 返回博客列表</router-link>
        <div class="nav-buttons">
          <button v-if="prevPost" @click="goToPost(prevPost.id)" class="nav-btn prev">
            ← {{ prevPost.title }}
          </button>
          <button v-if="nextPost" @click="goToPost(nextPost.id)" class="nav-btn next">
            {{ nextPost.title }} →
          </button>
        </div>
      </div>
    </div>
  </div>
  <div v-else class="not-found">
    <div class="container">
      <h1>文章未找到</h1>
      <p>抱歉，您访问的文章不存在。</p>
      <router-link to="/blog" class="back-btn">返回博客列表</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BlogPost',
  props: ['id'],
  data() {
    return {
      posts: [
        {
          id: 1,
          title: 'Vue 3 Composition API 实践指南',
          excerpt: '深入了解Vue 3的Composition API，学习如何在实际项目中使用这个强大的新特性。',
          date: '2024-01-15',
          category: '前端开发',
          tags: ['Vue3', 'JavaScript', 'Composition API'],
          image: 'https://via.placeholder.com/800x400/007bff/ffffff?text=Vue+3',
          content: `
            <h2>什么是 Composition API？</h2>
            <p>Composition API 是 Vue 3 中引入的一套全新的 API，它提供了一种更灵活、更可组合的方式来编写组件逻辑。</p>
            
            <h3>主要优势</h3>
            <ul>
              <li><strong>更好的逻辑复用</strong>：通过组合函数，可以轻松地在组件间共享逻辑</li>
              <li><strong>更好的类型推导</strong>：对 TypeScript 的支持更加友好</li>
              <li><strong>更灵活的代码组织</strong>：相关逻辑可以组织在一起，而不是分散在不同的选项中</li>
            </ul>

            <h3>基本用法</h3>
            <pre><code>import { ref, computed, onMounted } from 'vue'

export default {
  setup() {
    const count = ref(0)
    const doubleCount = computed(() => count.value * 2)
    
    const increment = () => {
      count.value++
    }
    
    onMounted(() => {
      console.log('组件已挂载')
    })
    
    return {
      count,
      doubleCount,
      increment
    }
  }
}</code></pre>

            <h3>与 Options API 的对比</h3>
            <p>虽然 Composition API 提供了更多的灵活性，但这并不意味着 Options API 被弃用。Vue 3 完全兼容 Options API，开发者可以根据项目需求选择合适的 API 风格。</p>

            <h3>总结</h3>
            <p>Composition API 是 Vue 3 的一个重要特性，它为开发者提供了更多的选择和灵活性。通过合理使用 Composition API，我们可以编写出更加模块化、可维护的代码。</p>
          `
        },
        {
          id: 2,
          title: 'CSS Grid 布局完全指南',
          excerpt: 'CSS Grid是现代网页布局的强大工具，本文将带你从基础到高级全面掌握Grid布局技术。',
          date: '2024-01-10',
          category: '前端开发',
          tags: ['CSS', 'Grid', '布局'],
          image: 'https://via.placeholder.com/800x400/28a745/ffffff?text=CSS+Grid',
          content: `
            <h2>CSS Grid 简介</h2>
            <p>CSS Grid Layout 是一个二维布局系统，为 Web 开发者提供了前所未有的布局控制能力。</p>
            
            <h3>基本概念</h3>
            <ul>
              <li><strong>Grid Container</strong>：设置了 display: grid 的元素</li>
              <li><strong>Grid Item</strong>：Grid Container 的直接子元素</li>
              <li><strong>Grid Line</strong>：构成网格结构的分界线</li>
              <li><strong>Grid Track</strong>：两条相邻网格线之间的空间</li>
            </ul>

            <h3>创建网格</h3>
            <pre><code>.container {
  display: grid;
  grid-template-columns: 200px 200px 200px;
  grid-template-rows: 100px 100px;
  gap: 10px;
}</code></pre>

            <h3>响应式网格</h3>
            <pre><code>.responsive-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}</code></pre>

            <p>这种布局会自动调整列数，确保每列至少 250px 宽，并且充分利用可用空间。</p>
          `
        },
        {
          id: 3,
          title: 'JavaScript 异步编程最佳实践',
          excerpt: '探讨JavaScript中的异步编程模式，包括Promise、async/await的使用技巧和最佳实践。',
          date: '2024-01-05',
          category: '前端开发',
          tags: ['JavaScript', '异步编程', 'Promise'],
          image: 'https://via.placeholder.com/800x400/ffc107/ffffff?text=JavaScript',
          content: `
            <h2>异步编程的重要性</h2>
            <p>在 JavaScript 中，异步编程是处理耗时操作（如网络请求、文件读取等）的重要方式。</p>
            
            <h3>Promise 基础</h3>
            <pre><code>const fetchData = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('数据获取成功')
    }, 1000)
  })
}

fetchData()
  .then(data => console.log(data))
  .catch(error => console.error(error))</code></pre>

            <h3>async/await 语法</h3>
            <pre><code>async function getData() {
  try {
    const data = await fetchData()
    console.log(data)
  } catch (error) {
    console.error(error)
  }
}</code></pre>

            <h3>并发处理</h3>
            <pre><code>// 并行执行多个异步操作
const [user, posts, comments] = await Promise.all([
  fetchUser(),
  fetchPosts(),
  fetchComments()
])</code></pre>

            <p>合理使用异步编程可以显著提升应用的性能和用户体验。</p>
          `
        }
      ]
    }
  },
  computed: {
    post() {
      return this.posts.find(p => p.id === parseInt(this.id))
    },
    currentIndex() {
      return this.posts.findIndex(p => p.id === parseInt(this.id))
    },
    prevPost() {
      return this.currentIndex > 0 ? this.posts[this.currentIndex - 1] : null
    },
    nextPost() {
      return this.currentIndex < this.posts.length - 1 ? this.posts[this.currentIndex + 1] : null
    }
  },
  methods: {
    formatDate(date) {
      return new Date(date).toLocaleDateString('zh-CN', {
        year: 'numeric',
        month: 'long',
        day: 'numeric'
      })
    },
    goToPost(id) {
      this.$router.push(`/blog/${id}`)
    }
  }
}
</script>

<style scoped>
.blog-post {
  padding: 80px 0;
  min-height: calc(100vh - 200px);
}

.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 0 20px;
}

.post-header {
  margin-bottom: 30px;
}

.post-meta {
  display: flex;
  gap: 15px;
  margin-bottom: 15px;
}

.post-category {
  background: #007bff;
  color: white;
  padding: 5px 12px;
  border-radius: 15px;
  font-size: 0.9rem;
  font-weight: 500;
}

.post-date {
  color: #666;
  font-size: 0.9rem;
}

.post-title {
  font-size: 2.5rem;
  color: #333;
  margin-bottom: 20px;
  line-height: 1.3;
}

.post-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.tag {
  background: #f8f9fa;
  color: #6c757d;
  padding: 5px 10px;
  border-radius: 5px;
  font-size: 0.85rem;
}

.post-image {
  margin-bottom: 40px;
}

.post-image img {
  width: 100%;
  height: auto;
  border-radius: 8px;
}

.post-content {
  line-height: 1.8;
  color: #333;
  margin-bottom: 50px;
}

.post-content :deep(h2) {
  font-size: 1.8rem;
  margin: 30px 0 15px 0;
  color: #333;
}

.post-content :deep(h3) {
  font-size: 1.4rem;
  margin: 25px 0 12px 0;
  color: #444;
}

.post-content :deep(p) {
  margin-bottom: 16px;
}

.post-content :deep(ul) {
  margin-bottom: 16px;
  padding-left: 20px;
}

.post-content :deep(li) {
  margin-bottom: 8px;
}

.post-content :deep(pre) {
  background: #f8f9fa;
  padding: 20px;
  border-radius: 5px;
  overflow-x: auto;
  margin: 20px 0;
}

.post-content :deep(code) {
  font-family: 'Monaco', 'Consolas', monospace;
  font-size: 0.9rem;
}

.post-navigation {
  border-top: 1px solid #eee;
  padding-top: 30px;
}

.back-btn {
  display: inline-block;
  color: #007bff;
  text-decoration: none;
  font-weight: 500;
  margin-bottom: 20px;
  transition: color 0.3s;
}

.back-btn:hover {
  color: #0056b3;
}

.nav-buttons {
  display: flex;
  justify-content: space-between;
  gap: 20px;
}

.nav-btn {
  background: #f8f9fa;
  border: 1px solid #dee2e6;
  padding: 10px 15px;
  border-radius: 5px;
  cursor: pointer;
  transition: all 0.3s;
  font-size: 0.9rem;
  max-width: 200px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.nav-btn:hover {
  background: #e9ecef;
}

.not-found {
  padding: 100px 0;
  text-align: center;
}

.not-found h1 {
  font-size: 2rem;
  color: #333;
  margin-bottom: 20px;
}

.not-found p {
  color: #666;
  margin-bottom: 30px;
}

@media (max-width: 768px) {
  .post-title {
    font-size: 2rem;
  }
  
  .nav-buttons {
    flex-direction: column;
  }
  
  .nav-btn {
    max-width: 100%;
  }
}
</style>
