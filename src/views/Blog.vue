<template>
  <div class="blog">
    <div class="container">
      <div class="blog-header">
        <h1>博客文章</h1>
        <p>探索技术世界，分享知识与经验</p>
      </div>
      
      <!-- 搜索和筛选 -->
      <div class="blog-filters">
        <div class="search-box">
          <input 
            v-model="searchQuery" 
            type="text" 
            placeholder="搜索文章..."
            class="search-input"
          />
        </div>
        <div class="category-filter">
          <select v-model="selectedCategory" class="category-select">
            <option value="">所有分类</option>
            <option v-for="category in categories" :key="category" :value="category">
              {{ category }}
            </option>
          </select>
        </div>
      </div>

      <!-- 文章列表 -->
      <div class="posts-grid">
        <BlogCard 
          v-for="post in filteredPosts" 
          :key="post.id" 
          :post="post"
        />
      </div>

      <!-- 分页 -->
      <div class="pagination" v-if="totalPages > 1">
        <button 
          @click="currentPage--" 
          :disabled="currentPage === 1"
          class="page-btn"
        >
          上一页
        </button>
        <span class="page-info">
          第 {{ currentPage }} 页，共 {{ totalPages }} 页
        </span>
        <button 
          @click="currentPage++" 
          :disabled="currentPage === totalPages"
          class="page-btn"
        >
          下一页
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import BlogCard from '../components/BlogCard.vue'

export default {
  name: 'Blog',
  components: {
    BlogCard
  },
  data() {
    return {
      searchQuery: '',
      selectedCategory: '',
      currentPage: 1,
      postsPerPage: 6,
      posts: [
        {
          id: 1,
          title: 'Vue 3 Composition API 实践指南',
          excerpt: '深入了解Vue 3的Composition API，学习如何在实际项目中使用这个强大的新特性。本文将通过实际案例展示Composition API的优势和使用方法。',
          date: '2024-01-15',
          category: '前端开发',
          tags: ['Vue3', 'JavaScript', 'Composition API'],
          image: '/image/DBBE2DD468E49905901871EC20BDCA84.jpg'
        },
        {
          id: 2,
          title: 'CSS Grid 布局完全指南',
          excerpt: 'CSS Grid是现代网页布局的强大工具，本文将带你从基础到高级全面掌握Grid布局技术。',
          date: '2024-01-10',
          category: '前端开发',
          tags: ['CSS', 'Grid', '布局'],
          image: '/image/DBBE2DD468E49905901871EC20BDCA84.jpg'
        },
        {
          id: 3,
          title: 'JavaScript 异步编程最佳实践',
          excerpt: '探讨JavaScript中的异步编程模式，包括Promise、async/await的使用技巧和最佳实践。',
          date: '2024-01-05',
          category: '前端开发',
          tags: ['JavaScript', '异步编程', 'Promise'],
          image: '/image/DBBE2DD468E49905901871EC20BDCA84.jpg'
        },
        {
          id: 4,
          title: 'Node.js 服务端开发入门',
          excerpt: '学习Node.js后端开发，从环境搭建到创建RESTful API，构建完整的服务端应用。',
          date: '2023-12-28',
          category: '后端开发',
          tags: ['Node.js', 'Express', 'API'],
          image: '/image/IMG_20241224_180750.jpg'
        },
        {
          id: 5,
          title: 'Git 版本控制最佳实践',
          excerpt: '掌握Git的核心概念和工作流程，学习如何在团队开发中高效使用Git进行版本控制。',
          date: '2023-12-20',
          category: '开发工具',
          tags: ['Git', '版本控制', '团队协作'],
          image: '/image/IMG_20241224_180750.jpg'
        },
        {
          id: 6,
          title: 'React Hooks 深度解析',
          excerpt: '深入理解React Hooks的原理和使用方法，学习如何使用Hooks构建现代React应用。',
          date: '2023-12-15',
          category: '前端开发',
          tags: ['React', 'Hooks', 'JavaScript'],
          image: '/image/Screenshot_2024-11-26-23-55-33-852_com.ss.android.ugc.aweme.jpg'
        }
      ]
    }
  },
  computed: {
    categories() {
      return [...new Set(this.posts.map(post => post.category))]
    },
    filteredPosts() {
      let filtered = this.posts

      // 搜索过滤
      if (this.searchQuery) {
        filtered = filtered.filter(post => 
          post.title.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
          post.excerpt.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
          post.tags.some(tag => tag.toLowerCase().includes(this.searchQuery.toLowerCase()))
        )
      }

      // 分类过滤
      if (this.selectedCategory) {
        filtered = filtered.filter(post => post.category === this.selectedCategory)
      }

      // 分页
      const start = (this.currentPage - 1) * this.postsPerPage
      const end = start + this.postsPerPage
      return filtered.slice(start, end)
    },
    totalPages() {
      let filtered = this.posts

      if (this.searchQuery) {
        filtered = filtered.filter(post => 
          post.title.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
          post.excerpt.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
          post.tags.some(tag => tag.toLowerCase().includes(this.searchQuery.toLowerCase()))
        )
      }

      if (this.selectedCategory) {
        filtered = filtered.filter(post => post.category === this.selectedCategory)
      }

      return Math.ceil(filtered.length / this.postsPerPage)
    }
  },
  watch: {
    searchQuery() {
      this.currentPage = 1
    },
    selectedCategory() {
      this.currentPage = 1
    }
  }
}
</script>

<style scoped>
.blog {
  padding: 80px 0;
  min-height: calc(100vh - 200px);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.blog-header {
  text-align: center;
  margin-bottom: 50px;
}

.blog-header h1 {
  font-size: 3rem;
  color: #333;
  margin-bottom: 10px;
}

.blog-header p {
  font-size: 1.2rem;
  color: #666;
}

.blog-filters {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 40px;
  gap: 20px;
}

.search-box {
  flex: 1;
  max-width: 400px;
}

.search-input {
  width: 100%;
  padding: 12px 16px;
  border: 2px solid #e9ecef;
  border-radius: 25px;
  font-size: 1rem;
  outline: none;
  transition: border-color 0.3s;
}

.search-input:focus {
  border-color: #007bff;
}

.category-select {
  padding: 12px 16px;
  border: 2px solid #e9ecef;
  border-radius: 8px;
  font-size: 1rem;
  outline: none;
  background: white;
  cursor: pointer;
  transition: border-color 0.3s;
}

.category-select:focus {
  border-color: #007bff;
}

.posts-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 30px;
  margin-bottom: 50px;
}

.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
}

.page-btn {
  padding: 10px 20px;
  border: 2px solid #007bff;
  background: #007bff;
  color: white;
  border-radius: 5px;
  cursor: pointer;
  transition: all 0.3s;
}

.page-btn:hover:not(:disabled) {
  background: #0056b3;
  border-color: #0056b3;
}

.page-btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.page-info {
  font-weight: 500;
  color: #666;
}

@media (max-width: 768px) {
  .blog-filters {
    flex-direction: column;
    align-items: stretch;
  }
  
  .posts-grid {
    grid-template-columns: 1fr;
  }
  
  .pagination {
    flex-direction: column;
    gap: 10px;
  }
}
</style>
