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
        title: "Simple Favourite Artists' website",
        description:
        'Simple website of Beyonce.',
        tags: ['HTML', 'CSS', 'UI'],
        image:
        'https://outsmartmag.s3.us-east-2.amazonaws.com/wp-content/uploads/2024/04/04152635/FEATURE_beyonce-cowboy-carter-first.jpg',
        demo: 'https://motheo-365.github.io/Beyonce/'
    },
    {
        id: 2,
        title: 'Flight Booking Website',
        description:
        'A simple non-functional flight booking website, for JetMotheo',
        tags: ['HTML', 'CSS','UI'],
        image:
        'https://www.sciencing.com/sciencing/difference-between-jet-plane-5263274/57d2067ecc744a07b20d4698aa11fcd4.jpg',
        demo: 'https://motheo-365.github.io/jet-motheo/'
    },
    {
        id: 3,
        title: 'Ticket Issuer',
        description:
        'A lightweight ticket issuing website.',
        tags: ['Vue 3', 'Vite', 'Responsive'],
        image:
        'data:image/png;base64,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',
        repo: 'https://github.com/motheo-365/ticket-viewer'
    }
    ];
</script>

<style scoped>
    .projects {
        padding: 1.5rem 0;
    }

    .section-title {
        font-size: 5rem;
        margin: 0 0 1rem;
        text-align: center;
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
        background: var(--card-bg);
        color: var(--card-text);
    }

    .thumb {
        display: block;
        width: 95%;
        aspect-ratio: 16 / 9;
        overflow: hidden;
        text-align: center;
    }

    .thumb img {
        width: 90%;
        height: 90%;
        object-fit: cover;
        transition: transform 200ms ease;
        display: block;
    }

    .thumb:hover img { transform: scale(1.06); }

    .card-body {
        display: flex;
        flex-direction: column;
        gap: 0.75rem;
        padding: 0.9rem;
        min-height: 25%;
    }

    .card-title {
        margin: 0 0 0.25rem;
        font-size: 1.05rem;
        display: -webkit-box;
        -webkit-box-orient: vertical;
        overflow: hidden;
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
        white-space: nowrap;
    }

    .actions {
        display: flex;
        gap: 0.5rem;
        margin-top: auto;
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
        background: #9A6B7D;
        color: white;
    }

    .btn-primary:hover { background: #7f5867;}

    .btn-ghost {
        background: #9A6B7D;
        color: #ffffff;
    }

    .btn-ghost:hover {
        background: #7f5867;
    }
</style>