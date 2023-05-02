<template>
  <div>
    <router-view v-slot="{ Component }">
      <transition name="fade" mode="out-in">
        <div>
          <component :is="Component" />
        </div>
      </transition>
    </router-view>
  </div>
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
.fade-enter-active {
  transition: all 0.8s ease-in-out;
}

.fade-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}

.fade-enter-from,
.fade-leave-to {
  transform: translateX(20px);
  opacity: 0;
}
</style>