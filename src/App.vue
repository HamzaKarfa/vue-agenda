<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import Button from 'primevue/button'
import Avatar from 'primevue/avatar'
</script>

<template>
  <header class="flex align-items-center justify-content-around w-full">
    <Button severity="primary" outlined class="p-2">
      <span class="pi pi-angle-left" style="font-size: 1.5rem; color: blue"></span>
    </Button>
    <RouterLink to="/">
      <img src="./assets/logo-min.png" />
    </RouterLink>
    <RouterLink to="/profile">
      <div class="flex flex-column align-items-center justify-content-center">
        <Avatar icon="pi pi-user" class="m-0" size="xlarge" shape="circle" />
        <p class="m-0">Jhon</p>
        <p class="m-0">Developer</p>
      </div>
    </RouterLink>
  </header>

  <RouterView />
</template>

<style scoped lang="scss">
header {
  img {
    width: 75px;
    border-radius: 50%;
    border: solid 1px black;
  }
}
</style>
