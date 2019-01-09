<template>
  <div class="hello">
    <el-checkbox v-model="checked">全选</el-checkbox>
    <el-checkbox v-model="checked2" @change="fanxuan()">反选</el-checkbox>
    <el-tree :data="data2" show-checkbox default-expand-all node-key="id" ref="tree" highlight-current :props="defaultProps"></el-tree>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      checked: '',
      checked2: '',
      data2: [
        {
          id: 1,
          label: '一级 1',
          children: [
            {
              id: 4,
              label: '二级 1-1',
              children: [
                {
                  id: 9,
                  label: '三级 1-1-1'
                },
                {
                  id: 10,
                  label: '三级 1-1-2'
                }
              ]
            }
          ]
        },
        {
          id: 2,
          label: '一级 2',
          children: [
            {
              id: 5,
              label: '二级 2-1'
            },
            {
              id: 6,
              label: '二级 2-2'
            }
          ]
        },
        {
          id: 3,
          label: '一级 3',
          children: [
            {
              id: 7,
              label: '二级 3-1'
            },
            {
              id: 8,
              label: '二级 3-2'
            }
          ]
        }
      ],
      defaultProps: {
        children: 'children',
        label: 'label'
      },
      arrId: []
    }
  },
  methods: {
    fanxuan() {
      this.arrId = []
      this.findId(this.data2)
      var list1 = this.$refs.tree.getCheckedKeys()
      var list2 = this.$refs.tree.getHalfCheckedKeys()
      var list = list1.concat(list2)
      console.log(list1, list2, list)
      for (let i = 0; i < list.length; i++) {
        let index = this.arrId.indexOf(list[i])
        if (index > -1) {
          this.arrId.splice(index, 1)
        }
      }
      console.log(this.arrId)
      this.$refs.tree.setCheckedKeys([])
      this.$refs.tree.setCheckedKeys(this.arrId)
    },
    spliceId() {
      for (var i = 0; i < list.length; i++) {
        console.log(this.arrId)
        if (this.arrId.indexOf(list[i])) {
          this.arrId.splice(i, 1)
        }
      }
    },
    findId(data) {
      var obj = data
      for (var key of obj) {
        if (key.id) {
          this.arrId.push(key.id)
        }
        if (key.hasOwnProperty('children') && key.children.length) {
          this.findId(key.children)
        }
      }
    },
    getCheckedNodes() {
      console.log(this.$refs.tree.getCheckedNodes())
    },
    getCheckedKeys() {
      console.log(this.$refs.tree.getCheckedKeys())
    },
    setCheckedNodes() {
      this.$refs.tree.setCheckedNodes([
        {
          id: 5,
          label: '二级 2-1'
        },
        {
          id: 9,
          label: '三级 1-1-1'
        }
      ])
    },
    setCheckedKeys() {
      this.$refs.tree.setCheckedKeys([3])
    },
    resetChecked() {
      this.$refs.tree.setCheckedKeys([])
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
</style>
