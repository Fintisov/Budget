<template>
  <el-card class="card-form">
    <el-form
        :model="formData"
        :rules="rules"
        ref="formRef"
        label-position="top"
    >
      <el-form-item label="Type" prop="type">
        <el-select
            v-model="formData.type"
            placeholder="please select type"
        >
          <el-option label="INCOME" value="income"/>
          <el-option label="OUTCOME" value="outcome"/>
        </el-select>
      </el-form-item>

      <el-form-item label="Comment" prop="comment">
        <el-input v-model="formData.comment"/>
      </el-form-item>

      <el-form-item label="Value" prop="value">
        <el-input v-model.number="formData.value"/>
      </el-form-item>

      <el-form-item>
        <el-button type="primary" @click="onSubmit">Add</el-button>
        <el-button @click="resetForm">Reset</el-button>
      </el-form-item>
    </el-form>
  </el-card>
</template>

<script>
export default {
  name: 'FormItem',
  emits: ['submitForm'],
  data: () => ({
    formData: {
      type: 'income',
      comment: '',
      value: 0,
    },
    rules: {
      type: [{required: true, message: 'Please select type', trigger: 'blur'}],
      comment: [{required: true, message: 'Please input comment', trigger: 'change'}],
      value: [
        {required: true, message: 'Please input comment', trigger: 'change'},
        {type: 'number', message: 'Type in the input must be number', trigger: 'change'},
      ],
    },
  }),
  methods: ({
    async onSubmit() {
      const form = this.$refs.formRef;

      await form.validate((isValid, fields) => {
        if (isValid) {
          const getTypeValue = this.formData.type.toLowerCase();

          switch (getTypeValue) {
            case 'income':
              this.formData.value = Math.abs(this.formData.value);
              break;
            case 'outcome':
              this.formData.value = this.formData.value * -1;
              break;
          }

          this.$emit('submitForm', {...this.formData});
          form.resetFields();

        } else {
          console.log('Error: ', fields);
        }
      });
    },
    resetForm() {
      this.$refs.formRef.resetFields();
    },
  }),
};
</script>

<style scoped>
.card-form {
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
}
</style>
