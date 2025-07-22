<template>
  <div class="interest-detail">
    <div class="container">
      <!-- 返回按钮 -->
      <div class="back-button" @click="goBack">
        ← 返回关于我
      </div>

      <!-- 头部区域 -->
      <div class="detail-header">
        <div class="interest-icon">{{ currentInterest.icon }}</div>
        <h1>{{ currentInterest.title }}</h1>
        <p class="interest-subtitle">{{ currentInterest.subtitle }}</p>
      </div>

      <!-- 内容区域 -->
      <div class="detail-content">
        <!-- 文章内容 -->
        <section class="articles-section" v-if="currentInterest.articles">
          <h2>相关文章</h2>
          <div class="articles-grid">
            <article 
              class="article-card" 
              v-for="article in currentInterest.articles" 
              :key="article.id"
            >
              <div class="article-date">{{ article.date }}</div>
              <h3>{{ article.title }}</h3>
              <p>{{ article.excerpt }}</p>
              <div class="article-tags">
                <span 
                  class="tag" 
                  v-for="tag in article.tags" 
                  :key="tag"
                >{{ tag }}</span>
              </div>
            </article>
          </div>
        </section>

        <!-- 照片画廊 -->
        <section class="gallery-section" v-if="currentInterest.photos">
          <h2>照片分享</h2>
          <div class="photo-grid">
            <div 
              class="photo-item" 
              v-for="photo in currentInterest.photos" 
              :key="photo.id"
              @click="openPhotoModal(photo)"
            >
              <img :src="photo.thumbnail" :alt="photo.title" />
              <div class="photo-overlay">
                <h4>{{ photo.title }}</h4>
                <p>{{ photo.location }}</p>
              </div>
            </div>
          </div>
        </section>

        <!-- 推荐资源 -->
        <section class="resources-section" v-if="currentInterest.resources">
          <h2>推荐资源</h2>
          <div class="resources-list">
            <div 
              class="resource-item" 
              v-for="resource in currentInterest.resources" 
              :key="resource.id"
            >
              <div class="resource-icon">{{ resource.icon }}</div>
              <div class="resource-content">
                <h4>{{ resource.title }}</h4>
                <p>{{ resource.description }}</p>
                <a :href="resource.link" target="_blank" class="resource-link">
                  查看详情 →
                </a>
              </div>
            </div>
          </div>
        </section>
      </div>
    </div>

    <!-- 照片模态框 -->
    <div class="photo-modal" v-if="selectedPhoto" @click="closePhotoModal">
      <div class="modal-content" @click.stop>
        <button class="close-button" @click="closePhotoModal">×</button>
        <img :src="selectedPhoto.fullSize" :alt="selectedPhoto.title" />
        <div class="photo-info">
          <h3>{{ selectedPhoto.title }}</h3>
          <p>📍 {{ selectedPhoto.location }}</p>
          <p>📅 {{ selectedPhoto.date }}</p>
          <p>{{ selectedPhoto.description }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'InterestDetail',
  data() {
    return {
      selectedPhoto: null,
      interestData: {
        reading: {
          icon: '📚',
          title: '阅读世界',
          subtitle: '在知识的海洋中遨游',
          articles: [
            {
              id: 1,
              title: '我的2024年度书单推荐',
              excerpt: '分享今年读过的优秀技术书籍和文学作品，包括《代码大全》、《人类简史》等...',
              date: '2024-12-01',
              tags: ['书单推荐', '技术书籍', '文学']
            },
            {
              id: 2,
              title: '如何培养高效的阅读习惯',
              excerpt: '从碎片化阅读到深度阅读，分享我的阅读方法和心得体会...',
              date: '2024-11-15',
              tags: ['阅读方法', '学习技巧', '个人成长']
            },
            {
              id: 3,
              title: '前端开发者必读的技术书籍',
              excerpt: '整理了前端开发者在不同阶段应该阅读的经典技术书籍...',
              date: '2024-10-20',
              tags: ['前端开发', '技术书籍', '学习路线']
            }
          ],
          resources: [
            {
              id: 1,
              icon: '📖',
              title: '我的豆瓣书单',
              description: '在豆瓣记录的读书笔记和评分',
              link: 'https://douban.com'
            },
            {
              id: 2,
              icon: '📝',
              title: '读书笔记分享',
              description: '整理的读书笔记和思维导图',
              link: '#'
            }
          ]
        },
        photography: {
          icon: '📷',
          title: '光影记录',
          subtitle: '用镜头捕捉生活的美好瞬间',
          articles: [
            {
              id: 1,
              title: '街头摄影的艺术',
              excerpt: '分享在城市街头拍摄的技巧和心得，如何捕捉生活中的精彩瞬间...',
              date: '2024-11-28',
              tags: ['街头摄影', '摄影技巧', '生活记录']
            },
            {
              id: 2,
              title: '夜景摄影入门指南',
              excerpt: '从器材选择到拍摄技巧，详细介绍夜景摄影的方方面面...',
              date: '2024-10-12',
              tags: ['夜景摄影', '摄影教程', '器材推荐']
            }
          ],
          photos: [
            {
              id: 1,
              title: '城市夜景',
              location: '上海外滩',
              date: '2024-11-20',
              description: '华灯初上的上海外滩，璀璨的灯光倒映在黄浦江中',
              thumbnail: '../assets/2D5101503CB6CB30B2FD2643F3FA8368.jpg',
              fullSize: '../assets/2D5101503CB6CB30B2FD2643F3FA8368.jpg'
            },
            {
              id: 2,
              title: '街头人文',
              location: '北京胡同',
              date: '2024-10-15',
              description: '老北京胡同里的生活气息，传统与现代的交融',
              thumbnail: '../assets/logo.png',
              fullSize: '../assets/logo.png'
            },
            {
              id: 3,
              title: '自然风光',
              location: '杭州西湖',
              date: '2024-09-08',
              description: '秋日西湖，层林尽染，如诗如画的江南美景',
              thumbnail: '../assets/25685BA5B1324BFE89628223741426F4.gif',
              fullSize: '../assets/25685BA5B1324BFE89628223741426F4.gif'
            }
          ],
          resources: [
            {
              id: 1,
              icon: '📸',
              title: '我的摄影作品集',
              description: '精选摄影作品展示',
              link: '#'
            },
            {
              id: 2,
              icon: '🎥',
              title: '摄影教程视频',
              description: '分享摄影技巧的视频教程',
              link: '#'
            }
          ]
        },
        travel: {
          icon: '✈️',
          title: '行走天下',
          subtitle: '在路上发现不一样的世界',
          articles: [
            {
              id: 1,
              title: '我的西藏自驾游记',
              excerpt: '14天的西藏自驾之旅，从成都到拉萨，感受高原的神秘与壮美...',
              date: '2024-09-30',
              tags: ['西藏', '自驾游', '旅行攻略']
            },
            {
              id: 2,
              title: '日本关西深度游攻略',
              excerpt: '京都、大阪、奈良的深度游玩攻略，包含美食、景点、交通指南...',
              date: '2024-08-15',
              tags: ['日本', '关西', '深度游']
            },
            {
              id: 3,
              title: '独自旅行的勇气',
              excerpt: '分享独自旅行的经历和感悟，如何在路上找到真正的自己...',
              date: '2024-07-20',
              tags: ['独自旅行', '心灵感悟', '成长']
            }
          ],
          photos: [
            {
              id: 1,
              title: '布达拉宫',
              location: '拉萨',
              date: '2024-09-15',
              description: '雄伟的布达拉宫在蓝天白云下显得格外神圣',
              thumbnail: '../assets/2D5101503CB6CB30B2FD2643F3FA8368.jpg',
              fullSize: '../assets/2D5101503CB6CB30B2FD2643F3FA8368.jpg'
            },
            {
              id: 2,
              title: '京都金阁寺',
              location: '京都',
              date: '2024-08-08',
              description: '金光闪闪的金阁寺倒映在池水中，美轮美奂',
              thumbnail: '../assets/logo.png',
              fullSize: '../assets/logo.png'
            }
          ],
          resources: [
            {
              id: 1,
              icon: '🗺️',
              title: '旅行路线规划',
              description: '我使用的旅行规划工具和方法',
              link: '#'
            },
            {
              id: 2,
              icon: '🎒',
              title: '旅行装备清单',
              description: '分享实用的旅行装备推荐',
              link: '#'
            }
          ]
        },
        music: {
          icon: '🎵',
          title: '音乐空间',
          subtitle: '在旋律中寻找编程的灵感',
          articles: [
            {
              id: 1,
              title: '编程时的音乐选择',
              excerpt: '分享适合编程时听的音乐类型，如何用音乐提高专注力和创造力...',
              date: '2024-11-10',
              tags: ['编程', '音乐', '专注力']
            },
            {
              id: 2,
              title: '我的年度音乐总结',
              excerpt: '回顾今年听过的优秀音乐作品，分享音乐带给我的感动...',
              date: '2024-12-05',
              tags: ['音乐推荐', '年度总结', '音乐感悟']
            }
          ],
          resources: [
            {
              id: 1,
              icon: '🎧',
              title: '我的音乐播放列表',
              description: '分享我的Spotify和网易云音乐歌单',
              link: '#'
            },
            {
              id: 2,
              icon: '🎼',
              title: '音乐与编程的结合',
              description: '探讨音乐对编程效率的影响',
              link: '#'
            }
          ]
        }
      }
    }
  },
  computed: {
    currentInterest() {
      const interestType = this.$route.params.type;
      return this.interestData[interestType] || {};
    }
  },
  methods: {
    goBack() {
      this.$router.push('/about');
    },
    openPhotoModal(photo) {
      this.selectedPhoto = photo;
    },
    closePhotoModal() {
      this.selectedPhoto = null;
    }
  }
}
</script>

<style scoped>
.interest-detail {
  padding: 80px 0;
  min-height: 100vh;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.back-button {
  display: inline-flex;
  align-items: center;
  color: #007bff;
  cursor: pointer;
  font-weight: 500;
  margin-bottom: 40px;
  padding: 10px 0;
  transition: color 0.3s;
}

.back-button:hover {
  color: #0056b3;
}

.detail-header {
  text-align: center;
  margin-bottom: 60px;
}

.detail-header .interest-icon {
  font-size: 4rem;
  margin-bottom: 20px;
}

.detail-header h1 {
  font-size: 3rem;
  color: #333;
  margin-bottom: 10px;
}

.interest-subtitle {
  font-size: 1.2rem;
  color: #666;
  margin-bottom: 0;
}

.detail-content section {
  margin-bottom: 60px;
}

.detail-content h2 {
  font-size: 2rem;
  color: #333;
  margin-bottom: 30px;
  padding-bottom: 10px;
  border-bottom: 2px solid #007bff;
}

/* 文章样式 */
.articles-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 30px;
}

.article-card {
  background: white;
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s;
}

.article-card:hover {
  transform: translateY(-5px);
}

.article-date {
  color: #007bff;
  font-size: 0.9rem;
  margin-bottom: 10px;
  font-weight: 500;
}

.article-card h3 {
  color: #333;
  margin-bottom: 15px;
  font-size: 1.3rem;
}

.article-card p {
  color: #666;
  line-height: 1.6;
  margin-bottom: 20px;
}

.article-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.tag {
  background: #f8f9fa;
  color: #007bff;
  padding: 4px 12px;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 500;
}

/* 照片画廊样式 */
.photo-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
}

.photo-item {
  position: relative;
  border-radius: 12px;
  overflow: hidden;
  cursor: pointer;
  transition: transform 0.3s;
}

.photo-item:hover {
  transform: scale(1.05);
}

.photo-item img {
  width: 100%;
  height: 250px;
  object-fit: cover;
}

.photo-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(transparent, rgba(0, 0, 0, 0.8));
  color: white;
  padding: 20px;
  transform: translateY(100%);
  transition: transform 0.3s;
}

.photo-item:hover .photo-overlay {
  transform: translateY(0);
}

.photo-overlay h4 {
  margin-bottom: 5px;
  font-size: 1.1rem;
}

.photo-overlay p {
  margin: 0;
  font-size: 0.9rem;
  opacity: 0.9;
}

/* 资源列表样式 */
.resources-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  gap: 20px;
}

.resource-item {
  display: flex;
  align-items: center;
  background: white;
  padding: 25px;
  border-radius: 12px;
  box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s;
}

.resource-item:hover {
  transform: translateY(-3px);
}

.resource-icon {
  font-size: 2.5rem;
  margin-right: 20px;
}

.resource-content h4 {
  color: #333;
  margin-bottom: 8px;
  font-size: 1.2rem;
}

.resource-content p {
  color: #666;
  margin-bottom: 10px;
  line-height: 1.5;
}

.resource-link {
  color: #007bff;
  text-decoration: none;
  font-weight: 500;
  font-size: 0.9rem;
}

.resource-link:hover {
  text-decoration: underline;
}

/* 照片模态框样式 */
.photo-modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.9);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.modal-content {
  position: relative;
  max-width: 90%;
  max-height: 90%;
  background: white;
  border-radius: 12px;
  overflow: hidden;
}

.close-button {
  position: absolute;
  top: 15px;
  right: 15px;
  background: rgba(0, 0, 0, 0.5);
  color: white;
  border: none;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  font-size: 24px;
  cursor: pointer;
  z-index: 1001;
}

.modal-content img {
  width: 100%;
  height: auto;
  max-height: 70vh;
  object-fit: contain;
}

.photo-info {
  padding: 25px;
}

.photo-info h3 {
  color: #333;
  margin-bottom: 15px;
  font-size: 1.5rem;
}

.photo-info p {
  color: #666;
  margin-bottom: 8px;
  line-height: 1.5;
}

@media (max-width: 768px) {
  .detail-header h1 {
    font-size: 2.2rem;
  }
  
  .articles-grid,
  .photo-grid {
    grid-template-columns: 1fr;
  }
  
  .resources-list {
    grid-template-columns: 1fr;
  }
  
  .resource-item {
    flex-direction: column;
    text-align: center;
  }
  
  .resource-icon {
    margin-right: 0;
    margin-bottom: 15px;
  }
  
  .modal-content {
    max-width: 95%;
    max-height: 95%;
  }
}
</style>
