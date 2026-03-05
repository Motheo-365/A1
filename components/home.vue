<!-- u24666981 MOtheo Morena -->
<script setup>
  import Nav from './navbar.vue'
  import Weather from './weather.vue'
</script>

<template>
  <section id = "home">
    <!-- Loading Screen -->
    <div v-if="loading" class="loading-screen">
      <div class="loader"> <em> Loading... </em></div>
    </div>

    <div v-else >
      <Nav class = "navbar" />

      <div class = "api">
        <Weather/>
      </div>

      <div class="container">
        <!-- Image -->
          <NuxtImg 
            src="/media/motheo.jpeg" 
            alt="An image of me, Motheo Morena." 
            class="img" 
          />

          <!-- Text box -->
          <div class="text-box">
            <h1 id="name">MOTHEO MORENA</h1>
            <p class="info-me">
              A Multimedia student at the University of Pretoria. <br/>
              I specialise in front-end web development, animation, and creative storytelling, blending code with creativity to bring ideas to life. <br/>
              Whether it’s a website, interactive project or visual concept, I love turning imagination into reality.
            </p>

            <!--
              <div class = "links">
                <a href = "#projects"> Projects </a>
                <a href = "#contact"> Contact </a>
              </div>
            -->
          </div>
      </div>


      
    </div>
  </section>
</template>

<style scoped>
    .loading-screen {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: black;
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 9999;
    }

    .img {
      max-width: 30%;
      border-radius: 8px;
      border: 5px solid #ffffff;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
      object-fit: cover;
    }

    .container {
      width: 90vw;
      max-width: 1200px;
      border: 2px solid #ffffff;
      display: flex;
      flex-direction: row; /* image left, text right */
      gap: 2rem;
      margin: 10rem auto 2rem auto;
      justify-content: flex-start;
      align-items: center;
      padding: 2rem;
      border-radius: 1rem;
      background-color: rgba(0, 0, 0, 0.6);
      box-shadow: 0 0 15px rgba(0, 0, 0, 0.3);
    }

    .text-box {
      display: flex;
      flex-direction: column;
      flex: 1; /* fills remaining space */
      justify-content: center;
      gap: 1.5rem;
    }

    #name {
      font-size: 10em;
      font-weight: bold;
      color: white;
      margin: 0 auto;
    }

    .info-me {
      color: white;
      text-align: left;
      font-size: 1.2em;
      line-height: 1.6;
    }

    .api {
      position: relative;
      color: white;
      max-width: 85%;
      transform: translate(7%, 50%);
      border: 1px solid white;
      border-radius: 8px;
      padding: 1.2%;
    }

    /*
    .links {
      transform: translateX(25%);
    }

    .links a {
      color: orange;
      font-size: 1.4rem;
      margin: 0.2%;
      padding: 5%;
    }
      */
</style>