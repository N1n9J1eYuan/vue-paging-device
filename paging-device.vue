<template>
  <ul class="hello">
    <li @click='goto'>上一页</li> <!-- 上一页 -->
    <li v-for='n in pages' :key='n' :class="{active: n===current }">{{n}}</li> <!-- 分页 -->
    <li @click='goto("+")'>下一页</li><!-- 下一页 -->
  </ul>
</template>
<script>
export default {
  name: 'hello',
  data () {
    return {
      current: 1, // 当前
      allPage: 13, // 所有的页数
      showItem: 5 // 显示几个页码
    }
  },
  computed: {
    pages () {
      let page = []
      // 当前页码 小于 每次显示页码的个数
      if (this.current < this.showItem) {
        var i = Math.min(this.showItem, this.allPage)
        while (i) {
          page.unshift(i--) // 54321
        }
      } else {
        let middle = this.current - Math.floor(this.showItem / 2)
        let i = this.showItem
        if (middle > (this.allPage - this.showItem)) {
          middle = this.allPage - this.showItem + 1
        }
        while (i--) {
          page.push(middle++)
        }
      }
      return page
    }
  },
  methods: {
    goto (val) {
      // 点击加号
      if (val === '+') {
        if (this.current < this.allPage) this.current++
      } else {
        // 点击减号
        if (this.current > 1) this.current--
      }
    }
  }
}
</script>
<style scoped>
  h1, h2 {
    font-weight: normal;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
    border: 1px solid #ccc;
    cursor: pointer;
    padding: .05rem .1rem;
  }

  a {
    color: #42b983;
  }
  .active{
    background-color: #999;
    color: #fff; 
  }
</style>