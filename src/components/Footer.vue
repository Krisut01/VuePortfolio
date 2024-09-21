<template>
  <footer class="footer">
    <div class="footer-content">
      <p>&copy; 2023 John Doe. All rights reserved.</p>
      <div class="social-links">
        <a href="https://github.com" target="_blank" rel="noopener noreferrer">GitHub</a>
        <a href="https://linkedin.com" target="_blank" rel="noopener noreferrer">LinkedIn</a>
        <a href="https://twitter.com" target="_blank" rel="noopener noreferrer">Twitter</a>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'Footer'
}
</script>

<style scoped>
.footer {
  position: fixed;
  bottom: 20px;
  right: 20px;
  background-color: rgba(26, 42, 58, 0.8);
  backdrop-filter: blur(5px);
  border-radius: 10px;
  padding: 15px;
  z-index: 1000;
  transition: transform 0.3s ease;
}

.footer:hover {
  transform: translateY(-5px);
}

.footer-content {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}

.footer p {
  margin: 0 0 10px 0;
  font-size: 0.8rem;
  color: #e0e0e0;
}

.social-links {
  display: flex;
  gap: 15px;
}

.social-links a {
  color: #42b983;
  text-decoration: none;
  font-size: 0.9rem;
  transition: color 0.3s ease;
}

.social-links a:hover {
  color: #fff;
}

@media (max-width: 768px) {
  .footer {
    position: static;
    margin-top: 50px;
    border-radius: 0;
    width: 100%;
  }

  .footer-content {
    align-items: center;
  }
}
</style>