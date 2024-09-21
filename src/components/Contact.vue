<template>
  <section id="contact" class="section">
    <h2 class="section-title">Contact Me</h2>
    <div class="contact-container">
      <div class="contact-card form-card">
        <div class="card-content">
          <h3>Send a Message</h3>
          <form @submit.prevent="submitForm" class="contact-form">
            <div class="form-group">
              <input type="text" id="name" v-model="form.name" required>
              <label for="name">Name</label>
            </div>
            <div class="form-group">
              <input type="email" id="email" v-model="form.email" required>
              <label for="email">Email</label>
            </div>
            <div class="form-group">
              <textarea id="message" v-model="form.message" required></textarea>
              <label for="message">Message</label>
            </div>
            <button type="submit" class="submit-btn">
              <span>Send</span>
              <i class="fas fa-paper-plane"></i>
            </button>
          </form>
        </div>
      </div>
      <div class="contact-card info-card">
        <div class="card-content">
          <h3>Let's Create Something Amazing Together</h3>
          <p class="get-in-touch">
            Are you ready to take your digital presence to the next level? As a passionate full-stack developer, I'm excited to bring your ideas to life with cutting-edge technology and sleek design. Whether you're looking to launch a new project, optimize an existing one, or need a tech-savvy partner for your next big idea, I'm here to help you succeed in the digital world.
          </p>
          <ul class="contact-info">
            <li>
              <i class="fas fa-envelope"></i>
              <span>christian@gmail.com</span>
            </li>
            <li>
              <i class="fas fa-phone"></i>
              <span>0912345678</span>
            </li>
            <li>
              <i class="fas fa-map-marker-alt"></i>
              <span>Butuan City, Philippines</span>
            </li>
          </ul>
          <p class="cta-text">
            Don't hesitate to reach out. Your next groundbreaking project could be just one message away!
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Contact',
  data() {
    return {
      form: {
        name: '',
        email: '',
        message: ''
      }
    }
  },
  methods: {
    submitForm() {
      console.log('Form submitted:', this.form);
      // Here you would typically send the form data to a server
      // For now, we'll just reset the form
      this.form = { name: '', email: '', message: '' };
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

.contact-container {
  display: flex;
  gap: 2rem;
  max-width: 1200px;
  margin: 0 auto;
  animation: fadeIn 1s ease-out;
  perspective: 1000px;
}

.contact-card {
  flex: 1;
  background: rgba(18, 18, 20, 0.6);
  padding: 2rem;
  border-radius: 15px;
  transition: all 0.5s ease;
  transform-style: preserve-3d;
  backdrop-filter: blur(10px);
}

.contact-card:hover {
  transform: scale(1.05) translateZ(30px);
  box-shadow: 0 20px 40px rgba(66, 185, 131, 0.3);
}

.card-content {
  transition: all 0.5s ease;
}

.contact-card:hover .card-content {
  transform: translateZ(60px);
}

.form-card .card-content {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.info-card .card-content {
  text-align: left;
}

.contact-form {
  width: 100%;
  max-width: 400px;
}

.form-group {
  margin-bottom: 1.5rem;
  position: relative;
  transition: all 0.3s ease;
}

.form-group:hover {
  transform: scale(1.05) translateZ(10px);
}

input, textarea {
  width: 100%;
  padding: 0.75rem;
  padding-top: 1.5rem;
  background: rgba(255, 255, 255, 0.15);
  border: 1px solid rgba(255, 255, 255, 0.3);
  border-radius: 5px;
  color: #fff;
  font-size: 1rem;
  transition: all 0.3s ease;
}

label {
  position: absolute;
  left: 0.75rem;
  top: 0.5rem;
  color: rgba(255, 255, 255, 0.7);
  font-size: 0.8rem;
  transition: all 0.3s ease;
  pointer-events: none;
  background-color: transparent;
}

input:focus, textarea:focus {
  outline: none;
  box-shadow: 0 0 10px rgba(66, 185, 131, 0.5);
  background: rgba(255, 255, 255, 0.2);
  border-color: #42b983;
  transform: scale(1.05) translateZ(20px);
}

input:focus + label, textarea:focus + label,
input:not(:placeholder-shown) + label, textarea:not(:placeholder-shown) + label {
  color: #42b983;
  transform: translateY(-1.2rem) scale(0.8);
}

input::placeholder, textarea::placeholder {
  color: transparent;
}

input:focus::placeholder, textarea:focus::placeholder {
  color: rgba(255, 255, 255, 0.5);
}

.submit-btn {
  background: #42b983;
  color: #0e0e10;
  border: none;
  padding: 0.75rem 1.5rem;
  font-size: 1rem;
  border-radius: 5px;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  font-weight: bold;
}

.submit-btn:hover {
  background-color: #3aa876;
  transform: scale(1.05) translateZ(20px);
  box-shadow: 0 5px 15px rgba(66, 185, 131, 0.4);
}

.info-card h3 {
  color: #42b983;
  margin-bottom: 1rem;
  font-size: 1.5rem;
}

.get-in-touch {
  margin-bottom: 1.5rem;
  line-height: 1.6;
  color: rgba(255, 255, 255, 0.87);
}

.contact-info {
  list-style-type: none;
  padding: 0;
  margin-bottom: 1.5rem;
}

.contact-info li {
  margin-bottom: 0.5rem;
  color: rgba(255, 255, 255, 0.87);
  display: flex;
  align-items: center;
  gap: 10px;
  transition: all 0.3s ease;
}

.contact-info li:hover {
  transform: scale(1.05) translateZ(10px);
}

.contact-info i {
  color: #42b983;
  width: 20px;
}

.cta-text {
  font-style: italic;
  color: #42b983;
  font-weight: bold;
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

@media (max-width: 768px) {
  .contact-container {
    flex-direction: column;
  }
}

/* Add this new style for better contrast in the form card */
.form-card {
  background: rgba(24, 24, 28, 0.8);
}
</style>