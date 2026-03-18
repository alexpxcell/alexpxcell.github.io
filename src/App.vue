
<template>
  <div :class="{ dark: darkMode }" id="app">
    <nav>
      <div class="nav-container">
        <div class="brand">
          <a href="#hero">MyPortfolio</a>
        </div>
        <button class="hamburger" @click="toggleMenu" aria-label="Toggle Menu">
          <span :class="{ open: isMenuOpen }"></span>
          <span :class="{ open: isMenuOpen }"></span>
          <span :class="{ open: isMenuOpen }"></span>
        </button>
        <ul :class="{ 'nav-links': true, open: isMenuOpen }">
          <li><a href="#hero" @click="closeMenu">Home</a></li>
          <li><a href="#about" @click="closeMenu">About</a></li>
          <li><a href="#projects" @click="closeMenu">Projects</a></li>
          <li><a href="#contact" @click="closeMenu">Reach Out</a></li>
          <li><a href="#" @click="downloadResume">Resume</a></li>
          <li class="theme-toggle-li">
            <button @click="darkMode = !darkMode" class="theme-toggle">
              <Moon v-if="!darkMode" class="icon" />
              <Sun v-else class="icon" />
            </button>
          </li>
        </ul>
      </div>
    </nav>

    <main>
      <section id="hero" class="hero">
        <div class="hero-content">
          <h1>Welcome to My Portfolio</h1>
          <p>
            I am an engineering student with a passion for creating and building. I have experience in 3D design, embedded systems, and software development. I am always looking for new challenges and opportunities to learn and grow.
          </p>
        </div>
      </section>

      <section id="about" class="about">
        <h2>About Me</h2>
        <p>
          I am passionate about robotics, automation, and control systems. I am also interested in software development and machine learning. <br/> I am in my 3rd year of study at Jomo Kenyatta University of Agriculture and Technology, pursuing a Bachelor's of Science in Mechtronic Engineering.
        </p>
      </section>

      <section id="projects" class="projects">
        <h2>My Projects</h2>
        <div class="projects-grid">
          <div
            class="project-item"
            v-for="item in portfolioItems"
            :key="item.id"
            @click="openModal(item)"
          >
            <div class="project-image-container">
              <img :src="item.image" :alt="item.title" class="project-image" />
            </div>
            <div class="project-info">
              <h3>{{ item.title }}</h3>
            </div>
          </div>
        </div>
      </section>

      <div v-if="selectedProject" class="modal-overlay" @click="closeModalOutside">
        <div class="modal">
          <div class="modal-header">
            <h3>{{ selectedProject.title }}</h3>
            <button class="close-button" @click="selectedProject = null">&times;</button>
          </div>
          <div class="modal-body">
            <div class="project-details">
              <p><b>Summary:</b> {{ selectedProject.summary }}</p>
            </div>
            <div class="iframe-container" v-if="selectedProject.id >= 2">
              <iframe :src="getEmbedUrl(selectedProject.description)" allowfullscreen="true" webkitallowfullscreen="true" mozallowfullscreen="true" frameborder="0"></iframe>
            </div>
            <div v-else class="project-details">
              <img :src="selectedProject.image" :alt="selectedProject.title" class="modal-image" />
              <p v-html="selectedProject.description"></p>
            </div>
          </div>
        </div>
      </div>

      <section id="skills" class="skills">
        <h2>Skills</h2>
        <div class="skills-grid">
          <div v-for="skill in skills" :key="skill.name" class="skill-item">
            <div class="skill-label">
              <span>{{ skill.name }}</span>
              <span>{{ skill.level }}%</span>
            </div>
            <div class="skill-bar">
              <div class="skill-bar-value" :style="{ width: skill.level + '%' }"></div>
            </div>
          </div>
        </div>
      </section>

      <section id="contact" class="contact">
        <h2>Contact Me</h2>
        <form @submit.prevent="handleSubmit">
          <div class="form-group">
            <label for="name">Name</label>
            <input type="text" id="name" v-model="form.name" required />
          </div>
          <div class="form-group">
            <label for="email">Email</label>
            <input type="email" id="email" v-model="form.email" required />
          </div>
          <div class="form-group">
            <label for="message">Message</label>
            <textarea id="message" v-model="form.message" required></textarea>
          </div>
          <button type="submit" class="submit-button">Send</button>
        </form>
      </section>
    </main>

    <footer>
      <div class="footer-content">
        <h2>Find Me Online</h2>
        <div class="social-links">
          <a href="https://github.com/alexpxcell" target="_blank">GitHub</a>
          <a href="https://x.com/LWandugu" target="_blank">X</a>
          <a href="https://web.facebook.com/people/Alex-Thiongo/pfbid0k43xFKtaRk45DkT8Tn3tTnGqQn9Xqb5QNV1r3nadjB2ueBNq1sDwqd9R5RDLFdgol/" target="_blank">Facebook</a>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
import { Sun, Moon } from 'lucide-vue-next';

export default {
  components: { Sun, Moon },
  data() {
    return {
      darkMode: false,
      isMenuOpen: false,
      portfolioItems: [
        {
          id: 2,
          title: 'TSFM716320NC',
          description: 'https://students74781.autodesk360.com/shares/public/SH90d2dQT28d5b6028119747afffdf866161?mode=embed',
          image: 'images/myProject1.jpeg',
          summary: 'A 3D model of a floor mounted electrical panel, created using Fusion 360. The model is exported to Eplan Pro Panel where it is outfitted with an APFC Plant, stay tuned for the full tutorial.'
        },
        {
          id: 3,
          title: 'Robotic Arm',
          description: 'https://students74781.autodesk360.com/shares/public/SH90d2dQT28d5b602811c38937ffa3466e55?mode=embed',
          image: 'images/myProject2.jpeg',
          summary: 'A multi-axis robotic arm designed for educational and hobbyist purposes, featuring 3D-printed components. Single tendon actuation for the fore-fingers and a double tendon design for the thumb. Additional parts for the wrist will be available soon. Circuit design is ongoing stay tuned.'
        },
      ],
      skills: [
        { name: '3D Design (Fusion 360)', level: 58 },
        { name: 'Embedded Systems (Arduino, ESP32)', level: 48 },
        { name: 'C++', level: 45 },
        { name: 'Vue.js', level: 40 },
        { name: 'Circuit Design', level: 40 },
      ],
      form: {
        name: '',
        email: '',
        message: '',
      },
      selectedProject: null,
    };
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
    },
    closeMenu() {
      this.isMenuOpen = false;
    },
    downloadResume() {
      this.closeMenu();
      window.open('https://drive.google.com/file/d/1TKJw7aUM9-zCLeH7vgoypKc5zU3Td_RG/view?usp=sharing', '_blank');
    },
    openModal(item) {
      this.selectedProject = item;
    },
    closeModalOutside(event) {
      if (event.target.classList.contains('modal-overlay')) {
        this.selectedProject = null;
      }
    },
    getEmbedUrl(description) {
      return description;
    },
    handleSubmit() {
      alert('Form submitted!');
      this.form.name = '';
      this.form.email = '';
      this.form.message = '';
    },
  },
  watch: {
    darkMode(newValue) {
      if (newValue) {
        document.body.classList.add('dark');
      } else {
        document.body.classList.remove('dark');
      }
      localStorage.setItem('theme', newValue ? 'dark' : 'light');
    },
  },
  created() {
    const savedTheme = localStorage.getItem('theme');
    this.darkMode = savedTheme === 'dark';
  },
};
</script>

<style>
:root {
  --primary-color: #007bff;
  --secondary-color: #6c757d;
  --background-color: #ffffff;
  --text-color: #212529;
  --light-gray: #f8f9fa;
  --dark-gray: #343a40;
  --font-family: 'Poppins', sans-serif;
}

.dark {
  --primary-color: #4dabf7;
  --secondary-color: #adb5bd;
  --background-color: #121212;
  --text-color: #f8f9fa;
  --light-gray: #1e1e1e;
  --dark-gray: #f8f9fa;
}

body {
  font-family: var(--font-family);
  background-color: var(--background-color);
  color: var(--text-color);
  transition: background-color 0.3s ease, color 0.3s ease;
  margin: 0;
  padding: 0;
}

#app {
  max-width: 100%;
  overflow-x: hidden;
}

/* Navigation */
nav {
  background-color: var(--background-color);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  position: sticky;
  top: 0;
  z-index: 1000;
  padding: 1rem 2rem;
}

.nav-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
}

.brand a {
  font-size: 1.5rem;
  font-weight: 700;
  color: var(--primary-color);
  text-decoration: none;
}

.nav-links {
  display: flex;
  align-items: center;
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav-links li {
  margin: 0 1rem;
}

.nav-links a {
  color: var(--text-color);
  text-decoration: none;
  font-weight: 500;
  transition: color 0.3s ease;
}

.nav-links a:hover {
  color: var(--primary-color);
}

.theme-toggle {
  background: none;
  border: none;
  color: var(--text-color);
  cursor: pointer;
  font-size: 1.2rem;
}

.hamburger {
  display: none;
  flex-direction: column;
  justify-content: space-around;
  width: 2rem;
  height: 2rem;
  background: transparent;
  border: none;
  cursor: pointer;
  padding: 0;
  z-index: 10;
}

.hamburger span {
  width: 2rem;
  height: 0.25rem;
  background: var(--text-color);
  border-radius: 10px;
  transition: all 0.3s linear;
  position: relative;
  transform-origin: 1px;
}

/* Main Content */
main {
  padding: 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

section {
  padding: 4rem 0;
}

h1, h2 {
  text-align: center;
  margin-bottom: 2rem;
  font-weight: 700;
}

h1 {
  font-size: 3rem;
  color: var(--primary-color);
}

h2 {
  font-size: 2.5rem;
}

/* Hero */
.hero {
  text-align: center;
}

.hero p {
  font-size: 1.1rem;
  max-width: 700px;
  margin: 0 auto;
  line-height: 1.8;
}

/* Projects */
.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 2rem;
}

.project-item {
  background-color: var(--light-gray);
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.project-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 12px rgba(0, 0, 0, 0.15);
}

.project-image-container {
  width: 100%;
  padding-top: 56.25%; /* 16:9 Aspect Ratio */
  position: relative;
}

.project-image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.project-info {
  padding: 1.5rem;
}

.project-info h3 {
  margin: 0;
  font-size: 1.25rem;
  color: var(--primary-color);
}

/* Modal */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1001;
}

.modal {
  background: var(--background-color);
  border-radius: 8px;
  max-width: 90vw;
  max-height: 90vh;
  width: 800px;
  display: flex;
  flex-direction: column;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 1.5rem;
  border-bottom: 1px solid var(--light-gray);
}

.modal-header h3 {
  margin: 0;
  font-size: 1.5rem;
}

.close-button {
  background: none;
  border: none;
  font-size: 2rem;
  cursor: pointer;
  color: var(--text-color);
}

.modal-body {
  padding: 1.5rem;
  overflow-y: auto;
}

.iframe-container {
  position: relative;
  width: 100%;
  padding-top: 75%; /* 4:3 Aspect Ratio */
}

.iframe-container iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.project-details {
  text-align: left;
  margin-bottom: 1rem;
}

.modal-image {
  max-width: 100%;
  height: auto;
  border-radius: 8px;
  margin-bottom: 1rem;
}


/* Skills */
.skills-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1.5rem;
}

.skill-item {
  background-color: var(--light-gray);
  padding: 1.5rem;
  border-radius: 8px;
}

.skill-label {
  display: flex;
  justify-content: space-between;
  margin-bottom: 0.5rem;
  font-weight: 500;
}

.skill-bar {
  height: 10px;
  background-color: var(--secondary-color);
  border-radius: 5px;
}

.skill-bar-value {
  height: 100%;
  background-color: var(--primary-color);
  border-radius: 5px;
}

/* Contact */
.contact form {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  max-width: 600px;
  margin: 0 auto;
}

.form-group {
  display: flex;
  flex-direction: column;
}

.form-group label {
  margin-bottom: 0.5rem;
  font-weight: 500;
}

.form-group input,
.form-group textarea {
  padding: 0.75rem;
  border: 1px solid var(--secondary-color);
  border-radius: 4px;
  background-color: var(--background-color);
  color: var(--text-color);
  font-family: var(--font-family);
}

.submit-button {
  padding: 0.75rem 1.5rem;
  background-color: var(--primary-color);
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-weight: 500;
  transition: background-color 0.3s ease;
  align-self: flex-start;
}

.submit-button:hover {
  opacity: 0.9;
}

/* Footer */
footer {
  background-color: var(--light-gray);
  padding: 2rem;
  text-align: center;
}

.social-links a {
  margin: 0 1rem;
  color: var(--text-color);
  text-decoration: none;
  font-size: 1.1rem;
  transition: color 0.3s ease;
}

.social-links a:hover {
  color: var(--primary-color);
}

/* Responsive Styles */
@media (max-width: 768px) {
  nav {
    padding: 1rem;
  }

  .nav-links {
    position: fixed;
    top: 0;
    right: -100%;
    width: 250px;
    height: 100vh;
    flex-direction: column;
    align-items: flex-start;
    padding: 4rem 2rem;
    background-color: var(--background-color);
    box-shadow: -2px 0 5px rgba(0, 0, 0, 0.1);
    transition: right 0.3s ease-in-out;
  }

  .nav-links.open {
    right: 0;
  }

  .nav-links li {
    margin: 1rem 0;
  }

  .theme-toggle-li {
    position: absolute;
    bottom: 2rem;
  }

  .hamburger {
    display: flex;
  }

  h1 {
    font-size: 2.5rem;
  }

  h2 {
    font-size: 2rem;
  }
}

</style>
