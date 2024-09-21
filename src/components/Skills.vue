<template>
  <section id="skills" class="section">
    <h2 class="section-title">Skills</h2>
    <div class="skills-grid">
      <div v-for="(skill, index) in skills" :key="index" class="skill-item" :style="{ animationDelay: `${index * 0.1}s` }">
        <h3>{{ skill.category }}</h3>
        <div class="skill-bar">
          <div class="skill-progress" :style="{ width: `${skill.level}%` }"></div>
        </div>
        <p>{{ skill.technologies.join(', ') }}</p>
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
        { category: 'Front-end', level: 90, technologies: ['HTML5', 'CSS3', 'JavaScript', 'Vue.js', 'React'] },
        { category: 'Back-end', level: 85, technologies: ['Node.js', 'Express.js', 'Python', 'Django'] },
        { category: 'Database', level: 80, technologies: ['MongoDB', 'MySQL', 'PostgreSQL'] },
        { category: 'DevOps', level: 75, technologies: ['Git', 'Docker', 'AWS', 'CI/CD'] },
      ]
    }
  }
}
</script>

<style scoped>
.section-title {
  text-align: center;
  margin-bottom: 2rem;
  font-size: 2.5rem;
  color: #42b983;
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 30px;
}

.skill-item {
  background: rgba(255, 255, 255, 0.1);
  padding: 20px;
  border-radius: 15px;
  transition: transform 0.5s ease, box-shadow 0.5s ease;
  animation: fadeInUp 0.5s ease forwards;
  opacity: 0;
  transform-style: preserve-3d;
}

.skill-item:hover {
  transform: translateY(-10px) rotateX(5deg) rotateY(5deg);
  box-shadow: 0 20px 30px rgba(66, 185, 131, 0.3);
}

.skill-item h3 {
  font-size: 1.3rem;
  margin-bottom: 15px;
  color: #42b983;
  transform: translateZ(20px);
}

.skill-bar {
  background: rgba(255, 255, 255, 0.2);
  height: 10px;
  border-radius: 5px;
  overflow: hidden;
  margin-bottom: 15px;
  transform: translateZ(10px);
}

.skill-progress {
  background: linear-gradient(90deg, #42b983, #3aa876);
  height: 100%;
  transition: width 1s ease-in-out;
  box-shadow: 0 0 10px rgba(66, 185, 131, 0.5);
}

.skill-item p {
  font-size: 0.9rem;
  color: #e0e0e0;
  transform: translateZ(15px);
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(50px) rotateX(-10deg);
  }
  to {
    opacity: 1;
    transform: translateY(0) rotateX(0);
  }
}

/* Media queries remain the same */
</style>