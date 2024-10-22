<template>
  <section id="about" class="section" ref="aboutSection">
    <div class="background-image"></div>
    <div class="content-wrapper">
      <h2 class="section-title" ref="sectionTitle">About Me</h2>
      <div class="about-content" ref="aboutContent">
        <div class="image-container" ref="imageContainer">
          <div class="image-border"></div>
          <img src="/images/3.jpeg" alt="Profile" class="profile-image">
        </div>
        <div class="about-text" ref="aboutText">
          <p class="highlight" ref="highlightText">Hello! I'm Christian, a dedicated student with several years of experience in HTML, Java, C, Python, web development, and Laravel, continuously expanding my skill set and expertise.</p>
          <p ref="paragraph1">I am passionate about programming and software development, always eager to explore cutting-edge technologies and industry best practices to deliver high-quality solutions.</p>
          <p ref="paragraph2">Outside of coding, I enjoy exploring nature and tackling new challenges by solving complex problems. I believe in leveraging technology to address real-world issues and am always looking for opportunities to grow and develop as a software engineer.</p>


          <div class="cta-container" ref="ctaContainer">
            <a href="#contact" class="cta-button" @click.prevent="scrollTo('contact')">Hire Me</a>
            <a href="#projects" class="cta-button secondary" @click.prevent="scrollTo('projects')">View Projects</a>
          </div>
        </div>
      </div>
    </div>
    <canvas ref="canvas" class="background-canvas"></canvas>
  </section>
</template>

<script>
import { gsap } from 'gsap';
import * as THREE from 'three';

export default {
  name: 'About',
  data() {
    return {
      scene: null,
      camera: null,
      renderer: null,
      geometry: null,
      material: null,
      mesh: null,
      isAnimating: false
    }
  },
  mounted() {
    this.initThreeJS();
    this.initAnimations();
    window.addEventListener('resize', this.onWindowResize);
  },
  beforeUnmount() {
    window.removeEventListener('resize', this.onWindowResize);
    this.disposeThreeJS();
  },
  methods: {
    scrollTo(sectionId) {
      const element = document.getElementById(sectionId);
      if (element) {
        element.scrollIntoView({ behavior: 'smooth' });
      }
    },
    initThreeJS() {
      this.scene = new THREE.Scene();
      this.camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
      this.renderer = new THREE.WebGLRenderer({ canvas: this.$refs.canvas, alpha: true });
      this.renderer.setSize(window.innerWidth, window.innerHeight);

      this.geometry = new THREE.SphereGeometry(1, 32, 32);
      this.material = new THREE.MeshBasicMaterial({ color: 0x42b983, wireframe: true });
      this.mesh = new THREE.Mesh(this.geometry, this.material);

      this.scene.add(this.mesh);
      this.camera.position.z = 5;

      this.animate();
    },
    animate() {
      requestAnimationFrame(this.animate);
      this.mesh.rotation.x += 0.01;
      this.mesh.rotation.y += 0.01;
      this.renderer.render(this.scene, this.camera);
    },
    onWindowResize() {
      this.camera.aspect = window.innerWidth / window.innerHeight;
      this.camera.updateProjectionMatrix();
      this.renderer.setSize(window.innerWidth, window.innerHeight);
    },
    disposeThreeJS() {
      this.geometry.dispose();
      this.material.dispose();
      this.renderer.dispose();
    },
    initAnimations() {
      const tl = gsap.timeline({ paused: true });

      tl.from(this.$refs.sectionTitle, { duration: 1, y: 50, opacity: 0, ease: 'power3.out' })
        .from(this.$refs.imageContainer, { duration: 1.5, scale: 0.5, opacity: 0, rotationY: 180, ease: 'back.out(1.7)' }, '-=0.5')
        .from(this.$refs.aboutText.children, { duration: 1, y: 30, opacity: 0, stagger: 0.2, ease: 'power3.out' }, '-=1')
        .from(this.$refs.ctaContainer.children, { duration: 0.8, scale: 0.5, opacity: 0, stagger: 0.2, ease: 'back.out(1.7)' }, '-=0.5');

      this.$refs.aboutSection.addEventListener('mouseenter', () => {
        if (!this.isAnimating) {
          this.isAnimating = true;
          tl.play();
        }
      });

      this.$refs.aboutSection.addEventListener('mouseleave', () => {
        if (this.isAnimating) {
          this.isAnimating = false;
          tl.reverse();
        }
      });
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
  background-color: rgb(0 0 0 / 60%);
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

.background-canvas {
  position: absolute;
  top: 0;
  left: 0;
  z-index: -1;
}
</style>