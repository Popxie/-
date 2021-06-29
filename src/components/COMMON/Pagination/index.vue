<template>
  <div
    v-show="total"
    class="pagination-cont">
    <el-pagination
      :current-page="currentPage"
      :page-sizes="[10, 15, 20, 25, 50, 100, 500]"
      :page-size="pageSize"
      :total="total"
      layout="total, sizes, prev, pager, next, jumper"
      background
      @current-change="handlePageChange"
      @size-change="handleSizeChange" />
  </div>
</template>

<script>
export default {
  name: 'KaDaPagination',
  props: {
    total: {
      type: Number,
      required: true
    },
    currentPage: {
      type: Number,
      default: 1
    },
    pageSize: {
      type: Number,
      default: 15
    }
  },
  methods: {
    handleSizeChange(pageSize) {
      this.$emit('size-change', pageSize)
    },
    handlePageChange(pageNum) {
      this.$emit('page-change', pageNum)
    }
  }
}
</script>

<style lang="scss" scoped>
.pagination-cont {
  display: flex;
  padding: 20px 20px 20px 0;
	background: #ffffff;
}
</style>
