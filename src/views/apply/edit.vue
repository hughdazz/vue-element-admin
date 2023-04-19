<template>
  <div class="createPost-container">
    <el-form ref="postForm" :model="postForm" :rules="rules" class="form-container">
      <sticky :z-index="10">
        <el-button v-loading="loading" style="margin-left: 10px;" type="success" @click="submitForm">
          Publish
        </el-button>
      </sticky>
    </el-form>
  </div>
</template>

<script>
export default {
  name: 'EditApply',
  data() {
    return {
      list: null,
      listLoading: false,
      tableKey: 0, // 表格的key, 用于重置表格
      showSubmiter: false
    }
  }
}
</script>

<style lang="scss" scoped>
@import "~@/styles/mixin.scss";
</style>
