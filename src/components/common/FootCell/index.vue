<!--
 * @Description: 提交表单底部的 提交 & 取消按钮组合
 * @Author: xiehuaqiang
 * @FilePath: /kdadmin-fe/src/components/common/FootCell/index.vue
 * @Date: 2021-05-19 18:36:53
-->
<template>
  <div
    id="foot-button-cell"
    class="foot-button-cell-cont">
    <el-button @click="cancelClick">
      取消
    </el-button>
    <el-button 
      type="primary"
      @click="submitClick">
      提交
    </el-button>
  </div>
</template>

<script>
export default {
  name: 'FootCell',
  methods: {
    submitClick() {
      this.$emit('submit-click')
    },
    cancelClick() {
      this.$router.go(-1)
      this.$emit('cancel-click')
    }
  }
}
</script>

<style lang='scss' scoped>
  .foot-button-cell-cont {
    display: flex;
    justify-content: flex-end;
    position: fixed;
    margin-left: -20px;
    bottom: 0;
    height: 56px;
    width: calc(100% - 180px); // 减去左边菜单栏的宽度
    padding-right: 20px;
    background: #ffffff;
    border-top: 1px solid #e9e9e9;
    z-index: 9999;
    .el-button {
      height: 30px;
      margin-top: 13px;
    }
  }
</style>