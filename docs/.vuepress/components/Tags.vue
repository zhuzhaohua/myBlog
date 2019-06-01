<template>
  <div>
      <el-button v-for=" item in items " :key="item" class = "tags" size="medium" round @click="showBlogs(item)"> {{ item}}</el-button>
    <div v-if = " !listHide " style=" margin-top : 30px">
      <BlogList :tag=" tag "/>
    </div>
    <div v-if = "listHide" style=" margin-top : 30px" >
      <el-alert
        title="请选择标签"
        type="info"
        show-icon
        center
        :closable=" false ">
      </el-alert>
    </div>
  </div>
 
</template>

<style scope>
.tags {
    margin: 10px
}

</style>

<script>

export default {
  data() {
    return {
        items:[],
        tag : '',
        listHide :true
    }
  },
  created: function () {
      this.items = this.tags;
  },
  computed: {

      tags() {
        const ret = [];
        this.$site.pages.forEach(item => {

          if (item.frontmatter.tags) {
              let tagArr = item.frontmatter.tags.split("|")
              tagArr.forEach(tag => {
                  if (ret.indexOf(tag) < 0 ) {
                      ret.push(tag);
                  }
                }
              ); 
          }
        });
        return ret;
      }
  },
  methods: {
    showBlogs(tag) {
        this.tag = tag;
        this.listHide = false
    }
  }
}
</script>
