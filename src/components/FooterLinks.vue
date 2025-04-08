<template>
  <footer class="footer">
    <div class="footer__container">
      <div class="footer__nav">
        <div class="nav-item active">Home</div>
        <div class="nav-item">About</div>
        <div class="nav-item">Contact</div>
      </div>
    </div>
  </footer>
</template>

<script setup>
// Footer component logic can go here

</script>

<style>
.footer {
  width: 100%;
  background-color: #212454;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 0;
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
}

.footer__container {
  width: 100%;
  display: flex;
  justify-content: center;
}

.footer__nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-item {
  padding: 15px 30px;
  color: white;
  font-weight: 500;
  cursor: pointer;
}

.nav-item.active {
  background-color: #e26575;
}

/* For proper spacing between items */
.footer__nav .nav-item:not(:last-child) {
  margin-right: 0;
}
</style>