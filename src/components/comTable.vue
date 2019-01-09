<template>
  <div class="com-tab">
    <el-table ref="multipleTable" style="width: 100%" v-loading="options.listLoading" :element-loading-text="options.text" :data="list" :stripe="options.stripe" tooltip-effect="dark" :border="options.border">
      <!-- 选择列 -->
      <el-table-column v-if="options.select" type="selection" width="75"></el-table-column>

      <!-- 序号列 -->
      <el-table-column v-if="options.index" type="index" :index="indexMethod" label="序号" width="75"></el-table-column>

      <!-- 数据列 -->
      <template v-for="(column) in columns">
        <el-table-column :prop="column.prop" :label="column.label" :align="column.align || 'center'" :width="column.width" :fixed="column.fixed" :key="column.prop" :show-overflow-tooltip="column.tooltip">
          <template slot-scope="scope">
            <!-- 没有formatter时正常显示-->
            <template v-if="!column.formatter">{{scope.row[column.prop]}}</template>
            <!-- 返归需要展示的标签-->
            <template v-else>
              <span v-html="column.formatter(scope.row,scope.$index)"></span>
            </template>
            <!-- switch按钮组  switch为true显示  -->
            <template v-if="column.switch">
              <div>
                <el-switch v-model="scope.row[column.value]" :active-text="column.active" :inactive-text="column.inactive" @change="column.operate(scope.row,scope.$index)"></el-switch>
              </div>
            </template>
            <!-- button按钮组 button为true显示-->
            <template v-if="column.button">
              <template v-for="(btn, i) in column.group">
                <el-button :key="i" :type="btn.type" :size="btn.size || 'mini'" :icon="btn.icon" :disabled="btn.disabled" :plain="btn.plain" @click.stop="btn.operate(scope.row, scope.$index)">{{btn.name}}</el-button>
              </template>
            </template>
          </template>
        </el-table-column>
        <!-- 表内按钮操作组-->
      </template>
    </el-table>
  </div>
</template>

<script>
export default {
  props: {
    list: {
      type: Array,
      default: () => []
    },
    columns: {
      type: Array,
      default: () => []
    },
    options: {
      type: Object,
      default: {}
    }
  },
  name: 'comTable',
  data() {
    return {}
  },

  methods: {
    indexMethod(index) {
      return this.pageRows * (this.pageNum - 1) + index + 1
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
</style>
