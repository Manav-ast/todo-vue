<script setup>
import NavBar from './components/NavBar.vue';
import FooterLinks from './components/FooterLinks.vue';
import HomeView from './components/pages/HomeView.vue';
</script>

<template>
  <div class="app-container">
    <NavBar />
    <main>
      <HomeView />
    </main>
    <FooterLinks />
  </div>
</template>

<style>
  /* Reset some default browser styling */
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body, html {
    height: 100%;
    width: 100%;
    margin: 0;
    padding: 0;
    background-color: whitesmoke;
  }

  .app-container {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
    width: 100%;
  }

  main {
    flex: 1;
    margin-top: 70px;
    padding: 1rem;
    width: 70vw;
  }
</style>