<template>
  <div id="app">
    <!-- NAV -->
    <header class="nav" :class="{ solid: scrolled }">
      <div class="nav-inner">
        <span class="logo" @click="scrollTo('hero')">tolibjon.dev</span>
        <nav class="links">
          <a
            v-for="l in nav"
            :key="l.id"
            @click="scrollTo(l.id)"
            :class="{ active: active === l.id }"
            >{{ l.label }}</a
          >
        </nav>
        <a href="mailto:tolibjonfayz@gmail.com" class="btn-nav">Hire Me</a>
      </div>
    </header>

    <!-- HERO -->
    <section id="hero" class="hero">
      <div class="hero-inner">
        <div class="hero-text">
          <p class="greeting"><span class="dot"></span> Available for work</p>
          <h1>Hi, I'm <span class="accent">Tolibjon Fayzullayev</span></h1>
          <h2 class="subtitle">
            Fullstack Developer
            <span class="stack-badges">
              <span class="badge">Node.js</span>
              <span class="badge">Vue.js</span>
            </span>
          </h2>
          <p class="bio">
            I build fast, clean web applications — from REST APIs to polished
            UIs. 2 years of professional experience, 2 companies, a few shipped
            products.
          </p>
          <div class="hero-actions">
            <button class="btn-primary" @click="scrollTo('projects')">
              See my work
            </button>
            <a
              href="/Tolibjon_Fayzullayev_CV.pdf"
              download
              class="btn-outline"
              target="_blank"
              >Download Resume</a
            >
          </div>
        </div>
        <div class="hero-card">
          <div class="code-window">
            <div class="win-bar">
              <span class="w-dot r"></span><span class="w-dot y"></span
              ><span class="w-dot g"></span>
              <span class="win-title">tolibjon.js</span>
            </div>
            <pre
              class="code-body"
            ><span class="ck">const</span> <span class="cv">developer</span> = {
  name<span class="cp">:</span>  <span class="cs">'Tolibjon Fayzullayev'</span>,
  role<span class="cp">:</span>  <span class="cs">'Fullstack Developer'</span>,
  exp<span class="cp">:</span>   <span class="cs">'2 years'</span>,
  stack<span class="cp">:</span> [<span class="cs">'Node.js'</span>, <span class="cs">'Vue.js'</span>,
         <span class="cs">'NuxtJS'</span>, <span class="cs">'PostgreSQL'</span>],
  open<span class="cp">:</span>  <span class="cb">true</span>, <span class="cmt">// to opportunities</span>
}
<span class="cmt">
// Let's build something together</span>
</pre>
          </div>
        </div>
      </div>
    </section>

    <!-- SKILLS -->
    <section id="skills" class="section">
      <div class="section-inner">
        <h3 class="sec-label">// skills</h3>
        <h2 class="sec-title"><span>What I work with</span></h2>
        <div class="skills-bento">
          <div
            class="bento-card featured"
            v-for="s in coreStack"
            :key="s.name"
            :style="{ '--sc': s.color }"
          >
            <div class="bento-icon" v-html="s.icon"></div>
            <div class="bento-name">{{ s.name }}</div>
            <div class="bento-desc">{{ s.desc }}</div>
            <div class="bento-exp">{{ s.exp }}</div>
          </div>
          <div
            class="bento-card list-card"
            v-for="cat in supportStack"
            :key="cat.name"
            :style="{ '--sc': cat.color }"
          >
            <div class="list-card-header">
              <span class="list-card-dot"></span>
              <span class="list-card-title">{{ cat.name }}</span>
            </div>
            <ul class="list-card-items">
              <li v-for="item in cat.items" :key="item">{{ item }}</li>
            </ul>
          </div>
        </div>
      </div>
    </section>

    <!-- EDUCATION -->
    <section id="education" class="section">
      <div class="section-inner">
        <h3 class="sec-label">// education</h3>
        <h2 class="sec-title"><span>Where I've learned</span></h2>
        <div class="edu-list">
          <div class="edu-item" v-for="(edu, i) in education" :key="i">
            <div class="edu-left">
              <div class="edu-year">{{ edu.period }}</div>
              <div class="edu-type-badge" :style="{ '--ec': edu.color }">
                {{ edu.type }}
              </div>
            </div>
            <div class="edu-body">
              <div class="edu-institution">{{ edu.institution }}</div>
              <div class="edu-degree">{{ edu.degree }}</div>
              <p class="edu-desc" v-if="edu.desc">{{ edu.desc }}</p>
              <div class="edu-tags" v-if="edu.tags">
                <span class="chip" v-for="t in edu.tags" :key="t">{{ t }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- EXPERIENCE -->
    <section id="experience" class="section alt">
      <div class="section-inner">
        <h3 class="sec-label">// experience</h3>
        <h2 class="sec-title"><span>Where I've worked</span></h2>
        <div class="exp-list">
          <div class="exp-item" v-for="(job, i) in experience" :key="i">
            <div class="exp-left">
              <div class="exp-period">{{ job.period }}</div>
            </div>
            <div class="exp-body">
              <div class="exp-header">
                <h3 class="exp-company">{{ job.company }}</h3>
                <span class="exp-role">{{ job.role }}</span>
              </div>
              <ul class="exp-tasks">
                <li v-for="t in job.tasks" :key="t">{{ t }}</li>
              </ul>
              <div class="exp-stack">
                <span class="chip" v-for="tech in job.stack" :key="tech">{{
                  tech
                }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- PROJECTS -->
    <section id="projects" class="section">
      <div class="section-inner">
        <h3 class="sec-label">// projects</h3>
        <h2 class="sec-title"><span>Things I've built</span></h2>
        <div class="projects-grid">
          <div class="project-card" v-for="p in projects" :key="p.name">
            <div class="browser-mockup">
              <div class="browser-bar">
                <div class="browser-dots">
                  <span class="b-dot r"></span>
                  <span class="b-dot y"></span>
                  <span class="b-dot g"></span>
                </div>
                <div class="browser-url">
                  <svg
                    width="10"
                    height="10"
                    viewBox="0 0 24 24"
                    fill="none"
                    stroke="currentColor"
                    stroke-width="2"
                  >
                    <rect x="3" y="11" width="18" height="11" rx="2" ry="2" />
                    <path d="M7 11V7a5 5 0 0 1 10 0v4" />
                  </svg>
                  <span>{{ p.url }}</span>
                </div>
                <div class="browser-actions">
                  <svg
                    width="12"
                    height="12"
                    viewBox="0 0 24 24"
                    fill="none"
                    stroke="currentColor"
                    stroke-width="2"
                  >
                    <polyline points="15 18 9 12 15 6" />
                  </svg>
                  <svg
                    width="12"
                    height="12"
                    viewBox="0 0 24 24"
                    fill="none"
                    stroke="currentColor"
                    stroke-width="2"
                  >
                    <polyline points="9 18 15 12 9 6" />
                  </svg>
                </div>
              </div>
              <div class="browser-screen" :style="{ background: p.imgBg }">
                <img :src="p.image" :alt="p.name" class="browser-img" />
                <div class="browser-overlay"></div>
              </div>
            </div>
            <div class="project-info">
              <div class="project-top">
                <span class="project-type">{{ p.type }}</span>
                <div class="project-links">
                  <a
                    v-if="p.github"
                    :href="p.github"
                    target="_blank"
                    title="GitHub"
                    class="icon-link"
                  >
                    <svg
                      width="15"
                      height="15"
                      viewBox="0 0 24 24"
                      fill="currentColor"
                    >
                      <path
                        d="M12 0C5.37 0 0 5.37 0 12c0 5.3 3.44 9.8 8.2 11.38.6.11.82-.26.82-.58v-2.03c-3.34.73-4.04-1.61-4.04-1.61-.54-1.38-1.33-1.75-1.33-1.75-1.08-.74.08-.72.08-.72 1.2.08 1.83 1.23 1.83 1.23 1.07 1.83 2.8 1.3 3.48 1 .1-.78.42-1.3.76-1.6-2.67-.3-5.47-1.33-5.47-5.93 0-1.31.47-2.38 1.24-3.22-.14-.3-.54-1.52.1-3.18 0 0 1.01-.32 3.3 1.23a11.5 11.5 0 0 1 3-.4c1.02 0 2.04.13 3 .4 2.28-1.55 3.3-1.23 3.3-1.23.64 1.66.24 2.88.12 3.18.77.84 1.23 1.91 1.23 3.22 0 4.61-2.8 5.63-5.48 5.92.43.37.81 1.1.81 2.22v3.29c0 .32.22.7.82.58C20.56 21.8 24 17.3 24 12c0-6.63-5.37-12-12-12z"
                      />
                    </svg>
                  </a>
                  <a
                    v-if="p.live"
                    :href="p.live"
                    target="_blank"
                    title="Live"
                    class="icon-link"
                  >
                    <svg
                      width="15"
                      height="15"
                      viewBox="0 0 24 24"
                      fill="none"
                      stroke="currentColor"
                      stroke-width="2"
                    >
                      <path
                        d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"
                      />
                      <polyline points="15,3 21,3 21,9" />
                      <line x1="10" y1="14" x2="21" y2="3" />
                    </svg>
                  </a>
                </div>
              </div>
              <h3 class="project-name">{{ p.name }}</h3>
              <p class="project-desc">{{ p.desc }}</p>
              <div class="project-stack">
                <span class="chip" v-for="t in p.tech" :key="t">{{ t }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- CONTACT -->
    <section id="contact" class="section alt">
      <div class="section-inner contact-inner">
        <div>
          <h3 class="sec-label">// contact</h3>
          <h2 class="sec-title"><span>Get in touch</span></h2>
          <p class="contact-bio">
            Open to fulltime roles, freelance projects, or just a good
            conversation about tech. Drop me a message, I reply within a day.
          </p>
          <div class="contact-links">
            <a
              v-for="c in contacts"
              :key="c.label"
              :href="c.href"
              target="_blank"
              class="contact-row"
            >
              <span class="c-icon">{{ c.icon }}</span>
              <span class="c-label">{{ c.label }}</span>
              <svg
                class="c-arrow"
                width="14"
                height="14"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
              >
                <path d="M5 12h14M12 5l7 7-7 7" />
              </svg>
            </a>
          </div>
        </div>
        <div class="contact-cta-box">
          <p class="cta-text">Ready to work together?</p>
          <a href="mailto:tolibjonfayz@gmail.com" class="btn-primary big"
            >Send me an email</a
          >
          <p class="cta-sub">tolibjonfayz@gmail.com</p>
        </div>
      </div>
    </section>

    <!-- FOOTER -->
    <footer class="footer">
      <span
        >Built with Vue.js by
        <span class="accent">Tolibjon Fayzullayev</span></span
      >
      <span class="footer-year">{{ new Date().getFullYear() }}</span>
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const nav = [
  { id: "skills", label: "Skills" },
  { id: "education", label: "Education" },
  { id: "experience", label: "Experience" },
  { id: "projects", label: "Projects" },
  { id: "contact", label: "Contact" },
];

const coreStack = [
  {
    name: "Vue.js",
    desc: "Primary frontend framework",
    exp: "2 yrs",
    color: "#42d392",
    icon: `<svg viewBox="0 0 128 128" width="32" height="32"><path fill="#42d392" d="M78.8 18.4L64 44.1 49.2 18.4H0l64 110.7L128 18.4z" opacity=".9"/><path fill="#35495e" d="M78.8 18.4L64 44.1 49.2 18.4H25.6L64 87l38.4-68.6z"/></svg>`,
  },
  {
    name: "Node.js",
    desc: "Backend runtime & APIs",
    exp: "2 yrs",
    color: "#68a063",
    icon: `<svg viewBox="0 0 128 128" width="32" height="32"><path fill="#68a063" d="M112.8 37.2L67.5 11a6.8 6.8 0 0 0-7 0L15.2 37.2A13.5 13.5 0 0 0 8.5 49v52.5a13.5 13.5 0 0 0 6.7 11.8l45.3 26.2a6.8 6.8 0 0 0 7 0l45.3-26.2a13.5 13.5 0 0 0 6.7-11.8V49a13.5 13.5 0 0 0-6.7-11.8z" opacity=".9"/></svg>`,
  },
  {
    name: "JavaScript",
    desc: "ES6+ & modern patterns",
    exp: "2 yrs",
    color: "#f7df1e",
    icon: `<svg viewBox="0 0 128 128" width="32" height="32"><rect width="128" height="128" rx="6" fill="#f7df1e"/><path d="M57.3 88.4c1.8 3 4.2 5.2 8.4 5.2 3.5 0 5.8-1.8 5.8-4.2 0-2.9-2.3-4-6.2-5.7l-2.1-.9c-6.2-2.6-10.3-5.9-10.3-12.9 0-6.4 4.9-11.3 12.5-11.3 5.4 0 9.3 1.9 12.1 6.8l-6.6 4.2c-1.5-2.6-3-3.6-5.5-3.6-2.5 0-4.1 1.6-4.1 3.6 0 2.5 1.6 3.5 5.2 5.1l2.1.9c7.3 3.1 11.4 6.3 11.4 13.4 0 7.7-6 11.9-14.1 11.9-7.9 0-13-3.8-15.5-8.7l6.9-4.8zm-27.4.8c1.3 2.3 2.5 4.3 5.4 4.3 2.7 0 4.5-1.1 4.5-5.2V59.3h8.5v29.3c0 8.6-5 12.5-12.4 12.5-6.6 0-10.5-3.4-12.4-7.6l6.4-4.3z" fill="#333"/></svg>`,
  },
  {
    name: "PostgreSQL",
    desc: "Relational DB & queries",
    exp: "1.5 yrs",
    color: "#336791",
    icon: `<svg viewBox="0 0 128 128" width="32" height="32"><path fill="#336791" d="M93.8 24.6C81 16.1 63 17.3 51.1 27.2a40.3 40.3 0 0 0-7 7.7c-4-1.5-8.1-2.5-12.4-2.2-9.4.6-18.3 6.6-22.2 15.2-2.5 5.5-2.8 11.7-1.3 17.5 1.5 5.9 4.9 11.2 9.6 15 4.5 3.7 10 5.8 15.7 6.1.8 3.4 2.3 6.7 4.5 9.4 3.3 4.2 8.1 7 13.3 7.8 5.3.8 10.8-.4 15.2-3.5 1.9 1.5 4 2.7 6.3 3.5 5 1.7 10.5 1.3 15.2-.9 4.7-2.2 8.4-6.1 10.4-10.9 4.6-.3 9.1-1.8 13-4.5 5.5-3.8 9.2-9.7 10.2-16.2 1-6.5-.7-13.2-4.5-18.5-3.8-5.2-9.5-8.7-15.8-9.6-.6-7.2-3.9-14.1-9-19.2z" opacity=".9"/></svg>`,
  },
];

const supportStack = [
  {
    name: "Frontend",
    color: "#4f9eff",
    items: [
      "Vue.js",
      "Nuxt.js",
      "TypeScript",
      "Tailwind CSS",
      "Pinia",
      "Vite",
      "HTML & CSS",
    ],
  },
  {
    name: "Backend",
    color: "#3dd68c",
    items: [
      "Node.js",
      "NestJS",
      "REST APIs",
      "MongoDB",
      "Redis",
      "WebSockets",
      "JWT",
    ],
  },
  {
    name: "Tools",
    color: "#e8a838",
    items: [
      "Git & GitHub",
      "Gitlab",
      "Postman",
      "Figma",
      "VS Code",
      "Docker",
      "Railway",
      "Vercel",
    ],
  },
];

const education = [
  {
    period: "Sep 2022 – present",
    type: "University",
    color: "#4f9eff",
    institution: "Tashkent State University of Economics",
    degree: "Finance and Financial Technologies",
    desc: "Bachelor's degree program focused on financial systems, fintech innovations, and economic principles. Coursework included programming, data analysis, and financial modeling.",
    tags: ["Finance", "Investment", "Networking"],
  },
  {
    period: "Apr 2023 – Dec 2023",
    type: "Course",
    color: "#4aa11e",
    institution: "Najot Ta'lim",
    degree: "Full stack (Node.js + Vue.js)",
    desc: "Intensive 9-month course covering fullstack web development with Node.js and Vue.js, including databases, REST APIs, and deployment",
    tags: [
      "Node.js",
      "Express.js",
      "Nest.js",
      "PostgreSQL",
      "Vue.js",
      "Nuxt.js",
      "Pinia",
      "Vite",
      "Redis",
      "Mongo DB",
    ],
  },
  {
    period: "Sep 2022 – Feb 2023",
    type: "Course",
    color: "#3dd68c",
    institution: "Najot Ta'lim",
    degree: "Foundation of programming",
    desc: "Intensive 5-month course covering programming fundamentals, algorithms, C and Python",
    tags: ["Algorithms", "C", "Python"],
  },
];

const experience = [
  {
    period: "Aug 2024 – Present",
    company: "Jihozvent",
    role: "Fullstack Web Developer",
    tasks: [
      "Built and maintained internal and client-facing web applications",
      "Developed scalable web solutions to support business growth",
      "Supported ongoing digital projects across the company",
    ],
    stack: [
      "Vue 3",
      "Nuxt.js",
      "Node.js",
      "Nest.js",
      "PostgreSQL",
      "Railway",
      "Vercel",
    ],
  },
  {
    period: "Apr 2024 – Jun 2024",
    company: "DT Ecosystem",
    role: "Junior Frontend Developer",
    tasks: [
      "Collaborated with a development team to build a personalized online store for company users. Contributed to frontend development that supported user experience and sales growth",
    ],
    stack: ["Vue 3", "Nuxt.js", "Sass", "Gitlab", "Figma"],
  },
];

const projects = [
  {
    name: "Climavent",
    type: "E-commerce platform (Frontend)",
    desc: "Sustainable online marketplace for eco-friendly products — personalized recommendations, seamless checkout, and a community forum.",
    tech: ["Nuxt.js", "Element Plus", "Pinia", "Scss"],
    github: "https://github.com/TolibjonFayz/climavent-front",
    live: "https://climavent.uz",
    url: "climavent.uz",
    image: "https://placehold.co/720x420/0d1117/4f9eff?text=Climavent",
    imgBg: "#0a0f1a",
  },
  {
    name: "Climavent Backend",
    type: "Backend Service",
    desc: "Robust REST API powering the Climavent platform — user auth, product management, order processing, and real-time notifications.",
    tech: ["Node.js", "Nest.js", "PostgreSQL", "JWT", "Sequelize"],
    github: null,
    live: null,
    url: "climavent.uz/api/docs",
    image: "https://placehold.co/720x420/0d1117/3dd68c?text=Climavent+Backend",
    github: "https://github.com/TolibjonFayz/climavent-back",
    imgBg: "#0a1410",
  },
  {
    name: "ERP Climavent",
    type: "ERP System (Frontend)",
    desc: "Internal ERP system for Climavent staff — customer data, sales tracking, attendance and analytics.",
    tech: ["Vue 3", "Scss", "Element Plus", "Pinia"],
    github: "https://github.com/TolibjonFayz/erp_climavent_frontend",
    live: "https://erp-climavent.vercel.app",
    url: "erp-climavent.vercel.app",
    image: "https://placehold.co/720x420/0d1117/e8a838?text=ERP+Climavent",
    imgBg: "#141008",
  },
  {
    name: "ERP Climavent Backend",
    type: "Backend Service",
    desc: "Robust REST API powering the ERP Climavent system — user auth, data management, and real-time notifications.",
    tech: ["Node.js", "Nest.js", "PostgreSQL", "JWT", "Sequelize"],
    github: null,
    live: null,
    url: "erp-climavent.vercel.app/api/docs",
    github: "https://github.com/TolibjonFayz/erp_climavent_backend",
    image: "https://placehold.co/720x420/0d1117/a78bfa?text=ERP+Backend",
    imgBg: "#0f0d17",
  },
];

const contacts = [
  {
    icon: "⌥",
    label: "github.com/TolibjonFayz",
    href: "https://github.com/TolibjonFayz",
  },
  {
    icon: "◈",
    label: "linkedin.com/in/tolibjonfayzullayev",
    href: "https://www.linkedin.com/in/tolibjonfayzullayev",
  },
  {
    icon: "✉",
    label: "tolibjonfayz@gmail.com",
    href: "mailto:tolibjonfayz@gmail.com",
  },
  { icon: "☎", label: "+998 90 815 04 12", href: "tel:+998908150412" },
  {
    icon: "✆",
    label: "@tolibjon_fayz (Telegram)",
    href: "https://t.me/tolibjon_fayz",
  },
];

const scrolled = ref(false);
const active = ref("hero");
function scrollTo(id) {
  document.getElementById(id)?.scrollIntoView({ behavior: "smooth" });
}

function onScroll() {
  scrolled.value = window.scrollY > 50;
  const ids = [
    "hero",
    "skills",
    "education",
    "experience",
    "projects",
    "contact",
  ];
  let found = "";
  for (const id of ids) {
    const el = document.getElementById(id);
    if (!el) continue;
    if (el.getBoundingClientRect().top <= 120) found = id;
  }
  if (found) active.value = found;
}

onMounted(() => {
  const link = document.createElement("link");
  link.rel = "stylesheet";
  link.href =
    "https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;600&family=Space+Grotesk:wght@400;500;600;700;800&display=swap";
  document.head.appendChild(link);
  window.addEventListener("scroll", onScroll);
});

onUnmounted(() => {
  window.removeEventListener("scroll", onScroll);
});
</script>

<style>
*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
html {
  scroll-behavior: smooth;
}
body {
  font-family: "Space Grotesk", sans-serif;
  background: #0d1117;
  color: #c9d1d9;
  line-height: 1.6;
  -webkit-font-smoothing: antialiased;
}
a {
  text-decoration: none;
  color: inherit;
}
ul {
  list-style: none;
}

:root {
  --accent: #4f9eff;
  --green: #3dd68c;
  --border: rgba(255, 255, 255, 0.08);
  --card: #161b22;
  --muted: #8b949e;
}

/* ─── NAV ─── */
.nav {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 99;
  padding: 0 5vw;
  height: 64px;
  display: flex;
  align-items: center;
  transition:
    background 0.25s,
    border-color 0.25s;
  border-bottom: 1px solid transparent;
}
.nav.solid {
  background: rgba(13, 17, 23, 0.92);
  backdrop-filter: blur(12px);
  border-color: var(--border);
}
.nav-inner {
  width: 100%;
  max-width: 1100px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  gap: 40px;
}
.logo {
  font-family: "JetBrains Mono", monospace;
  font-weight: 600;
  font-size: 0.95rem;
  color: #e6edf3;
  cursor: pointer;
  letter-spacing: -0.5px;
}
.logo::before {
  content: "./";
  color: var(--accent);
}
.links {
  display: flex;
  gap: 28px;
  margin-left: auto;
}
.links a {
  font-size: 0.88rem;
  color: var(--muted);
  cursor: pointer;
  transition: color 0.2s;
  position: relative;
  padding-bottom: 2px;
}
.links a::after {
  content: "";
  position: absolute;
  bottom: -2px;
  left: 0;
  width: 100%;
  height: 2px;
  background: var(--accent);
  transform: scaleX(0);
  transform-origin: left;
  transition: transform 0.2s;
}
.links a:hover,
.links a.active {
  color: #e6edf3;
}
.links a.active::after,
.links a:hover::after {
  transform: scaleX(1);
}
.btn-nav {
  font-family: "JetBrains Mono", monospace;
  font-size: 0.78rem;
  padding: 7px 16px;
  border: 1px solid var(--accent);
  color: var(--accent);
  border-radius: 6px;
  transition: all 0.2s;
  white-space: nowrap;
}
.btn-nav:hover {
  background: var(--accent);
  color: #0d1117;
}

/* ─── BUTTONS ─── */
.btn-primary {
  display: inline-block;
  background: var(--accent);
  color: #0d1117;
  font-family: "Space Grotesk", sans-serif;
  font-weight: 700;
  font-size: 0.9rem;
  padding: 12px 28px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition:
    opacity 0.2s,
    transform 0.2s;
}
.btn-primary:hover {
  opacity: 0.88;
  transform: translateY(-1px);
}
.btn-primary.big {
  font-size: 1rem;
  padding: 14px 36px;
}
.btn-outline {
  display: inline-block;
  color: #e6edf3;
  font-size: 0.9rem;
  padding: 12px 28px;
  border: 1px solid var(--border);
  border-radius: 8px;
  transition:
    border-color 0.2s,
    color 0.2s;
}
.btn-outline:hover {
  border-color: #e6edf3;
}

/* ─── HERO ─── */
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  padding: 100px 5vw 60px;
}
.hero-inner {
  width: 100%;
  max-width: 1100px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 60px;
}
.hero-text {
  flex: 1;
  max-width: 560px;
}
.greeting {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  font-family: "JetBrains Mono", monospace;
  font-size: 0.8rem;
  color: var(--green);
  margin-bottom: 20px;
  padding: 6px 14px;
  border: 1px solid rgba(61, 214, 140, 0.25);
  border-radius: 100px;
  background: rgba(61, 214, 140, 0.06);
}
.dot {
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: var(--green);
  animation: pulse 2s infinite;
}
@keyframes pulse {
  0%,
  100% {
    box-shadow: 0 0 0 0 rgba(61, 214, 140, 0.5);
  }
  50% {
    box-shadow: 0 0 0 5px rgba(61, 214, 140, 0);
  }
}
.hero-text h1 {
  font-size: clamp(2.2rem, 4.5vw, 3.4rem);
  font-weight: 800;
  color: #e6edf3;
  line-height: 1.15;
  margin-bottom: 12px;
}
.accent {
  color: var(--accent);
}
.subtitle {
  font-size: 1.2rem;
  font-weight: 600;
  color: var(--muted);
  margin-bottom: 24px;
  display: flex;
  align-items: center;
  gap: 12px;
  flex-wrap: wrap;
}
.stack-badges {
  display: flex;
  gap: 8px;
}
.badge {
  font-family: "JetBrains Mono", monospace;
  font-size: 0.7rem;
  padding: 3px 10px;
  background: rgba(79, 158, 255, 0.12);
  border: 1px solid rgba(79, 158, 255, 0.3);
  border-radius: 4px;
  color: var(--accent);
}
.bio {
  font-size: 1rem;
  color: var(--muted);
  line-height: 1.75;
  margin-bottom: 36px;
}
.hero-actions {
  display: flex;
  gap: 14px;
  flex-wrap: wrap;
}

/* ─── CODE WINDOW ─── */
.hero-card {
  flex-shrink: 0;
}
.code-window {
  background: #161b22;
  border: 1px solid var(--border);
  border-radius: 10px;
  overflow: hidden;
  width: 380px;
  box-shadow: 0 24px 64px rgba(0, 0, 0, 0.4);
}
.win-bar {
  display: flex;
  align-items: center;
  gap: 6px;
  padding: 12px 16px;
  background: #1c2128;
  border-bottom: 1px solid var(--border);
}
.w-dot {
  width: 11px;
  height: 11px;
  border-radius: 50%;
}
.w-dot.r {
  background: #ff5f57;
}
.w-dot.y {
  background: #febc2e;
}
.w-dot.g {
  background: #28c840;
}
.win-title {
  margin-left: 8px;
  font-family: "JetBrains Mono", monospace;
  font-size: 0.75rem;
  color: var(--muted);
}
.code-body {
  font-family: "JetBrains Mono", monospace;
  font-size: 0.82rem;
  line-height: 1.8;
  padding: 20px 24px;
  color: #c9d1d9;
  white-space: pre;
  overflow-x: auto;
}
.ck {
  color: #ff7b72;
}
.cv {
  color: #79c0ff;
}
.cs {
  color: #a5d6ff;
}
.cp {
  color: #c9d1d9;
}
.cb {
  color: #79c0ff;
}
.cmt {
  color: #484f58;
  font-style: italic;
}

/* ─── SECTIONS ─── */
.section {
  padding: 90px 5vw;
}
.section.alt {
  background: #0a0f15;
}
.section-inner {
  max-width: 1100px;
  margin: 0 auto;
}
.sec-label {
  font-family: "JetBrains Mono", monospace;
  font-size: 0.82rem;
  color: var(--accent);
  margin-bottom: 8px;
  display: block;
}
.sec-title {
  font-size: clamp(1.6rem, 2.5vw, 2.2rem);
  font-weight: 800;
  color: #e6edf3;
  margin-bottom: 40px;
  line-height: 1;
  overflow: visible;
}
.sec-title span {
  display: inline-block;
  line-height: 1.3;
  padding-bottom: 10px;
}

/* ─── SKILLS BENTO ─── */
.skills-bento {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: auto auto;
  gap: 16px;
}
.bento-card.featured {
  background: var(--card);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 14px;
  padding: 24px;
  display: flex;
  flex-direction: column;
  gap: 10px;
  position: relative;
  overflow: hidden;
  transition:
    border-color 0.25s,
    transform 0.25s;
  cursor: default;
}
.bento-card.featured::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 2px;
  background: var(--sc);
  opacity: 0.7;
}
.bento-card.featured:hover {
  border-color: color-mix(in srgb, var(--sc) 40%, transparent);
  transform: translateY(-3px);
}
.bento-icon {
  width: 44px;
  height: 44px;
  background: color-mix(in srgb, var(--sc) 12%, transparent);
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 6px;
  margin-bottom: 4px;
}
.bento-icon svg {
  display: block;
}
.bento-name {
  font-family: "Space Grotesk", sans-serif;
  font-size: 1rem;
  font-weight: 700;
  color: #e6edf3;
}
.bento-desc {
  font-size: 0.8rem;
  color: var(--muted);
  line-height: 1.4;
}
.bento-exp {
  font-family: "JetBrains Mono", monospace;
  font-size: 0.68rem;
  color: var(--sc);
  margin-top: auto;
  padding-top: 12px;
  border-top: 1px solid rgba(255, 255, 255, 0.06);
}
.bento-card.list-card {
  background: var(--card);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 14px;
  padding: 20px 24px;
  transition: border-color 0.25s;
}
.bento-card.list-card:nth-child(5) {
  grid-column: 1 / 3;
}
.bento-card.list-card:nth-child(6) {
  grid-column: 3 / 5;
}
.bento-card.list-card:nth-child(7) {
  grid-column: 1 / 5;
  display: grid;
  grid-template-columns: 180px 1fr;
  align-items: start;
  gap: 24px;
}
.bento-card.list-card:hover {
  border-color: rgba(255, 255, 255, 0.15);
}
.list-card-header {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 16px;
}
.bento-card.list-card:nth-child(7) .list-card-header {
  margin-bottom: 0;
  align-self: center;
}
.list-card-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: var(--sc);
  flex-shrink: 0;
}
.list-card-title {
  font-family: "JetBrains Mono", monospace;
  font-size: 0.72rem;
  font-weight: 600;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  color: var(--sc);
}
.list-card-items {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  list-style: none;
}
.list-card-items li {
  font-family: "JetBrains Mono", monospace;
  font-size: 0.76rem;
  color: var(--muted);
  padding: 5px 12px;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 6px;
  transition:
    color 0.2s,
    border-color 0.2s;
}
.list-card-items li:hover {
  color: #c9d1d9;
  border-color: rgba(255, 255, 255, 0.18);
}

/* ─── EDUCATION ─── */
.edu-list {
  display: flex;
  flex-direction: column;
  gap: 20px;
}
.edu-item {
  display: grid;
  grid-template-columns: 160px 1fr;
  gap: 32px;
  align-items: start;
  padding: 28px 32px 32px;
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: 12px;
  transition:
    border-color 0.25s,
    transform 0.25s;
}
.edu-item:hover {
  border-color: rgba(255, 255, 255, 0.16);
  transform: translateY(-2px);
}
.edu-left {
  display: flex;
  flex-direction: column;
  gap: 10px;
  padding-top: 2px;
}
.edu-year {
  font-family: "JetBrains Mono", monospace;
  font-size: 0.75rem;
  color: var(--accent);
  white-space: nowrap;
}
.edu-type-badge {
  display: inline-block;
  font-family: "JetBrains Mono", monospace;
  font-size: 0.65rem;
  font-weight: 600;
  letter-spacing: 1px;
  text-transform: uppercase;
  padding: 4px 10px;
  border-radius: 100px;
  color: var(--ec);
  background: color-mix(in srgb, var(--ec) 10%, transparent);
  border: 1px solid color-mix(in srgb, var(--ec) 30%, transparent);
  width: fit-content;
}
.edu-institution {
  font-size: 1.05rem;
  font-weight: 700;
  color: #e6edf3;
  margin-bottom: 4px;
}
.edu-degree {
  font-size: 0.9rem;
  color: var(--accent);
  font-weight: 600;
  margin-bottom: 10px;
}
.edu-desc {
  font-size: 0.88rem;
  color: var(--muted);
  line-height: 1.9;
  margin-bottom: 14px;
}
.edu-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

/* ─── EXPERIENCE ─── */
.exp-list {
  display: flex;
  flex-direction: column;
}
.exp-item {
  display: grid;
  grid-template-columns: 160px 1fr;
  gap: 32px;
}
.exp-item + .exp-item {
  margin-top: 40px;
  padding-top: 40px;
  border-top: 1px solid var(--border);
}
.exp-left {
  padding-top: 4px;
}
.exp-period {
  font-family: "JetBrains Mono", monospace;
  font-size: 0.75rem;
  color: var(--accent);
  white-space: nowrap;
}
.exp-header {
  margin-bottom: 12px;
}
.exp-company {
  font-size: 1.15rem;
  font-weight: 700;
  color: #e6edf3;
  margin-bottom: 4px;
}
.exp-role {
  font-size: 0.85rem;
  color: var(--muted);
}
.exp-tasks {
  margin-bottom: 16px;
}
.exp-tasks li {
  font-size: 0.9rem;
  color: var(--muted);
  padding-left: 14px;
  position: relative;
  margin-bottom: 8px;
  line-height: 1.8;
}
.exp-tasks li::before {
  content: "–";
  position: absolute;
  left: 0;
  color: var(--accent);
}
.exp-stack {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

/* ─── CHIP ─── */
.chip {
  font-family: "JetBrains Mono", monospace;
  font-size: 0.7rem;
  padding: 4px 10px;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid var(--border);
  border-radius: 4px;
  color: var(--muted);
  transition:
    color 0.2s,
    border-color 0.2s;
}
.chip:hover {
  color: #c9d1d9;
  border-color: rgba(255, 255, 255, 0.2);
}

/* ─── PROJECTS ─── */
.projects-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 28px;
}
.browser-mockup {
  border-radius: 8px 8px 0 0;
  overflow: hidden;
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-bottom: none;
  background: #1c2128;
  margin: -24px -24px 20px -24px;
}
.browser-bar {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 9px 14px;
  background: #1c2128;
  border-bottom: 1px solid rgba(255, 255, 255, 0.07);
}
.browser-dots {
  display: flex;
  gap: 5px;
}
.b-dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
}
.b-dot.r {
  background: #ff5f57;
}
.b-dot.y {
  background: #febc2e;
}
.b-dot.g {
  background: #28c840;
}
.browser-url {
  flex: 1;
  display: flex;
  align-items: center;
  gap: 6px;
  background: rgba(255, 255, 255, 0.06);
  border-radius: 5px;
  padding: 4px 10px;
  font-family: "JetBrains Mono", monospace;
  font-size: 0.68rem;
  color: var(--muted);
  overflow: hidden;
  white-space: nowrap;
}
.browser-url svg {
  flex-shrink: 0;
  color: var(--green);
  opacity: 0.7;
}
.browser-actions {
  display: flex;
  gap: 6px;
  color: var(--muted);
  opacity: 0.5;
}
.browser-screen {
  position: relative;
  aspect-ratio: 16/9;
  overflow: hidden;
}
.browser-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  transition: transform 0.5s ease;
}
.browser-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(
    to bottom,
    transparent 50%,
    rgba(22, 27, 34, 0.6) 100%
  );
  pointer-events: none;
}
.project-card:hover .browser-img {
  transform: scale(1.03);
}
/* FIX: overflow: hidden OLIB TASHLANDI — descender clipping sababi shu edi */
.project-card {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: 10px;
  padding: 24px;
  display: flex;
  flex-direction: column;
  transition:
    border-color 0.25s,
    transform 0.25s,
    box-shadow 0.25s;
}
.project-card:hover {
  border-color: rgba(79, 158, 255, 0.3);
  transform: translateY(-4px);
  box-shadow: 0 16px 40px rgba(0, 0, 0, 0.4);
}
.project-info {
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.project-top {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.project-type {
  font-family: "JetBrains Mono", monospace;
  font-size: 0.7rem;
  color: var(--accent);
  padding: 3px 8px;
  background: rgba(79, 158, 255, 0.1);
  border-radius: 4px;
}
.project-links {
  display: flex;
  gap: 10px;
}
.icon-link {
  color: var(--muted);
  transition: color 0.2s;
}
.icon-link:hover {
  color: #e6edf3;
}
.project-name {
  font-size: 1.05rem;
  font-weight: 700;
  color: #e6edf3;
}
.project-desc {
  font-size: 0.87rem;
  color: var(--muted);
  line-height: 1.8;
  flex: 1;
}
.project-stack {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  margin-top: 4px;
}

/* ─── CONTACT ─── */
.contact-inner {
  display: grid;
  grid-template-columns: 1fr auto;
  gap: 80px;
  align-items: start;
}
.contact-bio {
  font-size: 0.97rem;
  color: var(--muted);
  line-height: 1.75;
  margin-bottom: 32px;
}
.contact-links {
  display: flex;
  flex-direction: column;
  gap: 12px;
}
.contact-row {
  display: flex;
  align-items: center;
  gap: 14px;
  font-size: 0.88rem;
  color: var(--muted);
  padding: 12px 16px;
  border: 1px solid var(--border);
  border-radius: 8px;
  transition: all 0.2s;
}
.contact-row:hover {
  color: #e6edf3;
  border-color: rgba(255, 255, 255, 0.16);
  background: rgba(255, 255, 255, 0.03);
}
.c-icon {
  font-size: 1rem;
  color: var(--accent);
  width: 20px;
  text-align: center;
}
.c-arrow {
  margin-left: auto;
  opacity: 0;
  transition:
    opacity 0.2s,
    transform 0.2s;
}
.contact-row:hover .c-arrow {
  opacity: 1;
  transform: translateX(3px);
}
.contact-cta-box {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 36px 32px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 16px;
  text-align: center;
  min-width: 240px;
}
.cta-text {
  font-size: 1.05rem;
  font-weight: 700;
  color: #e6edf3;
}
.cta-sub {
  font-family: "JetBrains Mono", monospace;
  font-size: 0.78rem;
  color: var(--muted);
}

/* ─── FOOTER ─── */
.footer {
  padding: 28px 5vw;
  border-top: 1px solid var(--border);
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 0.82rem;
  color: var(--muted);
}
.footer-year {
  font-family: "JetBrains Mono", monospace;
}

/* ─── RESPONSIVE ─── */
@media (max-width: 860px) {
  .hero-inner {
    flex-direction: column;
  }
  .hero-card {
    width: 100%;
  }
  .code-window {
    width: 100%;
  }
  .links {
    display: none;
  }
  .skills-bento {
    grid-template-columns: repeat(2, 1fr);
  }
  .bento-card.list-card:nth-child(5),
  .bento-card.list-card:nth-child(6) {
    grid-column: span 1;
  }
  .bento-card.list-card:nth-child(7) {
    grid-column: 1 / -1;
    grid-template-columns: 1fr;
    gap: 12px;
  }
  .edu-item {
    grid-template-columns: 1fr;
    gap: 12px;
  }
  .exp-item {
    grid-template-columns: 1fr;
    gap: 8px;
  }
  .contact-inner {
    grid-template-columns: 1fr;
    gap: 40px;
  }
  .projects-grid {
    grid-template-columns: 1fr;
  }
}
</style>
