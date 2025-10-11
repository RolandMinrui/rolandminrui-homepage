<script setup>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faGraduationCap, faStar, faUser, faBook, faFileAlt, faCircleQuestion } from '@fortawesome/free-solid-svg-icons'
import { faGithub } from '@fortawesome/free-brands-svg-icons'
import HKUST  from '@/assets/institution/HKUST.png'
import Microsoft  from '@/assets/institution/Microsoft.png'
import Publication from '@/views/publication.vue'

const education = [
  {
    institution: "The Hong Kong University of Science and Technology (Guangzhou)",
    program: "Ph.D in Computer Science",
    time: "Incoming",
    logo: HKUST,
  },
  {
    institution: "The Hong Kong University of Science and Technology",
    program: "BSc in Data Science and Technology; BSc in Mathematics",
    time: "Sep 2021 - present",
    logo: HKUST,
    tags: ["Dean's List"]
  }
];

const experience = [
  {
    institution: "Microsoft Research Aisa (MSRA)",
    program: "Research Intern at Machine Learning Group",
    time: "Jan 2025 - present",
    logo: Microsoft,
    buttons: [
      {button: "RD-Agent", logo: faGithub, link: "https://github.com/microsoft/RD-Agent"}
    ]
  }
];
</script>

<template>
  <main class="main-content">
    <!-- Introduction -->
    <section>
      <div class="academic-header">
        <h2>
          <FontAwesomeIcon :icon="faUser" style="color: #4fc08d"/>
          Introduction
        </h2>
      </div>
      <p style="line-height: 1.5;">
        Welcome to my academic homepage! 👏
        I am Xu Minrui (徐敏瑞), also known as Roland. I am a final year undergraduate student at <a href="https://hkust.edu.hk" target="_blank" rel="noopener noreferrer">The Hong Kong University of Science and Technology (HKUST)</a>, majoring in Data Science and Technology, and additional major in Mathematics.
        I am excited to announce that I will be joining the <a href="https://lark-lab-hkustgz.github.io" target="_blank" rel="noopener noreferrer">LARK Lab@HKUST (GZ)</a> to pursue my Ph.D. in Computer Science under the supervision of Prof. <a href="https://cartus.github.io" target="_blank" rel="noopener noreferrer">Guo Zhijiang</a>.
      </p>
      <p style="line-height: 1.5;">
        Previously, I am a Research Intern at <a href="https://www.microsoft.com/en-us/research/lab/microsoft-research-asia-zh-cn/" target="_blank" rel="noopener noreferrer">Microsoft Research Asia (MSRA)</a> in the Machine Learning Group, working with the project <a href="https://github.com/microsoft/RD-Agent" target="_blank" rel="noopener noreferrer">RD-Agent</a>.
      </p>
    </section>
    
    <!-- Education -->
    <section>
      <div class="academic-header">
        <h2>
          <FontAwesomeIcon :icon="faGraduationCap" style="color: #4fc08d"/> Education
        </h2>
      </div>
      <div v-for="edu in education" :key="edu.program" class="academic-block">
        <img :src="edu.logo" :alt="edu.institution + ' Logo'" class="academic-logo">
        <div class="academic-content">
          <h3>{{ edu.institution }}</h3>
          <p>{{ edu.program }}</p>
          <p class="time">{{ edu.time }}</p>
          <div class="academic-tags" v-if="edu.tags">
            <span v-for="tag in edu.tags" :key="tag" class="academic-tag">{{ tag }}</span>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Experience -->
    <section>
      <div class="academic-header">
        <h2>
          <FontAwesomeIcon :icon="faStar" style="color: #4fc08d"/> Experience
        </h2>
      </div>
      <div v-for="exp in experience" :key="exp.program" class="academic-block">
        <img :src="exp.logo" :alt="exp.institution + ' Logo'" class="academic-logo">
        <div class="academic-content">
          <h3>{{ exp.institution }}</h3>
          <p>{{ exp.program }}</p>
          <p class="time">{{ exp.time }}</p>
          <div class="academic-tags" v-if="exp.buttons">
            <a v-for="button in exp.buttons" :key="button.button" :href="button.link" target="_blank" rel="noopener noreferrer" class="academic-button">
              <FontAwesomeIcon :icon="button.logo" /> {{ button.button }}
            </a>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Selected Publication -->
    <Publication :is_selected="true" />
  </main>
</template>