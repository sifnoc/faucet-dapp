<template>
  <div>
    <h3>transactions</h3>
    <p v-for="(transaction, index) in transactions" v-bind:key="index">
      {{ transaction }}
    </p>
  </div>
</template>

<script>
export default {
  props: ['transactions']
}
</script>

<style>

</style>
