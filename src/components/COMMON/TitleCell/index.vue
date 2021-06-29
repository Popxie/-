<!--
 * @Description: title组件
 * @Author: xiehuaqiang
 * @FilePath: /kdadmin-fe/src/components/common/TitleCell/index.vue
 * @Date: 2021-05-20 09:58:34
-->

<template>
  <div 
    :class="{'header-margin': isHeader, 'set-pading': isSetPadding }"
    class="common-title-cont">
    <div :class="{ 'is-header': isHeader }">
      {{ title }}       
    </div>
    <div class="btn-cont">
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  name: 'TitleCell',
  props: {
    title: {
      type: String,
      default: ''
    },
    isHeader: {
      type: Boolean,
      defalut: false
    },
    isSetPadding: {
      type: Boolean,
      defalut: false
    }
  }
}
</script>
<style lang="scss" scope>
  .common-title-cont {
    height: 55px;
    line-height: 55px;
    border-bottom: 1px solid #e9e9e9;
    display: flex;
    justify-content: space-between;
    background: #ffffff;
    font-size: 18px;
    font-weight: 400;
    margin-bottom: 10px;
    .is-header {
      font-weight: 600;
      padding: 0 15px;
    }
  }
  .header-margin {
    margin-bottom: 10px;
  }
  .set-pading {
    padding: 0 15px;
  }
</style>