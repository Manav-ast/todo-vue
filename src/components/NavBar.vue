<template>
  <nav class="navbar">
    <div class="navbar__logo">
      <router-link to="/">ToDo - Vue</router-link>
    </div>
    <ul class="navbar__links">
      <!-- <li><router-link to="/">Logout</router-link></li> -->
      <button class="button">Logout</button>
    </ul>
  </nav>
</template>

<script setup>
// No script content needed
</script>

<style>
  .navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem;
    background-color: #212454;
    /* border-bottom: 1px solid #ddd; */
    width: 100vw; /* Use viewport width */
    position: fixed; /* Fix it to the top */
    top: 0;
    left: 0;
    right: 0;
    z-index: 1000; /* Ensure it stays on top of other content */
    box-sizing: border-box; /* Include padding in width calculation */
  }

  .navbar__logo {
    font-size: 1.5rem;
    font-weight: bold;
    color: white;
  }

  .navbar__links {
    display: flex;
    gap: 1rem;
    list-style: none;
    margin: 0;
    padding: 0;
  }

  .button {
    cursor: pointer;
    text-decoration: none;
    color: white;
    background-color: red;
    padding: 5px 10px 5px 10px;
    border-radius: 15px;
    border: transparent;
  }

  .button:hover {
    background-color: black;
  }
</style>