<template>
  <main class="container">
    <AppHeader />
    <section class="layout">
      <AppAside />
      <AppBody />
    </section>
  </main>
</template>

<script>
import AppAside from "@/components/app-aside";
import AppBody from "@/components/app-body";
import AppHeader from "@/components/app-header";

export default {
  components: { AppHeader, AppAside, AppBody },
};
</script>

<style scoped>
.layout {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
}
</style>
