<script>
import AppHeader from './components/AppHeader.vue';
import AppMain from './pages/ProjectList.vue';

export default {
  components: {
    AppMain,
    AppHeader
  }
}
</script>

<template>
  <div>
    <AppHeader />
    <router-view/>
  </div>
</template>

<style lang="scss">
  @use './styles/generals.scss' as *;
</style>
