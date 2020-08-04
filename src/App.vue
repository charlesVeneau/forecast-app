<template>
  <div id="app">
    <NightSwitch />
    <transition name="slideX-fade" mode="out-in">
      <router-view />
    </transition>
    <div id="nav">
      <router-link to="/">Accueil</router-link> |
      <router-link to="/about">A Propos</router-link>
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

<style lang="scss">


</style>
