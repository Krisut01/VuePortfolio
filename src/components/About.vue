<template>
  <section id="about" class="section">
    <div class="background-image"></div>
    <div class="content-wrapper">
      <h2 class="section-title">About Me</h2>
      <div class="about-content">
        <div class="image-container">
          <div class="image-border"></div>
          <img src="/images/1.jpg" alt="Profile" class="profile-image">
        </div>
        <div class="about-text">
          <p class="highlight">Hello! I'm Christian , a passionate full-stack developer with 5 years of experience in creating robust and scalable web applications.</p>
          <p>I specialize in JavaScript, Vue.js, Node.js, and Python, always excited to explore new technologies and best practices in software development.</p>
          <p>When I'm not coding, you can find me hiking in the mountains or experimenting with new recipes in the kitchen. I believe in the power of technology to solve real-world problems and I'm always looking for new challenges to tackle.</p>
          <div class="cta-container">
            <a href="#contact" class="cta-button" @click.prevent="scrollTo('contact')">Hire Me</a>
            <a href="#projects" class="cta-button secondary" @click.prevent="scrollTo('projects')">View Projects</a>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'About',
  methods: {
    scrollTo(sectionId) {
      const element = document.getElementById(sectionId);
      if (element) {
        element.scrollIntoView({ behavior: 'smooth' });
      }
    }
  }
}
</script>

<style scoped>
.section {
  position: relative;
  overflow: hidden;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem 1rem;
  background-color: #0e0e10; /* Match the body background color */
}

.background-image {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image: url('/images/3.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  opacity: 0.1;
  filter: blur(8px);
  z-index: 1;
  transform: scale(1.1);
}

.content-wrapper {
  position: relative;
  z-index: 2;
  width: 100%;
  max-width: 1200px;
}

.section-title {
  text-align: center;
  margin-bottom: 3rem;
  font-size: clamp(2rem, 5vw, 3rem);
  color: #42b983;
  text-shadow: 0 0 15px rgba(66, 185, 131, 0.7);
  animation: float 3s ease-in-out infinite;
}

.about-content {
  display: flex;
  align-items: center;
  gap: 50px;
  animation: fadeIn 1s ease-out;
  transform-style: preserve-3d;
  perspective: 1000px;
  background-color: rgba(18, 18, 20, 0.6); /* Slightly lighter than the background */
  padding: 2rem;
  border-radius: 15px;
  backdrop-filter: blur(10px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.image-container {
  flex-shrink: 0;
  perspective: 1000px;
  position: relative;
  width: 300px;
  height: 300px;
}

.image-border {
  position: absolute;
  top: -10px;
  left: -10px;
  right: -10px;
  bottom: -10px;
  border-radius: 50%;
  border: 2px dashed #42b983;
  animation: spin 20s linear infinite;
}

.profile-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 50%;
  box-shadow: 0 0 30px rgba(66, 185, 131, 0.3);
  transition: transform 0.5s ease;
  transform: rotateY(0deg);
  animation: float 6s ease-in-out infinite;
}

.profile-image:hover {
  transform: rotateY(10deg) scale(1.05);
}

.about-text {
  flex: 1;
  transform: translateZ(30px);
  background: rgba(255, 255, 255, 0.1);
  padding: 2rem;
  border-radius: 15px;
  backdrop-filter: blur(10px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.about-text p {
  margin-bottom: 20px;
  line-height: 1.8;
  text-align: left;
  color: rgba(255, 255, 255, 0.87); /* High emphasis text */
  font-size: clamp(1rem, 2vw, 1.1rem);
  transition: transform 0.3s ease;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
}

.about-text p.highlight {
  font-size: clamp(1.1rem, 2.5vw, 1.3rem);
  color: #42b983;
  font-weight: bold;
}

.about-text p:hover {
  transform: translateZ(10px);
}

.cta-container {
  display: flex;
  gap: 20px;
  margin-top: 30px;
  flex-wrap: wrap;
  justify-content: center;
}

.cta-button {
  padding: 12px 24px;
  background-color: #42b983;
  color: #0e0e10;
  text-decoration: none;
  border-radius: 30px;
  font-weight: bold;
  transition: all 0.3s ease;
  box-shadow: 0 5px 15px rgba(66, 185, 131, 0.3);
  font-size: clamp(0.9rem, 2vw, 1rem);
}

.cta-button:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 20px rgba(66, 185, 131, 0.5);
}

.cta-button.secondary {
  background-color: transparent;
  border: 2px solid #42b983;
  color: #42b983;
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(50px); }
  to { opacity: 1; transform: translateY(0); }
}

@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}

@keyframes spin {
  0% {
    transform: rotateY(0deg) rotateX(0deg);
  }
  100% {
    transform: rotateY(360deg) rotateX(360deg);
  }
}

@media (max-width: 1024px) {
  .about-content {
    flex-direction: column;
    text-align: center;
    gap: 30px;
  }

  .image-container {
    width: 250px;
    height: 250px;
  }

  .profile-image {
    width: 250px;
    height: 250px;
  }

  .about-text p {
    text-align: center;
  }
}

@media (max-width: 768px) {
  .section {
    padding: 1rem;
  }

  .image-container {
    width: 200px;
    height: 200px;
  }

  .profile-image {
    width: 200px;
    height: 200px;
  }

  .about-text {
    padding: 1.5rem;
  }

  .cta-container {
    flex-direction: column;
    align-items: center;
  }

  .cta-button {
    width: 100%;
    text-align: center;
  }
}

@media (max-width: 480px) {
  .section-title {
    margin-bottom: 2rem;
  }

  .image-container {
    width: 150px;
    height: 150px;
  }

  .profile-image {
    width: 150px;
    height: 150px;
  }

  .about-text {
    padding: 1rem;
  }
}
</style>