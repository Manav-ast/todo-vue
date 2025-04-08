<template>
  <div class="bg-[#FAFBEA] min-h-screen flex items-center justify-center p-4">
    <div class="bg-white rounded-lg shadow-md overflow-hidden max-w-4xl w-full">
      <img
        src="@/assets/about-image.png"
        alt="About"
        class="w-full h-auto object-cover"
      />
      <div class="p-6 text-lg text-gray-800 leading-relaxed">
        This Simple Todo App is created using <strong>Nuxt 3</strong> and uses <strong>Supabase</strong> for storing and authentication.
        With this app you can create, update or delete todo. You can also mark todo as completed if it’s done. You can also
        filter your todo based on completed, all and remaining. For state management tool used <strong>Pinia</strong>.
      </div>
    </div>
  </div>
</template>

<script setup>
// No script logic needed for this simple static About component
</script>

<style scoped>
/* Optional custom styling if needed */
</style>
