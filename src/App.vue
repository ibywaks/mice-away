<script setup lang="ts">
import { RouterLink, RouterView } from "vue-router";
// import HelloWorld from '@/components/HelloWorld.vue'
import MainHeader from '@/components/MainHeader.vue'
</script>

<template>
  <header>
    <MainHeader />
    <div class="sub-header">
      <h3 class="logo-tag">
        Powered by
        <img
          alt="Vue logo"
          class="logo"
          src="@/assets/logo.svg"
          width="40"
          height="40"
        />
      </h3>
    </div>
  </header>

  <RouterView />
</template>

<style>
@import "@/assets/base.css";
@import "../node_modules/bootstrap/dist/css/bootstrap.css";

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;

  font-weight: normal;
}

header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  /* display: block; */
  margin: 0 auto 2rem;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

@media (min-width: 1024px) {
  body {
    display: flex;
    place-items: center;
  }

  #app {
    padding: 0 2rem;
  }

  header {
    display: flex;
    padding-right: calc(var(--section-gap) / 2);
    padding-bottom: 40px;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  .sub-header {
    padding-top: 50px;
  }

  .logo {
    margin: 0 2rem 0 0;
  }
}
</style>
