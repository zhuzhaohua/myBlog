<template>
  <el-carousel :interval="2000" type="card" height="300px">
    <el-carousel-item v-for="item in 3" :key="item" >
      <div style=" text-align: center " @click=" selected(item) ">
          <h3>{{ title[item] }}</h3>
      </div>
    </el-carousel-item>
  </el-carousel>
</template>

<style scope>
  .el-carousel__item h3 {
  
    font-size: 20px;
    opacity: 0.75;
    line-height: 300px;
    margin: 0;
  }
  
  .el-carousel__item:nth-child(2n) {
     background-color: #d3dce6;

  }
  
  .el-carousel__item:nth-child(2n+1) {
   
    background-color: #99a9bf;
  }
</style>

<script>
export default {
  data() {
    return {
      title:['','本博客搭建教程','暂无专题','暂无专题']
    };
  },
  methods: {
    selected(index) {
      if (index === 1) {
        window.location.href= './technology/vue/20190601_myblog.html';
      }
    }
  }
}
</script>