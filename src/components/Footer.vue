<template>
  <footer class="footer">
    <div class="footer-content">
      <div class="footer-section">
        <p>&copy; {{ currentYear }} Christian Doe. All rights reserved.</p>
      </div>
      <div class="footer-section">
        <div class="social-links">
          <a href="https://github.com" target="_blank" rel="noopener noreferrer" aria-label="GitHub">
            <i class="fab fa-github"></i>
          </a>
          <a href="https://linkedin.com" target="_blank" rel="noopener noreferrer" aria-label="LinkedIn">
            <i class="fab fa-linkedin"></i>
          </a>
          <a href="https://twitter.com" target="_blank" rel="noopener noreferrer" aria-label="Twitter">
            <i class="fab fa-twitter"></i>
          </a>
        </div>
      </div>
      <div class="footer-section">
        <a href="/path-to-your-resume.pdf" download class="download-resume">Download Resume</a>
      </div>
    </div>
    <div class="back-to-top-container">
      <a href="#about" class="back-to-top" @click.prevent="scrollTo('about')">
        <i class="fas fa-chevron-up"></i>
      </a>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'Footer',
  props: ['scrollTo'],
  computed: {
    currentYear() {
      return new Date().getFullYear();
    }
  }
}
</script>

<style scoped>
.footer {
  background-color: rgba(18, 18, 20, 0.9);
  backdrop-filter: blur(10px);
  color: rgba(255, 255, 255, 0.87);
  padding: 2rem 0 1rem;
  position: relative;
  width: 100%;
  bottom: 0;
  left: 0;
  z-index: 10;
}

.footer-content {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  padding: 0 2rem;
}

.footer-section {
  margin: 0.5rem 0;
}

.social-links {
  display: flex;
  gap: 1rem;
}

.social-links a {
  color: rgba(255, 255, 255, 0.6);
  font-size: 1.5rem;
  transition: color 0.3s ease, transform 0.3s ease;
}

.social-links a:hover {
  color: #42b983;
  transform: translateY(-3px);
}

.download-resume {
  background-color: rgba(66, 185, 131, 0.1);
  padding: 0.5rem 1rem;
  border-radius: 5px;
  border: 1px solid #42b983;
  color: #42b983;
  text-decoration: none;
  font-weight: bold;
  transition: all 0.3s ease;
}

.download-resume:hover {
  background-color: #42b983;
  color: #0e0e10;
}

.back-to-top-container {
  position: absolute;
  top: -25px;
  left: 50%;
  transform: translateX(-50%);
}

.back-to-top {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 50px;
  height: 50px;
  background-color: #42b983;
  color: #0e0e10;
  text-decoration: none;
  border-radius: 50%;
  transition: all 0.3s ease;
  box-shadow: 0 2px 10px rgba(66, 185, 131, 0.3);
}

.back-to-top:hover {
  background-color: #3aa876;
  transform: translateY(-3px);
  box-shadow: 0 5px 15px rgba(66, 185, 131, 0.4);
}

@media (max-width: 768px) {
  .footer-content {
    flex-direction: column;
    text-align: center;
  }

  .footer-section {
    margin: 1rem 0;
  }

  .social-links {
    justify-content: center;
  }
}
</style>