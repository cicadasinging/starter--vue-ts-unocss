<script lang="ts" setup>
defineProps<{ msg: string }>();
</script>

<template>
  <div class="text-center" lg="text-left">
    <h1 class="green font-medium text-5xl leading-normal -top-10px">{{ msg }}</h1>
    <h3 class="text-xl leading-normal">
      You’ve successfully created a project with
      <a href="https://vitejs.dev/" rel="noopener" target="_blank">Vite</a> +
      <a href="https://vuejs.org/" rel="noopener" target="_blank">Vue 3</a>. What's next?
    </h3>
  </div>
</template>
