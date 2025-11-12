<script setup>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faHouse, faRadio, faFlask } from '@fortawesome/free-solid-svg-icons'

</script>


<template>
  <div class="header">
    <div class="header-left">
      <h1>ROLAND</h1>
    </div>
    <div class="nav-block">
      <router-link to="/" class="nav-box">
        <FontAwesomeIcon :icon="faHouse" />
        Home
      </router-link>
      <router-link to="/publication" class="nav-box">
        <FontAwesomeIcon :icon="faRadio" />
        Publication
      </router-link>
      <router-link to="/project" class="nav-box disabled">
        <FontAwesomeIcon :icon="faFlask" />
        Project
      </router-link>
    </div>
  </div>
</template>

<style scoped>
.header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 8vh;
  min-height: 60px;
  background: linear-gradient(135deg, rgb(0, 93, 233), rgb(58, 154, 236));
  color: white;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 2rem;
  z-index: 100;
  box-sizing: border-box;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

.header:hover {
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.15);
}

.header-left h1 {
  font-size: 1.5rem;
  margin: 0;
  font-weight: 600;
  letter-spacing: 0.5px;
  transition: transform 0.3s ease;
}

.header-left h1:hover {
  transform: scale(1.05);
}

.nav-block {
  display: flex;
  gap: 1.5rem;
  align-items: center;
}

/* Responsive Design */
@media (max-width: 1023px) {
  .header {
    padding: 0 1.5rem;
  }
  
  .nav-block {
    gap: 1rem;
  }
}

@media (max-width: 768px) {
  .header {
    padding: 0 1rem;
    height: 7vh;
    min-height: 50px;
  }

  .header-left h1 {
    font-size: 1.3rem;
  }

  .nav-block {
    gap: 0.6rem;
  }

  .nav-box {
    padding: 0.4rem 0.6rem;
    font-size: 0.85rem;
  }
}

@media (max-width: 480px) {
  .header {
    padding: 0 0.75rem;
    height: 6vh;
    min-height: 45px;
  }

  .header-left h1 {
    font-size: 1.1rem;
  }

  .nav-block {
    gap: 0.4rem;
  }

  .nav-box {
    padding: 0.3rem 0.5rem;
    font-size: 0.8rem;
  }

  .nav-box svg {
    font-size: 0.9rem;
  }
}

@media (max-width: 360px) {
  .header {
    padding: 0 0.5rem;
  }

  .header-left h1 {
    font-size: 1rem;
  }

  .nav-block {
    gap: 0.3rem;
  }

  .nav-box {
    padding: 0.25rem 0.4rem;
    font-size: 0.75rem;
  }

  .nav-box svg {
    font-size: 0.8rem;
  }
}
</style>