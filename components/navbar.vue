<!-- u24666981 Motheo Morena -->

<template>
  <nav class="navbar">
    <div class="container">
      <ul class="nav-links">
        <li><a href="#home">Home</a></li>
        <li><a href="#projects">Projects</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
    </div>
  </nav>
</template>

<style scoped>
    /* Navbar container */
    .navbar {
        width: 90%;
        padding: 0.3%;
        background-color: #FFFFFF;
        position: fixed;           
        top: 1%;                 /* small space from top */
        left: 50%;
        transform: translateX(-50%); /* center the navbar container */
        border-radius: 5px;
        z-index: 1000;
        box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }

    /* Inner container to center content */
    .navbar .container {
        max-width: 1200px;
        margin: 0 auto;
        padding: 1rem 2rem;
        display: flex;
        justify-content: center;  /* center links horizontally */
        align-items: center;      /* center links vertically */
    }

    /* Navbar list */
    .nav-links {
        list-style: none;
        display: flex;
        gap: 3rem;               /* space between links */
        padding: 0;
        margin: 0;
    }

    /* Links style */
    .nav-links li a {
        color: #000000;
        text-decoration: none;
        font-weight: 500;
        font-size: 2rem;
        transition: color 0.3s ease;
    }

    /* Hover effect */
    .nav-links li a:hover {
        color: #9A6B7D;
    }
</style>