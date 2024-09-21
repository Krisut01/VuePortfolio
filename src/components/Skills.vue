<template>
  <section id="skills" class="section" ref="skillsSection" @click="animateAllSkills">
    <h2 class="section-title">Skills</h2>
    <div class="skills-grid">
      <div v-for="(skill, index) in skills" :key="index" class="skill-item">
        <div class="skill-content">
          <h3>{{ skill.category }}</h3>
          <div class="skill-bar-container">
            <div class="skill-bar">
              <div class="skill-progress" :style="{ width: `${skill.currentLevel}%`, backgroundColor: skill.color }"></div>
            </div>
            <span class="skill-percentage">{{ Math.round(skill.currentLevel) }}%</span>
          </div>
          <p>{{ skill.technologies.join(', ') }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Skills',
  data() {
    return {
      skills: [
        { category: 'Front-end', level: 90, currentLevel: 0, technologies: ['HTML5', 'CSS3', 'JavaScript', 'Vue.js', 'React'], color: '#42b983' },
        { category: 'Back-end', level: 85, currentLevel: 0, technologies: ['Node.js', 'Express.js', 'Python', 'Django'], color: '#3498db' },
        { category: 'Database', level: 80, currentLevel: 0, technologies: ['MongoDB', 'MySQL', 'PostgreSQL'], color: '#e74c3c' },
        { category: 'DevOps', level: 75, currentLevel: 0, technologies: ['Git', 'Docker', 'AWS', 'CI/CD'], color: '#f39c12' },
        { category: 'Mobile Development', level: 70, currentLevel: 0, technologies: ['React Native', 'Flutter', 'iOS (Swift)', 'Android (Kotlin)'], color: '#9b59b6' },
        { category: 'UI/UX Design', level: 65, currentLevel: 0, technologies: ['Figma', 'Adobe XD', 'Sketch', 'Prototyping'], color: '#1abc9c' },
      ],
      observer: null,
    }
  },
  mounted() {
    this.setupIntersectionObserver();
    this.setupHashChangeListener();
  },
  beforeUnmount() {
    if (this.observer) {
      this.observer.disconnect();
    }
    window.removeEventListener('hashchange', this.checkHash);
  },
  methods: {
    setupIntersectionObserver() {
      this.observer = new IntersectionObserver((entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            this.animateAllSkills();
          }
        });
      }, { threshold: 0.1 });

      this.observer.observe(this.$refs.skillsSection);
    },
    setupHashChangeListener() {
      window.addEventListener('hashchange', this.checkHash);
      this.checkHash(); // Check hash on initial load
    },
    checkHash() {
      if (window.location.hash === '#skills') {
        this.animateAllSkills();
      }
    },
    animateAllSkills() {
      this.skills.forEach(skill => {
        skill.currentLevel = 0;
        this.smoothAnimate(skill);
      });
    },
    smoothAnimate(skill) {
      const duration = 1500; // Animation duration in milliseconds
      const start = performance.now();
      
      const animate = (time) => {
        const elapsed = time - start;
        const progress = Math.min(elapsed / duration, 1);
        skill.currentLevel = progress * skill.level;
        
        if (progress < 1) {
          requestAnimationFrame(animate);
        }
      };
      
      requestAnimationFrame(animate);
    },
  }
}
</script>

<style scoped>
.section-title {
  text-align: center;
  margin-bottom: 3rem;
  font-size: 2.5rem;
  color: #42b983;
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 2rem;
}

.skill-item {
  background: rgba(255, 255, 255, 0.05);
  border-radius: 15px;
  overflow: hidden;
  transition: all 0.3s ease;
  padding: 1.5rem;
  cursor: pointer;
}

.skill-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 20px rgba(66, 185, 131, 0.2);
}

.skill-item h3 {
  font-size: 1.4rem;
  margin-bottom: 1rem;
  color: #42b983;
}

.skill-bar-container {
  background: rgba(255, 255, 255, 0.1);
  height: 10px;
  border-radius: 5px;
  overflow: hidden;
  margin-bottom: 1rem;
  position: relative;
}

.skill-bar {
  height: 100%;
  border-radius: 5px;
  overflow: hidden;
}

.skill-progress {
  height: 100%;
  transition: width 1s ease-out;
}

.skill-percentage {
  position: absolute;
  right: 0;
  top: -20px;
  font-size: 0.9rem;
  color: #ffffff;
}

.skill-item p {
  font-size: 0.9rem;
  color: #e0e0e0;
  margin-top: 0.5rem;
}

@media (max-width: 768px) {
  .skills-grid {
    grid-template-columns: 1fr;
  }
}
</style>