<template>
  <div id="app">
    <mu-container>
      <mu-form :model="form">
        <mu-form-item>
          <mu-button color="primary" @click="calculate">Calculate</mu-button>
        </mu-form-item>
      </mu-form>
    </mu-container>
  </div>
</template>

<script>
  export default {
    name: 'App',
    data() {
      return {
        form: {}
      }
    },
    methods: {
      calculate() {
        this.$toast.message("hello world")
      }
    }
  }
</script>

<style>

</style>
