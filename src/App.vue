<template>
  <div id="app">
    <!-- <HelloWorld/> -->
    <!-- <tableHead/> -->
    <com-table :list="list" :options="options" :columns="columns"></com-table>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import tableHead from './components/tableHead'
import comTable from './components/comTable'

export default {
  name: 'App',
  components: {
    HelloWorld,
    tableHead,
    comTable
  },
  data() {
    return {
      options: {
        text: '正在加载数据...',
        stripe: true, // 是否为斑马纹 table
        listLoading: false, // 是否添加表格loading加载动画
        highlightCurrentRow: true, // 是否支持当前行高亮显示
        mutiSelect: false, // 是否支持列表项选中功能
        border: false, // 是否带有纵向边框
        select: false,
        index: false
      },
      list: [
        { name: '11', age: '18', height: '175', weight: '130', btn: false },
        { name: '22', age: '19', height: '175', weight: '130', btn: true },
        { name: '33', age: '20', height: '175', weight: '130', btn: false },
        { name: '44', age: '21', height: '175', weight: '130', btn: true },
        { name: '55', age: '22', height: '175', weight: '130', btn: false }
      ],
      columns: [
        {
          prop: 'name',
          label: '姓名'
        },
        {
          prop: 'age',
          label: '年龄'
        },
        {
          prop: 'height',
          label: '身高'
        },
        {
          prop: 'weight',
          label: '体重'
        },
        {
          prop: 'btn',
          label: '状态',
          formatter: row => {
            if (row.btn) {
              return '<span>开启</span>'
            } else {
              return '<span>关闭</span>'
            }
          }
        },
        {
          value: 'btn',
          label: '设置',
          switch: true,
          operate: (row, i) => {
            console.log(row)
            // 发送请求改变状态
          }
        },
        {
          button: true,
          label: '按钮',
          group: [
            {
              type: 'success',
              name: '新增',
              operate: (row, i) => {
                console.log('新增')
              }
            },
            {
              type: 'danger',
              name: '删除',
              operate: (row, i) => {
                console.log('删除')
              }
            }
          ]
        }
      ]
    }
  }
}
</script>

<style>
</style>
