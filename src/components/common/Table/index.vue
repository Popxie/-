<template>
  <el-table
    v-loading="loading"
    :empty-text="emptyText"
    :border="border"
    :data="dataList"
    :stripe="stripe"
    :row-class-name="rowClassName"
    :default-sort="defaultSort"
    @selection-change="selectionChange"
    @select-all="selectAllClick"
    @select="singleSelectClick"
    @sort-change="sortChange">
    <el-table-column
      v-if="isCheckBox"
      type="selection"
      width="55" />
    <template v-for="(col,index) in columns">
      <el-table-column
        v-if="col.slot"
        :key="`${col.prop}_${index}`"
        :show-overflow-tooltip="col.isShowOverTooltip"
        :width="col.width ? col.width : undefined"
        :render-header="col.renderHeader"
        :min-width="col.minWidth"
        :sortable="col.sortable"
        :label="col.label"
        :fixed="col.fixed"
        :align="col.align"
        :prop="col.prop">
        <template slot-scope="scope">
          <!-- 若果col.prop为链式的属性即 xxx.yyy的话 那么row['xxx.yyy']是获取不到对应的值的，此时应该用row -->
          <slot
            :slotValue="scope.row[col.prop]"
            :rowIndex="scope.$index"
            :filters="col.filters"
            :row="scope.row"
            :name="col.slot" />
        </template>
      </el-table-column>
      <el-table-column
        v-else
        :key="index"
        :show-overflow-tooltip="col.isShowOverTooltip"
        :width="col.width ? col.width : undefined"
        :render-header="col.renderHeader"
        :min-width="col.minWidth"
        :sortable="col.sortable"
        :fixed="col.fixed"
        :label="col.label"
        :align="col.align"
        :prop="col.prop" />
    </template>
  </el-table>
</template>

<script>
/**
 * 抛出事件和属性原则： 保持element原有特色
 * @param {Array} columns 数组项说明：
 * @param {String} label 表格头文案 与 element所需参数保持一致
 * @param {String} prop <String>：单元格字段 与 element所需参数保持一致
 * @param {String} slot <String>：插槽名称（可选）。需特殊处理的单元格，设置单独的slot
 * @param {Array} filters 过滤器名称（可选）。支持级联filter
 */

export default {
  name: 'KaDaTable',
  props: {
    defaultSort: {
      type: Object,
      default: () => {}
    },
    stripe: {
      type: Boolean,
      default: false
    },
    isShowOverTooltip: {
      type: Boolean,
      default: false
    },
    dataList: { // 表格数据
      type: Array,
      default: () => []
    },
    columns: { // 表格列配置
      type: Array,
      default: () => []
    },
    emptyText: { // 没有数据提示文案
      type: String,
      default: '暂无数据.'
    },
    headerCellStyle: { // 头部样式 暂未开启
      type: Object,
      default: function() {
        return {
          background: '#f7f8fb',
          color: '#333'
        }
      }
    },
    isCheckBox: {
      type: Boolean,
      default: false
    },
    border: {
      type: Boolean,
      default: false
    },
    loading: {
      type: Boolean,
      default: false
    },
    rowClassName: {
      type: [String, Function],
      default: null
    }
  },
  data() {
    return {}
  },
  methods: {
    /**
     * @param {Array} selection 选中行的对象集合
     * 向外抛出原有的事件名
     * select单选change事件
     */
    selectionChange(selection) {
      this.$emit('selection-change', selection)
    },
    /**
     * @param {type}
     * 向外抛出原有的事件名
     * select全选change事件
     */
    selectAllClick(selection) {
      this.$emit('select-all', selection)
    },
    /**
     * @param {Array} selection 选中行的对象集合
     * @param {Object} 点击的当前行的数据
     * 向外抛出原有的事件名
     */
    singleSelectClick(selection, row) {
      this.$emit('select', selection, row)
    },
    // 当表格的排序条件发生变化的时候会触发该事件
    sortChange({ column, prop, order }) {
      this.$emit('sort-change', column, prop, order)
    }
  }
}
</script>
