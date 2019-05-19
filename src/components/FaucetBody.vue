<template>
  <div id="faucet-body">
    <slot name="faucet"></slot>
  </div>
</template>

<script>
export default {
  data() {
    return {
      account: null
    }
  },
  methods: {

  }
}
</script>

<style>
#faucet-body {
  margin-left: 10%;
  margin-right: 10%;
  margin-bottom: 6%;
}
</style>
