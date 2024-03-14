<template>
  <p>Total balance: <b>{{total}}</b> </p>
</template>

<script>
export default {
  name: "TotalBalance",
  props: {
    total: {
      type: Number,
      default: 0
    }
  }
}
</script>

<style scoped>

</style>