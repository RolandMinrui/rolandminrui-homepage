<template>
  <div class="cv-container">
    <iframe
      :src="cvUrl"
      width="100%"
      height="100%"
      frameborder="0"
    ></iframe>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const cvUrl = ref('/src/assets/profile/CV.pdf')
</script>

<style scoped>
.cv-container {
  width: 100%;
  height: 92vh;
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #f8f9fa;
}

/* Responsive design for CV view */
@media (max-width: 1023px) {
  .cv-container {
    height: 93vh;
  }
}

@media (max-width: 768px) {
  .cv-container {
    height: 94vh;
    padding: 1rem;
  }
  
  .cv-container iframe {
    height: calc(100% - 2rem);
  }
}

@media (max-width: 480px) {
  .cv-container {
    height: 94vh;
    padding: 0.75rem;
  }
  
  .cv-container iframe {
    height: calc(100% - 1.5rem);
  }
}

@media (max-width: 360px) {
  .cv-container {
    padding: 0.5rem;
  }
  
  .cv-container iframe {
    height: calc(100% - 1rem);
  }
}
</style>