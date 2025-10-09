<script setup>
// Font Awesome Icon
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faCircleQuestion, faSort, faSortUp, faSortDown, faBook, faFileAlt, faSearch } from '@fortawesome/free-solid-svg-icons'
import { faGithub } from '@fortawesome/free-brands-svg-icons'

// Publication Thumbnails
import RD_Agent from '@/assets/publication/RD-Agent.png'
import RD_Agent_Quant from '@/assets/publication/RD-Agent_Quant.png'
import ScaleBiO from '@/assets/publication/ScaleBiO.png'
import Math_for_AI from '@/assets/publication/Math-for-AI.png'
import trustworthy_distillation from '@/assets/publication/trustworthy_distillation.png'
import DiscipLink from '@/assets/publication/DiscipLink.png'

// Add reactive reference and computed property
import { ref, computed } from 'vue'

// Add prop definition
const props = defineProps({
  is_selected: {type: Boolean, default: false}
})

const search_query = ref('')
const sort_date = ref('none') // 'none', 'asc', 'desc'
const filtered_publication = computed(() => {
  let filtered = publication;
  
  // selected publication
  if (props.is_selected) {
    filtered = filtered.filter(pub => pub.selected);
  }

  // search bar
  if (search_query.value) {
    const query = search_query.value.toLowerCase();
    filtered = filtered.filter(pub => 
      pub.title.toLowerCase().includes(query)
    );
  }

  // sort by date
  if (sort_date.value === 'asc') {
    return [...filtered].reverse();
  } else if (sort_date.value === 'desc') {
    return filtered;
  }
  return filtered;
});

const publication = [
{
    title: "R&D-Agent: Automating Data-Driven AI Solution Building Through LLM-Powered Automated Research, Development, and Evolution",
    author: "Xu Yang, Xiao Yang, Shikai Fang, Bowen Xian, Yuante Li, Jian Wang, <u>Minrui Xu</u>, Haoran Pan, Xinpeng Hong, Weiqing Liu, Yelong Shen, Weizhu Chen, Jiang Bian",
    venue: "Arixv",
    img: RD_Agent,
    buttons: [
      {button: "Arxiv", logo: faFileAlt, link: "https://arxiv.org/abs/2505.14738"},
      {button: "GitHub", logo: faGithub, link: "https://github.com/microsoft/RD-Agent"}
    ],
    tags: ['MLEngineering', 'Data Science Agents'],
    selected: false
  },
  {
    title: "R&D-Agent-Quant: A Multi-Agent Framework for Data-Centric Factors and Model Joint Optimization",
    author: "Yuante Li, Xu Yang, Xiao Yang, <u>Minrui Xu</u>, Xisen Wang, Weiqing Liu, Jiang Bian",
    venue: "NeurIPS 2025",
    img: RD_Agent_Quant,
    buttons: [
      {button: "Arxiv", logo: faFileAlt, link: "https://arxiv.org/abs/2505.15155"},
      {button: "GitHub", logo: faGithub, link: "https://github.com/microsoft/RD-Agent"}
    ],
    tags: ['Quantitative Finance Agents'],
    selected: false
  },
  {
    title: "ScaleBiO: Scalable Bilevel Optimization for LLM Data Reweighting",
    author: "Rui Pan, Dylan Zhang, Hanning Zhang, Xingyuan Pan, <u>Minrui Xu</u>, Jipeng Zhang, Renjie Pi, Xiaoyu Wang, Tong Zhang",
    venue: "ACL 2025 Main",
    img: ScaleBiO,
    buttons: [
      {button: "Arxiv", logo: faFileAlt, link: "https://arxiv.org/abs/2406.19976"},
      {button: "GitHub", logo: faGithub, link: "https://github.com/2003pro/ScaleBiO"}
    ],
    tags: ['Bilevel Optimization', 'Data Reweighting'],
    selected: false
  },
  {
    title: "Math for AI: On the Generalization of Learning Mathematical Problem Solving",
    author: "Ruochen Zhou, <u>Minrui Xu</u>, Shiqi Chen, Junteng Liu, Yunqi Li, Xinxin Lin, Zhengyu Chen, Junxian He",
    venue: "NeurIPS 2024 Workshop",
    img: Math_for_AI,
    buttons: [
      {button: "Openreview", logo: faFileAlt, link: "https://openreview.net/forum?id=xlnvZ85CSo"}
    ],
    tags: ['Math for AI'],
    selected: false
  },
  {
    title: "FIRST: Teach A Reliable Large Language Model Through Efficient Trustworthy Distillation",
    author: "KaShun Shum*, <u>Xu Minrui</u>*, Jianshu Zhang*, Zixin Chen, Shizhe Diao, Hanze Dong, Jipeng Zhang, Muhammad Omer Raza",
    venue: "EMNLP 2024 Main",
    img: trustworthy_distillation,
    buttons: [
      {button: "Arxiv", logo: faFileAlt, link: "https://arxiv.org/abs/2408.12168"},
      {button: "GitHub", logo: faGithub, link: "https://github.com/SHUMKASHUN/FIRST"}
    ],
    tags: ['Trustworthy', 'Knowledge Distillation', 'Efficient Post-training'],
    selected: true
  },
  {
    title: "DiscipLink: Unfolding Interdisciplinary Information Seeking Process via Human-AI Co-Exploration",
    author: "Chengbo Zheng, Yuanhao Zhang, Zeyu Huang, Chuhan Shi, Minrui Xu, Xiaojuan Ma",
    venue: "UIST 2024",
    img: DiscipLink,
    buttons: [
      {button: "Arxiv", logo: faFileAlt, link: "https://arxiv.org/abs/2408.00447"}
    ],
    tags: ['Information Retrieval', 'Human-AI Collaboration', 'Interdisciplinary Research'],
    selected: false
  }
];
</script>

<template>
  <main :class="{ 'main-content': !props.is_selected }">
    <!-- Header -->
    <div class="academic-header">
      <h2>
        <FontAwesomeIcon :icon="faBook" style="color: #4fc08d"/> {{ props.is_selected ? 'Selected Publication' : 'Publication' }}
      </h2>
      
      <div class="academic-header-toolbox">
        <!-- Search Bar -->
        <div class="search-bar">
          <FontAwesomeIcon :icon="faSearch" class="search-icon" />
          <input 
            type="text" 
            v-model="search_query" 
            placeholder="Search publications..." 
            class="search-input"
          />
        </div>

        <!-- Control Icons -->
        <div class="control-icons">
          <div class="tooltip">
            <FontAwesomeIcon :icon="faCircleQuestion" class="tooltip-icon control-icon" />
            <span class="tooltip-content">* denotes Equal Contribution</span>
          </div>

          <div class="tooltip">
            <FontAwesomeIcon 
              :icon="sort_date === 'asc' ? faSortUp : sort_date === 'desc' ? faSortDown : faSort" 
              class="tooltip-icon control-icon"
              @click="sort_date = sort_date === 'none' ? 'asc' : sort_date === 'asc' ? 'desc' : 'none'"
            />
            <span class="tooltip-content">Sort by date</span>
          </div>
        </div>
      </div>
    </div>
    
    <!-- Publication -->
    <div v-for="pub in filtered_publication" :key="pub.title" class="academic-block">
      <div>
        <div class="academic-venue">{{ pub.venue }}</div>
        <a :href="pub.arxiv" target="_blank" rel="noopener noreferrer">
          <img :src="pub.img" :alt="pub.title + ' Thumbnail'" class="academic-img">
        </a>
      </div>
      <div class="academic-content">
        <h3>{{ pub.title }}</h3>
        <div class="academic-tags">
          <span v-for="tag in pub.tags" :key="tag" class="academic-tag">{{ tag }}</span>
        </div>
        <p class="program" v-html="pub.author"></p>
        <div class="academic-tags">
          <a v-for="button in pub.buttons" :key="button.button" :href="button.link" target="_blank" rel="noopener noreferrer" class="academic-button">
            <FontAwesomeIcon :icon="button.logo" /> {{ button.button }}
          </a>
        </div>
      </div>
    </div>
  </main>
</template>