<template>
  <div class="blog-card">
    <div class="blog-image" v-if="post.image">
      <img :src="post.image" :alt="post.title" />
    </div>
    <div class="blog-content">
      <div class="blog-meta">
        <span class="blog-date">{{ formatDate(post.date) }}</span>
        <span class="blog-category">{{ post.category }}</span>
      </div>
      <h3 class="blog-title">{{ post.title }}</h3>
      <p class="blog-excerpt">{{ post.excerpt }}</p>
      <div class="blog-tags">
        <span v-for="tag in post.tags" :key="tag" class="tag">{{ tag }}</span>
      </div>
      <router-link :to="`/blog/${post.id}`" class="read-more">阅读更多</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BlogCard',
  props: {
    post: {
      type: Object,
      required: true
    }
  },
  methods: {
    formatDate(date) {
      return new Date(date).toLocaleDateString('zh-CN', {
        year: 'numeric',
        month: 'long',
        day: 'numeric'
      })
    }
  }
}
</script>

<style scoped>
.blog-card {
  background: #fff;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  transition: transform 0.3s, box-shadow 0.3s;
  margin-bottom: 30px;
}

.blog-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
}

.blog-image {
  height: 200px;
  overflow: hidden;
}

.blog-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s;
}

.blog-card:hover .blog-image img {
  transform: scale(1.05);
}

.blog-content {
  padding: 20px;
}

.blog-meta {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
  font-size: 0.9rem;
  color: #666;
}

.blog-category {
  background: #007bff;
  color: #fff;
  padding: 2px 8px;
  border-radius: 12px;
  font-size: 0.8rem;
}

.blog-title {
  margin: 0 0 10px 0;
  font-size: 1.3rem;
  color: #333;
  line-height: 1.4;
}

.blog-excerpt {
  color: #666;
  line-height: 1.6;
  margin-bottom: 15px;
}

.blog-tags {
  margin-bottom: 15px;
}

.tag {
  display: inline-block;
  background: #f8f9fa;
  color: #6c757d;
  padding: 2px 8px;
  border-radius: 4px;
  font-size: 0.8rem;
  margin-right: 8px;
  margin-bottom: 5px;
}

.read-more {
  color: #007bff;
  text-decoration: none;
  font-weight: 500;
  transition: color 0.3s;
}

.read-more:hover {
  color: #0056b3;
}
</style>
