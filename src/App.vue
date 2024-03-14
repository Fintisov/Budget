<template>
  <TotalBalance :total='totalBalance'/>
  <BudgetList :list='list'/>
</template>

<script>
import BudgetList from "@/components/BudgetList.vue";
import TotalBalance from "@/components/TotalBalance.vue";

export default {
  name: 'App',
  components: {
    BudgetList,
    TotalBalance
  },
  data: () => ({
    list: {
      1: {
        type: 'INCOME',
        value: 100,
        comment: 'Some comment',
        id: 1
      },
      2: {
        type: 'OUTCOME',
        value: -50,
        comment: 'Some outcome comment',
        id: 2
      }
    }
  }),

  computed: {
    totalBalance() {
      let total = 0;
      const valueList = Object.values(this.list);

      total = valueList.reduce((acc, item) => {
        return acc + item.value
      }, 0)

      return total
    }
  }
}
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

  ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }
}
</style>
