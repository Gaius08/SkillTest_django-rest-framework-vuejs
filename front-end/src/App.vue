<template>
  <transition name="fade" mode="out-in">
    <router-view v-slot="{ Component }">
      <component :is="Component" />
    </router-view>
  </transition>
</template>
<script>
export default {
  mounted() {
    const token = localStorage.getItem("token");
    if (token) {
      // Redirect to home page
      this.$router.push("/help");
    } else {
      // Redirect to login page
      this.$router.push("/login");
    }
  },
};
</script>
<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>