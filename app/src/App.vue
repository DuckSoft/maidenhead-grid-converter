<template>
  <div id="app">
    <mu-appbar style="width: 100%;" color="primary" title="Maidenhead Grid Converter">
    </mu-appbar>

    <mu-container>
      <PageGridConv></PageGridConv>
    </mu-container>
  </div>
</template>

<script>
  import PageGridConv from "./components/PageGridConv";
  export default {
    name: 'App',
    components: {PageGridConv},
    data() {
      return {
        active_tab: 0,
      }
    }
  }
</script>

<style>

</style>
