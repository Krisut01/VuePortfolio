<template>
  <v-container id="projects" class="section" fluid>
    <h2 class="section-title">Projects</h2>
    <v-row class="projects-grid">
      <v-col
        v-for="(project, index) in projects"
        :key="index"
        cols="12"
        md="6"
        lg="4"
        class="project-card"
        :style="{ animationDelay: `${index * 0.1}s` }"
      >
        <div class="project-image">
          <img :src="project.image" :alt="project.title" />
        </div>
        <div class="project-content">
          <h3>{{ project.title }}</h3>
          <p>{{ project.description }}</p>
          <div class="project-tech">
            <v-chip
              v-for="tech in project.technologies"
              :key="tech"
              class="tech-tag"
              small
            >
              {{ tech }}
            </v-chip>
          </div>
        </div>
        <v-btn
          :href="project.link"
          class="project-link"
          target="_blank"
          rel="noopener noreferrer"
          block
        >
          View Project
        </v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>


<script>
export default {
  name: 'Projects',
  data() {
    return {
      projects: [
        {
          title: "Social Media Analytics Tool",
          description: "A comprehensive analytics platform for social media managers, offering insights and trend analysis.",
          technologies: ["React", "Python", "D3.js"],
          link: "#",
          image: "/images/Projects/project-1.jpg"
        },
        {
          title: "Fitness Tracking Mobile App",
          description: "A cross-platform mobile application helping users track workouts, nutrition, and set fitness goals.",
          technologies: ["React Native", "Redux", "Firebase"],
          link: "#",
          image: "/images/Projects/project-2.png"
        },
        {
          title: "AI-powered Chatbot",
          description: "An intelligent chatbot designed to assist customers with product inquiries and support.",
          technologies: ["Node.js", "NLP", "Socket.io"],
          link: "#",
          image: "/images/Projects/project-3.jpg"
        }
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
  text-shadow: 0 0 10px rgba(66, 185, 131, 0.5);
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  perspective: 1000px;
}

.project-card {
  background: rgba(255, 255, 255, 0.1);
  border-radius: 15px;
  overflow: hidden;
  transition: transform 0.5s ease, box-shadow 0.5s ease;
  display: flex;
  flex-direction: column;
  animation: fadeInUp 0.5s ease forwards;
  opacity: 0;
  transform-style: preserve-3d;
}

.project-card:hover {
  transform: translateY(-15px) rotateX(5deg) rotateY(5deg);
  box-shadow: 0 20px 40px rgba(66, 185, 131, 0.3);
}

.project-image {
  width: 100%;
  height: 200px;
  overflow: hidden;
}

.project-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.project-card:hover .project-image img {
  transform: scale(1.1);
}

.project-content {
  padding: 1.5rem;
  flex-grow: 1;
  transform: translateZ(30px);
}

.project-card h3 {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  color: #42b983;
  text-shadow: 0 0 5px rgba(66, 185, 131, 0.5);
}

.project-card p {
  font-size: 1rem;
  margin-bottom: 1rem;
  color: #e0e0e0;
}

.project-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.tech-tag {
  background-color: rgba(66, 185, 131, 0.2);
  color: #42b983;
  padding: 0.25rem 0.5rem;
  border-radius: 15px;
  font-size: 0.8rem;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.tech-tag:hover {
  transform: translateZ(10px);
  box-shadow: 0 5px 10px rgba(66, 185, 131, 0.3);
}

.project-link {
  display: inline-block;
  padding: 0.75rem 1.5rem;
  background-color: #42b983;
  color: #fff;
  text-decoration: none;
  border-radius: 5px;
  transition: background-color 0.3s ease, transform 0.3s ease, box-shadow 0.3s ease;
  text-align: center;
  font-weight: bold;
  transform: translateZ(20px);
  margin-top: auto;
  margin-bottom: 1rem;
  align-self: center;
}

.project-link:hover {
  background-color: #3aa876;
  transform: translateY(-2px) translateZ(30px);
  box-shadow: 0 10px 20px rgba(66, 185, 131, 0.4);
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

@media (max-width: 768px) {
  .projects-carousel {
    max-width: 100%;
    height: auto;
  }

  .project-card {
    width: 100%;
    height: auto;
    position: relative;
    transform: none !important;
    animation: none !important;
    opacity: 1 !important;
    box-shadow: none !important;
  }

  .project-image {
    width: 100%;
    height: 200px;
    margin-bottom: 1rem;
  }

  .project-info {
    padding: 1rem;
    transform: none;
  }

  .project-link {
    margin-top: 1rem;
    transform: none;
    box-shadow: none;
  }

  .project-indicators {
    margin-top: 1rem;
  }

  .show-more-container {
    margin-top: 1rem;
  }
}

.background-canvas {
  position: absolute;
  top: 0;
  left: 0;
  z-index: -1;
}
</style>