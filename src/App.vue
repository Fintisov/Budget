<template>
  <FormItem @submit-form="addNewFiledToList"/>
  <TotalBalance :total='totalBalance'/>
  <BudgetList :list='list' @delete-item="onDeleteListItem"/>
</template>

<script>
import BudgetList from "@/components/BudgetList.vue";
import TotalBalance from "@/components/TotalBalance.vue";
import FormItem from "@/components/FormItem.vue";

export default {
  name: 'App',
  components: {
    BudgetList,
    TotalBalance,
    FormItem,
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
    },
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
  },
  methods: ({
    onDeleteListItem(value) {
      delete this.list[value]
    },

    addNewFiledToList(dataForm) {
      const MAX_NUMBER_ID = 10;
      const createId = () => Math.floor(Math.random() * MAX_NUMBER_ID);
      let newId = createId();
      const idList = Object.keys(this.list);

      console.log(dataForm)

      // Check max length
      if (idList.length >= MAX_NUMBER_ID) {
        alert('max length');
        return;
      }

      // Check free id in the list
      while (idList.includes(`${newId}`)) {
        newId = createId();
      }

      this.list[newId] = {
        ...dataForm,
        id: newId
      };
    }
  })
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
