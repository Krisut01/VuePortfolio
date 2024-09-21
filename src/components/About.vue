<template>
  <section id="about" class="section">
    <h2 class="section-title">About Me</h2>
    <div class="about-content">
      <div class="image-container">
        <img src="/images/1.jpg" alt="Profile" class="profile-image">
      </div>
      <div class="about-text">
        <p>Hello! I'm Christian , a passionate full-stack developer with 5 years of experience in creating robust and scalable web applications.</p>
        <p>I specialize in JavaScript, Vue.js, Node.js, and Python, always excited to explore new technologies and best practices in software development.</p>
        <p>When I'm not coding, you can find me hiking in the mountains or experimenting with new recipes in the kitchen. I believe in the power of technology to solve real-world problems and I'm always looking for new challenges to tackle.</p>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'About'
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

.about-content {
  display: flex;
  align-items: center;
  gap: 50px;
  animation: fadeIn 1s ease-out;
  transform-style: preserve-3d;
  perspective: 1000px;
}

.image-container {
  flex-shrink: 0;
  perspective: 1000px;
}

.profile-image {
  width: 300px;
  height: 300px;
  object-fit: cover;
  border-radius: 50%;
  box-shadow: 0 0 30px rgba(66, 185, 131, 0.3);
  transition: transform 0.5s ease;
  transform: rotateY(0deg);
}

.profile-image:hover {
  transform: rotateY(10deg) scale(1.05);
}

.about-text {
  flex: 1;
  transform: translateZ(30px);
}

.about-text p {
  margin-bottom: 20px;
  line-height: 1.8;
  text-align: left;
  color: #e0e0e0;
  font-size: 1.1rem;
  transition: transform 0.3s ease;
}

.about-text p:hover {
  transform: translateZ(10px);
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(50px); }
  to { opacity: 1; transform: translateY(0); }
}

@media (max-width: 768px) {
  .about-content {
    flex-direction: column;
    text-align: center;
  }

  .profile-image {
    width: 250px;
    height: 250px;
    margin-bottom: 30px;
  }

  .about-text p {
    text-align: center;
  }
}
</style>