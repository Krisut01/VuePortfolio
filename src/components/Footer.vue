<template>
  <footer class="footer">
    <div class="footer-content">
      <p>&copy; 2023 Christian Doe. All rights reserved.</p>
      <div class="footer-actions">
        <div class="social-links">
          <a href="https://github.com" target="_blank" rel="noopener noreferrer">GitHub</a>
          <a href="https://linkedin.com" target="_blank" rel="noopener noreferrer">LinkedIn</a>
          <a href="https://twitter.com" target="_blank" rel="noopener noreferrer">Twitter</a>
        </div>
        <a href="/path-to-your-resume.pdf" download class="download-resume">Download Resume</a>
      </div>
    </div>
    <a href="#about" class="back-to-top" @click.prevent="scrollTo('about')">Back to Top</a>
  </footer>
</template>

<script>
export default {
  name: 'Footer',
  props: ['scrollTo']
}
</script>

<style scoped>
.footer {
  background-color: rgba(18, 18, 20, 0.6);
  backdrop-filter: blur(10px);
  color: rgba(255, 255, 255, 0.87);
  text-align: center;
  padding: 30px 0;
  font-size: 0.9rem;
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

.footer-actions {
  display: flex;
  align-items: center;
  gap: 20px;
}

.social-links {
  display: flex;
  gap: 20px;
}

.social-links a, .download-resume {
  color: rgba(255, 255, 255, 0.6);
  text-decoration: none;
  transition: color 0.3s ease;
}

.social-links a:hover, .download-resume:hover {
  color: #42b983;
}

.download-resume {
  background-color: rgba(66, 185, 131, 0.1);
  padding: 8px 16px;
  border-radius: 5px;
  border: 1px solid #42b983;
  font-weight: bold;
  transition: all 0.3s ease;
}

.download-resume:hover {
  background-color: #42b983;
  color: #0e0e10;
}

.back-to-top {
  display: inline-block;
  margin-top: 20px;
  padding: 10px 20px;
  background-color: #42b983;
  color: #0e0e10;
  text-decoration: none;
  border-radius: 5px;
  transition: all 0.3s ease;
  font-weight: bold;
}

.back-to-top:hover {
  background-color: #3aa876;
  transform: translateY(-3px);
  box-shadow: 0 5px 15px rgba(66, 185, 131, 0.4);
}

@media (max-width: 768px) {
  .footer-content {
    flex-direction: column;
    gap: 20px;
  }

  .footer-actions {
    flex-direction: column;
    align-items: center;
  }

  .social-links {
    margin-bottom: 10px;
  }
}
</style>