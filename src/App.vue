<template>
  <MyMemos />
</template>

<script>
import MyMemos from '@/components/MyMemos'
export default {
  name: 'App',
  components: { MyMemos }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
  padding-left: 40px;
}
</style>
