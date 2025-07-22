<template>
  <div class="contact">
    <div class="container">
      <div class="contact-header">
        <h1>联系我</h1>
        <p>有任何问题或合作机会，欢迎随时联系</p>
      </div>

      <div class="contact-content">
        <!-- 联系信息 -->
        <div class="contact-info">
          <h2>联系方式</h2>
          <div class="info-list">
            <div class="info-item">
              <div class="info-icon">📧</div>
              <div class="info-details">
                <h3>邮箱</h3>
                <p>your-email@example.com</p>
                <a href="mailto:your-email@example.com" class="contact-link">发送邮件</a>
              </div>
            </div>
            
            <div class="info-item">
              <div class="info-icon">💼</div>
              <div class="info-details">
                <h3>LinkedIn</h3>
                <p>专业社交网络</p>
                <a href="https://linkedin.com" target="_blank" class="contact-link">查看主页</a>
              </div>
            </div>
            
            <div class="info-item">
              <div class="info-icon">🐙</div>
              <div class="info-details">
                <h3>GitHub</h3>
                <p>开源项目和代码仓库</p>
                <a href="https://github.com" target="_blank" class="contact-link">访问GitHub</a>
              </div>
            </div>
            
            <div class="info-item">
              <div class="info-icon">🐦</div>
              <div class="info-details">
                <h3>微博</h3>
                <p>日常动态分享</p>
                <a href="https://weibo.com" target="_blank" class="contact-link">关注微博</a>
              </div>
            </div>
          </div>
        </div>

        <!-- 联系表单 -->
        <div class="contact-form-section">
          <h2>发送消息</h2>
          <form @submit.prevent="submitForm" class="contact-form">
            <div class="form-group">
              <label for="name">姓名 *</label>
              <input 
                type="text" 
                id="name" 
                v-model="form.name" 
                required 
                class="form-input"
                placeholder="请输入您的姓名"
              />
            </div>
            
            <div class="form-group">
              <label for="email">邮箱 *</label>
              <input 
                type="email" 
                id="email" 
                v-model="form.email" 
                required 
                class="form-input"
                placeholder="请输入您的邮箱"
              />
            </div>
            
            <div class="form-group">
              <label for="subject">主题 *</label>
              <input 
                type="text" 
                id="subject" 
                v-model="form.subject" 
                required 
                class="form-input"
                placeholder="请输入消息主题"
              />
            </div>
            
            <div class="form-group">
              <label for="message">消息内容 *</label>
              <textarea 
                id="message" 
                v-model="form.message" 
                required 
                class="form-textarea"
                placeholder="请输入您想说的话..."
                rows="6"
              ></textarea>
            </div>
            
            <button type="submit" class="submit-btn" :disabled="isSubmitting">
              {{ isSubmitting ? '发送中...' : '发送消息' }}
            </button>
          </form>
          
          <!-- 成功提示 -->
          <div v-if="showSuccess" class="success-message">
            <h3>✅ 消息发送成功！</h3>
            <p>感谢您的留言，我会尽快回复您。</p>
          </div>
        </div>
      </div>

      <!-- FAQ 部分 -->
      <div class="faq-section">
        <h2>常见问题</h2>
        <div class="faq-list">
          <div class="faq-item" v-for="(faq, index) in faqs" :key="index">
            <h3 class="faq-question" @click="toggleFaq(index)">
              {{ faq.question }}
              <span class="faq-icon" :class="{ active: faq.isOpen }">▼</span>
            </h3>
            <div class="faq-answer" v-show="faq.isOpen">
              <p>{{ faq.answer }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Contact',
  data() {
    return {
      form: {
        name: '',
        email: '',
        subject: '',
        message: ''
      },
      isSubmitting: false,
      showSuccess: false,
      faqs: [
        {
          question: '您通常多久回复邮件？',
          answer: '我通常会在24-48小时内回复邮件。如果是紧急事务，请在邮件标题中注明。',
          isOpen: false
        },
        {
          question: '可以咨询技术问题吗？',
          answer: '当然可以！我很乐意帮助解决前端开发相关的技术问题，特别是Vue.js、JavaScript等方面的问题。',
          isOpen: false
        },
        {
          question: '是否接受合作项目？',
          answer: '我对有趣的项目很感兴趣，特别是开源项目或有意义的技术挑战。请通过邮件详细描述项目需求。',
          isOpen: false
        },
        {
          question: '可以分享博客文章吗？',
          answer: '欢迎分享我的博客文章！请注明原文链接和作者信息即可。',
          isOpen: false
        }
      ]
    }
  },
  methods: {
    async submitForm() {
      this.isSubmitting = true
      
      // 模拟发送邮件
      try {
        await new Promise(resolve => setTimeout(resolve, 2000))
        
        // 清空表单
        this.form = {
          name: '',
          email: '',
          subject: '',
          message: ''
        }
        
        // 显示成功消息
        this.showSuccess = true
        setTimeout(() => {
          this.showSuccess = false
        }, 5000)
        
      } catch (error) {
        console.error('发送失败:', error)
      } finally {
        this.isSubmitting = false
      }
    },
    
    toggleFaq(index) {
      this.faqs[index].isOpen = !this.faqs[index].isOpen
    }
  }
}
</script>

<style scoped>
.contact {
  padding: 80px 0;
  min-height: calc(100vh - 200px);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.contact-header {
  text-align: center;
  margin-bottom: 60px;
}

.contact-header h1 {
  font-size: 3rem;
  color: #333;
  margin-bottom: 15px;
}

.contact-header p {
  font-size: 1.2rem;
  color: #666;
}

.contact-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 60px;
  margin-bottom: 80px;
}

/* 联系信息 */
.contact-info h2 {
  font-size: 2rem;
  color: #333;
  margin-bottom: 30px;
}

.info-list {
  display: flex;
  flex-direction: column;
  gap: 25px;
}

.info-item {
  display: flex;
  align-items: flex-start;
  gap: 20px;
  padding: 20px;
  background: white;
  border-radius: 10px;
  box-shadow: 0 3px 15px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s;
}

.info-item:hover {
  transform: translateY(-3px);
}

.info-icon {
  font-size: 2rem;
  flex-shrink: 0;
}

.info-details h3 {
  font-size: 1.2rem;
  color: #333;
  margin-bottom: 5px;
}

.info-details p {
  color: #666;
  margin-bottom: 10px;
}

.contact-link {
  color: #007bff;
  text-decoration: none;
  font-weight: 500;
  transition: color 0.3s;
}

.contact-link:hover {
  color: #0056b3;
}

/* 联系表单 */
.contact-form-section h2 {
  font-size: 2rem;
  color: #333;
  margin-bottom: 30px;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.form-group {
  display: flex;
  flex-direction: column;
}

.form-group label {
  font-weight: 600;
  color: #333;
  margin-bottom: 8px;
}

.form-input,
.form-textarea {
  padding: 12px 16px;
  border: 2px solid #e9ecef;
  border-radius: 8px;
  font-size: 1rem;
  font-family: inherit;
  outline: none;
  transition: border-color 0.3s;
}

.form-input:focus,
.form-textarea:focus {
  border-color: #007bff;
}

.form-textarea {
  resize: vertical;
  min-height: 120px;
}

.submit-btn {
  padding: 15px 30px;
  background: #007bff;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 1.1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s;
}

.submit-btn:hover:not(:disabled) {
  background: #0056b3;
  transform: translateY(-2px);
}

.submit-btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.success-message {
  margin-top: 20px;
  padding: 20px;
  background: #d4edda;
  border: 1px solid #c3e6cb;
  border-radius: 8px;
  color: #155724;
}

.success-message h3 {
  margin-bottom: 10px;
}

/* FAQ 部分 */
.faq-section {
  margin-top: 80px;
}

.faq-section h2 {
  font-size: 2.5rem;
  text-align: center;
  color: #333;
  margin-bottom: 40px;
}

.faq-list {
  max-width: 800px;
  margin: 0 auto;
}

.faq-item {
  background: white;
  border-radius: 10px;
  box-shadow: 0 3px 15px rgba(0, 0, 0, 0.1);
  margin-bottom: 15px;
  overflow: hidden;
}

.faq-question {
  padding: 20px;
  margin: 0;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: #333;
  transition: background 0.3s;
}

.faq-question:hover {
  background: #f8f9fa;
}

.faq-icon {
  transition: transform 0.3s;
}

.faq-icon.active {
  transform: rotate(180deg);
}

.faq-answer {
  padding: 0 20px 20px;
  color: #666;
  line-height: 1.6;
}

@media (max-width: 768px) {
  .contact-content {
    grid-template-columns: 1fr;
    gap: 40px;
  }
  
  .contact-header h1 {
    font-size: 2.5rem;
  }
  
  .info-item {
    flex-direction: column;
    text-align: center;
  }
}
</style>
