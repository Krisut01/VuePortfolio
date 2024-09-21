<template>
  <nav class="navbar" :class="{ 'navbar-scrolled': isScrolled }">
    <div class="navbar-container">
      <div class="navbar-logo">
        <a href="#about" @click.prevent="scrollTo('about')">
          <span class="typing-container">
            <span class="typing-text">{{ currentText }}</span>
          </span>
        </a>
      </div>
      <div class="navbar-menu-toggle" @click="toggleMenu">
        <div class="bar"></div>
        <div class="bar"></div>
        <div class="bar"></div>
      </div>
      <ul class="navbar-menu" :class="{ 'active': isMenuOpen }">
        <li v-for="item in menuItems" :key="item.id">
          <a :href="`#${item.id}`" @click.prevent="scrollTo(item.id)">{{ item.name }}</a>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'Navbar',
  props: ['scrollTo'],
  data() {
    return {
      isScrolled: false,
      isMenuOpen: false,
      menuItems: [
        { id: 'about', name: 'About' },
        { id: 'projects', name: 'Projects' },
        { id: 'skills', name: 'Skills' },
        { id: 'contact', name: 'Contact' }
      ],
      currentText: '',
      fullTexts: ['Hello!', "I'm Christian Doe", 'A Web Developer'],
      textIndex: 0,
      charIndex: 0,
      isDeleting: false,
      typingSpeed: 150,
      deletingSpeed: 75,
      pauseDuration: 2000
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll);
    this.typeText();
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.handleScroll);
  },
  methods: {
    handleScroll() {
      this.isScrolled = window.scrollY > 50;
    },
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
    },
    typeText() {
      const currentFullText = this.fullTexts[this.textIndex];
      
      if (this.isDeleting) {
        this.currentText = currentFullText.substring(0, this.charIndex - 1);
        this.charIndex--;
      } else {
        this.currentText = currentFullText.substring(0, this.charIndex + 1);
        this.charIndex++;
      }

      let typingSpeed = this.isDeleting ? this.deletingSpeed : this.typingSpeed;

      if (!this.isDeleting && this.charIndex === currentFullText.length) {
        typingSpeed = this.pauseDuration;
        this.isDeleting = true;
      } else if (this.isDeleting && this.charIndex === 0) {
        this.isDeleting = false;
        this.textIndex = (this.textIndex + 1) % this.fullTexts.length;
      }

      setTimeout(() => this.typeText(), typingSpeed);
    }
  }
}
</script>

<style scoped>
.navbar {
  background-color: rgba(14, 14, 16, 0.8);
  backdrop-filter: blur(10px);
  transition: background-color 0.3s ease;
}

.navbar-scrolled {
  background-color: rgba(14, 14, 16, 0.95);
}

.navbar-container {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
}

.navbar-logo a {
  color: #ffffff;
  font-size: 1.8rem;
  font-weight: bold;
  text-decoration: none;
  letter-spacing: 1px;
  display: flex;
  align-items: center;
}

.typing-container {
  position: relative;
  display: inline-block;
  min-width: 200px;
}

.typing-text {
  position: relative;
  color: #42b983;
  font-weight: bold;
}

.typing-text::after {
  content: '|';
  position: absolute;
  right: -8px;
  top: 0;
  color: #42b983;
  animation: blink 0.7s infinite;
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0; }
}

.navbar-menu {
  list-style-type: none;
  padding: 0;
  margin: 0;
  display: flex;
}

.navbar-menu li {
  margin-left: 2rem;
}

.navbar-menu a {
  text-decoration: none;
  color: #ffffff;
  font-weight: 500;
  font-size: 1.1rem;
  transition: color 0.3s ease;
  position: relative;
}

.navbar-menu a::after {
  content: '';
  position: absolute;
  width: 0;
  height: 2px;
  bottom: -5px;
  left: 0;
  background-color: #42b983;
  transition: width 0.3s ease;
}

.navbar-menu a:hover {
  color: #42b983;
}

.navbar-menu a:hover::after {
  width: 100%;
}

.navbar-menu-toggle {
  display: none;
  flex-direction: column;
  cursor: pointer;
}

.bar {
  width: 25px;
  height: 3px;
  background-color: #ffffff;
  margin: 3px 0;
  transition: 0.4s;
}

@media (max-width: 768px) {
  .navbar-menu-toggle {
    display: flex;
  }

  .navbar-menu {
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    flex-direction: column;
    background-color: rgba(14, 14, 16, 0.95);
    padding: 1rem 0;
    clip-path: circle(0% at top right);
    transition: clip-path 0.5s ease-out;
  }

  .navbar-menu.active {
    clip-path: circle(150% at top right);
  }

  .navbar-menu li {
    margin: 1rem 0;
  }

  .navbar-menu a {
    display: block;
    padding: 0.5rem 2rem;
  }

  .navbar-menu a::after {
    display: none;
  }
}
</style>