<template>
  <div id="app">
    <h1>封装滚动</h1>
    <!-- 在使用的时候定义元素的位置以及大小 -->
    <!-- 标签使用组件内部定义的名称 -->
    <scroll
      class="scroll"
      ref="scroll"
      scroll-width="400px"
      :scrollX="true"
    >
      <div class="banner">
        <h5 v-for="item in bannerSum" :key="item">{{ item }}</h5>
      </div>
      <p v-for="item in 50" :key="item">内容 --> {{ item }}</p>
    </scroll>
  </div>
</template>

<script>
// 将滚动进行封装成一个组件，进行引入
// * 在src中的文件使用相对路径，@符号表示src文件夹
import Scroll from "./components/scroll/scroll";
export default {
  data() {
    return {
      bannerSum: [],
    };
  },
  // 将进入的组件进行注册
  components: {
    // 使用组件内部的名称，在中括号内是表达式，先进行一次运算
    [Scroll.name]: Scroll,
  },
  // 模拟后台加载数据
  created(){
    setTimeout(() => {
      this.bannerSum = [1,2,3,4,5]
      // 在这里进行调用方法进行刷新滚动视图
      // this.$nextTick(() => {
      //   this.$refs.scroll.refresh()
      // })

    },2000)
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
.scroll {
  position: absolute;
  top: 20px;
  left: 0;
  right: 0;
  bottom: 20px;
  background-color: red;
}
p{
  width: 400px;
}
</style>
