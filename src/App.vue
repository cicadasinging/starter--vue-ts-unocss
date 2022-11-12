<template>
  <header class="leading-normal max-h-screen" lg="flex place-items-center">
    <i class="flex-none block text-9xl mb-8 mx-auto" i-logos-vue lg="my-0 ml-0 mr-8" />
    <div lg="flex place-items-start flex-wrap">
      <HelloWorld msg="You did it!" />

      <nav class="w-full text-xs leading-normal text-center mt-8" lg="mt-4 -ml-4 py-4 text-base text-left">
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    padding-right: calc(var(--section-gap) / 2);
  }
}
</style>
