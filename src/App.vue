<template>
  <WheatherApp/>
</template>

<script>
import WheatherApp from './components/WheatherApp.vue';

export default {
  name: 'App',
  components: {
    WheatherApp,
  },
};
</script>

<style lang="scss">
#app {
  font-family: 'Rubik';
  font-style: normal;
  font-weight: 400;
  font-size: 18px;
  line-height: 20px;
  color: #7E7E7E;
}
</style>
