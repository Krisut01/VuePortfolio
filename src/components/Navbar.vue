<template>
  <nav class="navbar" :class="{ 'navbar-scrolled': isScrolled }">
    <div class="navbar-container">
      <div class="navbar-logo">
        <a href="#about" @click.prevent="scrollTo('about')">
          <span class="typing-animation">{{ currentText }}</span>
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
      fullTexts: ['Christian Doe', 'Web Developer'],
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
    scrollTo(sectionId) {
      const element = document.getElementById(sectionId);
      if (element) {
        const yOffset = -60;
        const y = element.getBoundingClientRect().top + window.pageYOffset + yOffset;
        window.scrollTo({top: y, behavior: 'smooth'});
      }
      this.isMenuOpen = false;
    },
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
  background-color: rgba(14, 14, 16, 0.2); /* Darker, more transparent */
  backdrop-filter: blur(5px);
}

.navbar-scrolled {
  background-color: rgba(14, 14, 16, 0.8); /* Darker when scrolled */
}

.navbar-container {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 2rem;
}

.navbar-logo a {
  color: rgba(255, 255, 255, 0.87); /* High emphasis text */
  font-size: 1.8rem;
  font-weight: bold;
  text-decoration: none;
  letter-spacing: 1px;
  transition: all 0.3s ease;
}

.navbar-logo a:hover {
  color: #42b983;
  text-shadow: 0 0 10px rgba(66, 185, 131, 0.5);
}

.typing-animation {
  display: inline-block;
  overflow: hidden;
  border-right: 2px solid #42b983;
  white-space: nowrap;
  margin: 0 auto;
  animation: blink-caret 0.75s step-end infinite;
}

@keyframes blink-caret {
  from, to { border-color: transparent }
  50% { border-color: #42b983 }
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
  color: rgba(255, 255, 255, 0.6); /* Medium emphasis text */
  font-weight: 500;
  font-size: 1.1rem;
  transition: all 0.3s ease;
  position: relative;
  padding-bottom: 5px;
}

.navbar-menu a::after {
  content: '';
  position: absolute;
  width: 0;
  height: 2px;
  bottom: 0;
  left: 0;
  background-color: #42b983;
  transition: all 0.3s ease;
}

.navbar-menu a:hover {
  color: rgba(255, 255, 255, 0.87); /* High emphasis on hover */
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
  background-color: rgba(255, 255, 255, 0.87); /* High emphasis for menu toggle */
  margin: 3px 0;
  transition: all 0.3s ease;
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
    background-color: rgba(14, 14, 16, 0.95); /* Darker background for mobile menu */
    padding: 1rem 0;
    clip-path: circle(0% at top right);
    transition: all 0.5s ease-out;
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