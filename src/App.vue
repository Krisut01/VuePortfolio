<template lang="">
  <div id="app">
    <Navbar :scrollTo="scrollTo" />
    <div class="content">
      <About :scrollTo="scrollTo" />
      <Projects />
      <Skills />
      <Contact />
    </div>
    <Footer :scrollTo="scrollTo" />
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue'
import About from './components/About.vue'
import Projects from './components/Projects.vue'
import Skills from './components/Skills.vue'
import Contact from './components/Contact.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Navbar,
    About,
    Projects,
    Skills,
    Contact,
    Footer
  },
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

<style>
@import './components/Styles/styles.css';

#app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.content {
  flex: 1;
  padding-top: 60px; /* Adjust based on navbar height */
  padding-bottom: 100px; /* Add padding to prevent footer overlap */
}

@media (max-width: 768px) {
  .content {
    padding-bottom: 0; /* Remove padding on mobile as footer is not fixed */
  }
}
</style>