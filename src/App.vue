<template>
  <div id="app">
    <NightSwitch />
    <router-view />
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
  </div>
</template>

<script>
import NightSwitch from "@/components/NightSwitch.vue";

export default {
  components: {
    NightSwitch
  }
};
</script>

<style lang="scss"></style>
