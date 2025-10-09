<script setup>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faRankingStar, faFilePdf, faEnvelope, faEnvelopeOpen, faBars, faBarsStaggered } from '@fortawesome/free-solid-svg-icons'
import { faGoogleScholar, faGithub, faLinkedin, faInstagram, faXTwitter } from '@fortawesome/free-brands-svg-icons'
import { useRouter } from 'vue-router'
import { ref } from 'vue'

const router = useRouter()
const isClicked = ref(false)
const isHovered = ref(false)

const SocialMedia = [
  { name: 'Google Scholar', icon: faGoogleScholar, color: '#4A90E2', url: 'https://scholar.google.com/citations?user=2QyPdfgAAAAJ&hl=en' },
  { name: 'GitHub', icon: faGithub, color: '#333', url: 'https://github.com/RolandMinrui' },
  { name: 'LinkedIn', icon: faLinkedin, color: '#0077B5', url: 'https://www.linkedin.com/in/minrui-xu-531b30242/' },
  { name: 'CV', icon: faFilePdf, color: '#2E7D32', url: '#', isRouter: true },
  // { name: 'X', icon: faXTwitter, color: '#000000' },
  { name: 'Instagram', icon: faInstagram, 
    color: 'linear-gradient(45deg, #405DE6, #5851DB, #833AB4, #C13584, #E1306C, #FD1D1D, #F56040, #F77737, #FCAF45, #FFDC80)' },
];

const News = [
  {
    date: '2025.10',
    content: 'One paper accepted to NeurIPS 2025!🎉',
  },
  {
    date: '2025.05',
    content: 'One paper accepted to ACL 2025!🎉',
  },
  {
    date: '2024.10',
    content: 'One paper accepted to MATH-AI Workshop at NeurIPS 2024!🎉',
  },
  {
    date: '2024.09',
    content: 'One paper accepted to EMNLP 2024!🎉',
  },
  {
    date: '2024.07',
    content: 'One paper accepted to UIST 2024!🎉',
  },
];
</script>


<template>
  <div class="sidebar">
    <!-- Profile Card -->
    <div class="sidebar-card">
      <img src="@/assets/profile/profile_life.jpg" alt="Profile Photo">
      <div class="sidebar-block" @click="isClicked = !isClicked">
        <h3 style="margin: 0; font-size: 1.5rem;">Minrui Xu</h3>
        <FontAwesomeIcon :icon="(isClicked) ? faBarsStaggered : faBars" />
      </div>
      <div v-if="isClicked" class="sidebar-block" style="animation: dropdown 0.3s" @mouseenter="isHovered = true" @mouseleave="isHovered = false">
        <FontAwesomeIcon :icon="isHovered ? faEnvelopeOpen : faEnvelope" />
        <p style="margin: 0;">mxubh@connect.ust.hk</p>
      </div>
    </div>

    <!-- Social Media -->
    <div class="sidebar-card social-section">
      <div class="social-links">
        <a 
          v-for="link in SocialMedia" 
          :key="link.name"
          :href="link.isRouter ? undefined : (link.url || '#')" 
          class="tooltip-wrapper" 
          :title="link.name"
          :style="{ background: link.color }"
          :target="link.isRouter ? undefined : '_blank'"
          :rel="link.isRouter ? undefined : 'noopener noreferrer'"
          @click="link.isRouter ? router.push(link.url) : undefined"
        >
          <FontAwesomeIcon :icon="link.icon" />
        </a>
      </div>
    </div>

    <!-- News -->
    <div class="sidebar-card scrollbar">
      <h3>News
        <FontAwesomeIcon :icon="faRankingStar" style="color: #4fc08d"/>
      </h3>
      <div v-for="item in News" :key="item.date" class="sidebar-block">
        <div style="font-size: 1rem; color: #4fc08d; font-weight: 600; margin-bottom: 0.25rem;">{{ item.date }}</div>
        <div style="font-size: 1.1rem; line-height: 1.4;">{{ item.content }}</div>
      </div>
    </div>
  </div>
</template>


<style scoped>
.sidebar {
  width: 35%;
  padding: 1rem;
  background-color: #f8f9fa;
  display: flex;
  flex-direction: column;
  gap: 1rem;
  overflow-y: auto;
  height: 92vh;
}

.sidebar-card {
  background: white;
  border-radius: 12px;
  padding: 0.5rem;
  text-align: center;
  position: relative;
}

.sidebar-card img {
  width: 180px;
  height: 180px;
  border-radius: 50%;
  object-fit: cover;
  border: 3px solid #4fc08d;
  transition: transform 0.3s ease;
}

.sidebar-block {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.75rem;
  margin-bottom: 0.8rem;
  padding: 0.6rem 0.8rem;
  border-bottom: 2px solid #eaeaea;
  border-radius: 6px;
  transition: all 0.2s ease;
  cursor: pointer;
  font-size: 1rem;
  text-align: center;
}

.sidebar-block:hover {
  background: #f8f8f8;
  color: #4fc08d;
  transition: all 0.3s ease;
}

.sidebar-block svg {
  transition: transform 0.3s ease;
}

.sidebar-block:hover svg {
  transform: scale(1.1);
}

.social-section {
  text-align: center;
}

.social-links {
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
  gap: 0.75rem;
}

.tooltip-wrapper {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 36px;
  height: 36px;
  border-radius: 50%;
  color: white;
  font-size: 1.1rem;
  transition: transform 0.2s;
  position: relative;
}

.tooltip-wrapper:hover {
  transform: translateY(-5px);
}

.tooltip-wrapper::after {
  content: attr(title);
  position: absolute;
  bottom: -30px;
  left: 50%;
  transform: translateX(-50%);
  background: rgba(0, 0, 0, 0.8);
  color: white;
  padding: 4px 8px;
  border-radius: 4px;
  font-size: 0.8rem;
  white-space: nowrap;
  z-index: 1000;
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.2s, visibility 0.2s;
}

.tooltip-wrapper::before {
  content: '';
  position: absolute;
  bottom: -6px;
  left: 50%;
  transform: translateX(-50%);
  border-width: 4px;
  border-style: solid;
  border-color: transparent transparent rgba(0, 0, 0, 0.8) transparent;
  z-index: 1000;
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.2s, visibility 0.2s;
}

.tooltip-wrapper:hover::after,
.tooltip-wrapper:hover::before {
  opacity: 1;
  visibility: visible;
}

.tooltip-wrapper svg {
  width: 1em;
  height: 1em;
  vertical-align: middle;
}

/* Responsive Design */
@media (max-width: 600px) {
  .sidebar {
    width: 100%;
    height: auto;
    flex-direction: column;
    padding: 0.5rem;
    gap: 1rem;
  }

  .sidebar-card {
    width: 100%;
    padding: 1rem;
    margin: 0;
  }

  .sidebar-card img {
    width: 150px;
    height: 150px;
  }

  .social-links {
    justify-content: center;
    gap: 1rem;
  }

  .tooltip-wrapper {
    width: 40px;
    height: 40px;
  }
}
</style>