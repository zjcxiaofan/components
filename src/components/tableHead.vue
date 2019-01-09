<template>
  <div class="hello">
    <el-checkbox v-for="i in data" v-model="i.show" :key="i.name">{{i.label}}</el-checkbox>
    <el-button @click="changeTb()">确定</el-button>
    <el-table :data="data1">
      <el-table-column prop="name" label="姓名" width="180" v-if="data2[0]"></el-table-column>
      <el-table-column prop="age" label="年龄" width="180" v-if="data2[1]"></el-table-column>
      <el-table-column prop="height" label="身高" v-if="data2[2]"></el-table-column>
      <el-table-column prop="weight" label="体重" v-if="data2[3]"></el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  name: 'tableHead',
  data() {
    return {
      data: [{ label: '姓名', show: true }, { label: '年龄', show: true }, { label: '身高', show: true }, { label: '体重', show: true }], //开始选中的表头
      data2: [], //对话框表头
      data1: [{ name: '张三', age: 17, height: 175, weight: 130 }, { name: '李四', age: 18, height: 185, weight: 150 }]
    }
  },

  methods: {
    changeTb() {
      this.data2 = []
      for (var i = 0; i < this.data.length; i++) {
        this.data2.push(this.data[i].show)
      }
    }
  },
  created() {
    for (var i = 0; i < this.data.length; i++) {
      this.data2.push(this.data[i].show)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
</style>
