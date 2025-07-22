<template>
  <footer class="footer">
    <div class="footer-content">
      <div class="footer-section">
        <h3>我的博客</h3>
        <p>分享技术心得，记录生活点滴</p>
      </div>
      <div class="footer-section">
        <h3>快速链接</h3>
        <ul>
          <li><router-link to="/">首页</router-link></li>
          <li><router-link to="/blog">博客</router-link></li>
          <li><router-link to="/about">关于我</router-link></li>
          <li><router-link to="/contact">联系方式</router-link></li>
        </ul>
      </div>
      <div class="footer-section">
        <h3>联系方式</h3>
        <p>邮箱: 2911793994@qq.com</p>
        <div class="social-links">
          <a href="#" target="_blank">GitHub</a>
          <a href="#" target="_blank">微博</a>
          <a href="#" target="_blank">知乎</a>
        </div>
      </div>
    </div>
    <div class="footer-bottom">
      <p>&copy; {{ currentYear }} 我的博客. 版权所有.</p>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'Footer',
  computed: {
    currentYear() {
      return new Date().getFullYear()
    }
  }
}
</script>

<style scoped>
.footer {
  background-color: #333;
  color: #fff;
  padding: 40px 0 20px;
}

.footer-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 30px;
}

.footer-section h3 {
  margin-bottom: 15px;
  color: #007bff;
}

.footer-section ul {
  list-style: none;
  padding: 0;
}

.footer-section ul li {
  margin-bottom: 8px;
}

.footer-section a {
  color: #ccc;
  text-decoration: none;
  transition: color 0.3s;
}

.footer-section a:hover {
  color: #007bff;
}

.social-links {
  margin-top: 15px;
}

.social-links a {
  margin-right: 15px;
  color: #ccc;
  text-decoration: none;
  transition: color 0.3s;
}

.social-links a:hover {
  color: #007bff;
}

.footer-bottom {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  text-align: center;
  border-top: 1px solid #555;
  margin-top: 30px;
}

.footer-bottom p {
  margin: 0;
  color: #ccc;
}
</style>
