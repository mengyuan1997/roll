<template>
<!-- 滚动视图，滚动视图的大小由外部决定 -->
<!-- 对滚动视图设置overflow -->
  <div class="scroll-view" ref="scroll">
      <!-- 滚动容器 并接受外部传输的宽度-->
      <div class="scroll-container" :style="{width:scrollWidth}">
          <!-- 滚动的内容由外部传递 -->
          <slot />
      </div>
    
  </div>
</template>

<script>
// 将组建进行引入
import IScroll  from './iscroll'
export default {
    // 在组件内部定义好名称，在外部使用
    name:"Scroll",
    // 接受外面的滚动设置并设置默认值
    props:{
        // 定义X轴
        scrollX:{
            type:Boolean,
            default:false
        },
        // 定义Y轴
        scrollY:{
            type:Boolean,
            default:true
        },
        // 定义X轴滚动的大小
        scrollWidth:{
            type:String,
            default:'100%'
        },
    },
    // 创建滚动视图
    mounted(){
        this.scroll=new IScroll(this.$refs.scroll,{
            scrollX:this.scrollX,
            scrollY:this.scrollY,
            freeScroll:this.scrollX && this.scrollY,
            tap:true,
            click:true
        });
        // 监听滚动之前，在滚动的时候刷新滚动视图
        this.scroll.on('beforeScrollStart',() => {
            this.scroll.refresh()
        })
    },
    // 设置滚动视图的刷新
    methods:{
        refresh(){
            this.scroll.refresh();
        }
    }
};
</script>

<style scodped>
.scroll-view,.scroll-container{
    overflow: hidden;
}
</style>
