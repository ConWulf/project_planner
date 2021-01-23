<template>
  <teleport to=".main-nav">
      <router-link :to="{name: 'Home'}">PROJECTS</router-link>
      <router-link :to="{name: 'AddProject'}">ADD A PROJECT</router-link>
  </teleport>
</template>

<script>
export default {
  name: "Navbar"
}
</script>
