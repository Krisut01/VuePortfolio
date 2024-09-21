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
          <h3>Get in Touch</h3>
          <p>I'm always open to new opportunities and collaborations. Feel free to reach out!</p>
          <ul class="contact-info">
            <li>
              <i class="fas fa-envelope"></i>
              <span>john.doe@example.com</span>
            </li>
            <li>
              <i class="fas fa-phone"></i>
              <span>+1 (123) 456-7890</span>
            </li>
            <li>
              <i class="fas fa-map-marker-alt"></i>
              <span>San Francisco, CA</span>
            </li>
          </ul>
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
  max-width: 1000px;
  margin: 0 auto;
  animation: fadeIn 1s ease-out;
  perspective: 1000px;
}

.contact-card {
  flex: 1;
  background: rgba(255, 255, 255, 0.1);
  padding: 2rem;
  border-radius: 15px;
  transition: transform 0.5s ease, box-shadow 0.5s ease;
  transform-style: preserve-3d;
}

.contact-card:hover {
  transform: translateY(-10px) rotateX(5deg) rotateY(5deg);
  box-shadow: 0 20px 40px rgba(66, 185, 131, 0.3);
}

.card-content {
  transform: translateZ(30px);
}

.form-card .card-content {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.info-card .card-content {
  text-align: center;
}

.contact-form {
  width: 100%;
  max-width: 400px;
}

.form-group {
  margin-bottom: 1.5rem;
  position: relative;
}

input, textarea {
  width: 100%;
  padding: 0.75rem;
  background: rgba(255, 255, 255, 0.1);
  border: none;
  border-radius: 5px;
  color: #fff;
  font-size: 1rem;
  transition: all 0.3s ease;
}

label {
  position: absolute;
  left: 0.75rem;
  top: 0.75rem;
  color: #aaa;
  transition: all 0.3s ease;
  pointer-events: none;
}

input:focus, textarea:focus {
  outline: none;
  box-shadow: 0 0 10px rgba(66, 185, 131, 0.5);
}

input:focus + label, textarea:focus + label,
input:not(:placeholder-shown) + label, textarea:not(:placeholder-shown) + label {
  top: -1.5rem;
  font-size: 0.8rem;
  color: #42b983;
}

.submit-btn {
  background: #42b983;
  color: #fff;
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
}

.submit-btn:hover {
  background-color: #3aa876;
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(66, 185, 131, 0.4);
}

.contact-info h3 {
  color: #42b983;
  margin-bottom: 1rem;
}

.contact-info ul {
  list-style-type: none;
  padding: 0;
}

.contact-info li {
  margin-bottom: 0.5rem;
  color: #e0e0e0;
  display: flex;
  align-items: center;
  gap: 10px;
}

.contact-info i {
  color: #42b983;
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
</style>