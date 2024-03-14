<template>
  <div class="budget-list-wrapper">
    <el-card :header="header">
      <template v-if="isEmptyList">
        <el-alert
            title="This list is empty"
            type="info"
            center
            show-icon
            :closable="elAlert.closable"
        />
      </template>
      <template v-else>
        <ul class="budget-list">
          <li class="budget-list__item"
              v-for="(item, index) in list" :key="index"
          >
            <p class="budget-list__text">{{ item.comment }} <b>{{ item.value }}</b></p>
            {{ isEmptyList }}
            <el-button type="danger" plain>Delete</el-button>
          </li>
        </ul>
      </template>
    </el-card>
  </div>

</template>

<script>
export default {
  name: "BudgetList",
  props: {
    list: {
      type: Object,
      default: () => ({})
    }
  },
  data: () => ({
    header: 'Budget header',
  }),
  setup: () => ({
    elAlert: {
      closable: false
    }
  }),
  computed: {
    isEmptyList() {
      return !Object.keys(this.list).length
    }
  }
}
</script>

<style scoped>
.budget-list-wrapper {
  max-width: 500px;
  margin: 0 auto;

  .budget-list__item {
    display: flex;
    align-items: center;
    gap: 10px;

    &:not(:last-of-type) {
      margin-bottom: 10px;
    }
  }

  .budget-list__text {
    display: flex;
    width: 100%;
    justify-content: space-between;
  }
}
</style>;