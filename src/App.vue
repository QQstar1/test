<template>
  <div id="app">
    <div>
      <span class="content">请输入一个数组，数组元素之间以逗号分隔</span>
      <input class="input" v-model="obj">
    </div>
    <button class="btn" @click="countPoint">按钮</button>
    <div>平衡位：{{balancePoint}}</div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      obj: '',
      balancePoint: null
    }
  },
  methods: {
    countPoint () {
      this.balancePoint = null
      let arr = []
      let sumRight = null
      let sumLeft = null
      arr = JSON.parse(`[${this.obj}]`)
      if (arr.length > 2) {
        arr.forEach(i => {
          sumRight += i
        })
        for (let [ index, value ] of new Map(arr.map((value, index) => [ index, value ]))) {
          sumRight -= value
          if (sumLeft === sumRight) {
            this.balancePoint = index
            return
          } else {
            sumLeft += value
          }
        }
      } else {
        this.balancePoint = -1
      }
      this.balancePoint = this.balancePoint ? this.balancePoint : -1
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.content {
  margin-right: 50px;
}
.input {
  padding: 5px;
  width: 300px;
  font-size: 16px;
  line-height: 18px;
  border: 1px solid #bbb;
  border-radius: 5px;
}
.btn {
  margin-top: 50px;
  width: 80px;
  height: 40px;
  background: #fff;
  border: 1px solid #bbb;
  border-radius: 5px;
  font-size: 20px;
  cursor: pointer;
  outline: none;
}
.btn:hover {
  background: #f0f0f0;
}
.btn:active {
  background: #ddd;
}
</style>
