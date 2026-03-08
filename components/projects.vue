<!-- u24666981 Motheo Morena -->

<template>
  <section id="projects" class="projects">
    <h2 class="section-title">Projects</h2>

    <div class="grid">
      <article
        v-for="proj in projects"
        :key="proj.id"
        class="card"
      >
        <a
          :href="proj.demo || proj.repo || '#'"
          target="_blank"
          rel="noopener"
          class="thumb"
          :aria-label="`Open ${proj.title}`"
        >
          <img
            :src="proj.image"
            :alt="proj.title + ' preview'"
            loading="lazy"
            decoding="async"
          />
        </a>

        <div class="card-body">
          <header class="card-head">
            <h3 class="card-title">{{ proj.title }}</h3>
            <p class="card-desc">{{ proj.description }}</p>
          </header>

          <ul class="tags" role="list">
            <li v-for="tag in proj.tags" :key="tag" class="tag">{{ tag }}</li>
          </ul>

          <div class="actions">
            <a
              v-if="proj.demo"
              :href="proj.demo"
              target="_blank"
              rel="noopener"
              class="btn btn-primary"
            >
              Live Demo
            </a>
            <a
              v-if="proj.repo"
              :href="proj.repo"
              target="_blank"
              rel="noopener"
              class="btn btn-ghost"
            >
              View Code
            </a>
          </div>
        </div>
      </article>
    </div>
  </section>
</template>

<script setup>
// Minimal, data‑driven projects. Replace links/images as you like.
const projects = [
  {
    id: 1,
    title: 'Modern Landing Page',
    description:
      'Clean, responsive landing page with a hero section, feature grid, and CTA. Built mobile-first.',
    tags: ['HTML', 'CSS', 'Accessibility'],
    image:
      'https://images.unsplash.com/photo-1498050108023-c5249f4df085?w=800&q=80&auto=format&fit=crop',
    demo: 'https://example.com/landing',
    repo: 'https://github.com/yourname/modern-landing'
  },
  {
    id: 2,
    title: 'Weather & Air Quality',
    description:
      'Simple weather dashboard showing temperature, PM2.5/PM10, and US AQI with color status.',
    tags: ['Vue 3', 'API', 'UI'],
    image:
      'https://images.unsplash.com/photo-1502303756781-9f4b1b2d8d53?w=800&q=80&auto=format&fit=crop',
    demo: 'https://example.com/weather',
    repo: 'https://github.com/yourname/weather-aqi'
  },
  {
    id: 3,
    title: 'Portfolio Starter',
    description:
      'A lightweight portfolio template with sections for About, Work, and Contact.',
    tags: ['Vue 3', 'Vite', 'Responsive'],
    image:
      'https://images.unsplash.com/photo-1526498460520-4c246339dccb?w=800&q=80&auto=format&fit=crop',
    demo: 'https://example.com/portfolio',
    repo: 'https://github.com/yourname/portfolio-starter'
  },
  {
    id: 4,
    title: 'Mini Store Grid',
    description:
      'Minimal e‑commerce product grid with cards, price, and hover effects.',
    tags: ['CSS Grid', 'UI', 'Components'],
    image:
      'https://images.unsplash.com/photo-1517336714731-489689fd1ca8?w=800&q=80&auto=format&fit=crop',
    demo: 'https://example.com/store',
    repo: 'https://github.com/yourname/mini-store-grid'
  }
];
</script>

<style scoped>
    .projects {
        padding: 1.5rem 0;
    }

    .section-title {
        font-size: 1.5rem;
        margin: 0 0 1rem;
        font-weight: 700;
    }

    .grid {
        display: grid;
        gap: 1rem;
        grid-template-columns: 1fr;
    }

    /* Responsive: 2 cols on md, 3 on lg */
    @media (min-width: 640px) {
        .grid { grid-template-columns: repeat(2, 1fr); }
    }
    @media (min-width: 1024px) {
        .grid { grid-template-columns: repeat(3, 1fr); }
    }

    .card {
    display: flex;
    flex-direction: column;
    border: 2px solid #e5e7eb;
    border-radius: 10px;
    overflow: hidden;
    }

    .thumb {
        display: block;
        aspect-ratio: 16 / 9;
        overflow: hidden;
    }

    .thumb img {
        width: 100%;
        height: 100%;
        object-fit: cover;
        transform: scale(1.02);
        transition: transform 200ms ease;
    }

    .thumb:hover img { transform: scale(1.06); }

    .card-body {
        display: grid;
        gap: 0.75rem;
        padding: 0.9rem;
    }

    .card-title {
        margin: 0 0 0.25rem;
        font-size: 1.05rem;
    }

    .card-desc {
        margin: 0;
        color: #ffffff;
        font-size: 0.95rem;
    }

    .tags {
        display: flex;
        flex-wrap: wrap;
        gap: 0.5rem;
        margin: 0;
        padding: 0;
        list-style: none;
    }

    .tag {
        font-size: 0.75rem;
        padding: 0.2rem 0.5rem;
        border-radius: 999px;
        background: #f1f5f9;
        color: #334155;
    }

    .actions {
        display: flex;
        gap: 0.5rem;
        margin-top: auto; /* push buttons to bottom for equal-height cards */
    }

    .btn {
        display: inline-flex;
        align-items: center;
        gap: 0.4rem;
        font-size: 0.85rem;
        padding: 0.45rem 0.7rem;
        border-radius: 8px;
        text-decoration: none;
        border: 1px solid transparent;
        transition: background 150ms ease, color 150ms ease, border-color 150ms ease;
    }

    .btn-primary {
        background: #0ea5e9;
        color: white;
    }

    .btn-primary:hover { background: #0284c7;}

    .btn-ghost {
        background: transparent;
        color: #0f172a;
        border-color: #e5e7eb;
    }

    .btn-ghost:hover {
        background: #f8fafc;
    }
</style>