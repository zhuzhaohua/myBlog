<template>
  <div>
    <div class=" items ">

      <el-row>
        <el-col :span="11" v-for=" (item, index) in data.items" :key="item.key" :offset=" index%2 == 1? 2: 0 ">
          <el-card  class="box-card" shadow="always" :body-style="{ padding: '0px' }"  >
            <div style=" cursor:pointer;" @click="gogogo(item.path)">
              <div slot="header" class="cardHeader">
                <div style=" padding: 10px ">
                  <span class="blogTitle">{{ item.title }}</span>

                </div>
              </div>
              <div class="cardContent">
                <div v-if=" item.frontmatter.note ">
                    <span class="note" > {{"\"" + item.frontmatter.note + "\""   }} </span>
                </div>
              </div>
              <div class="cardFooter">
                <el-tag size="mini" type="warning">{{item.frontmatter.type  }}  </el-tag>
                <el-tag v-for=" tag in item.frontmatter.tags.split('|') " :key="tag" style="margin-left: 5px" size="mini" >{{ tag}}</el-tag>
                <time class="time">{{ item.frontmatter.date }}</time>
              </div>
            </div>
          </el-card>
        </el-col>
      </el-row>
      <el-alert
        v-if = " data.items == null  || data.items.length == 0 "
        title="暂无文章"
        type="info"
        center
        show-icon
        :closable=" false ">
      </el-alert>
    </div>

    <div class="pagination">
      <el-pagination
        background
        layout="prev, pager, next"
        :page-size = " pageSize "
        :total=" data.total "
        @current-change= "pageChange"
        @prev-click= "prevPage" 
        @next-click= "nextPage" >
      </el-pagination>
    </div>

  </div>
</template>

<style scope>
  .blogTitle {
    font-size: 18px;
    font-weight:bold 
  }
  .note {
    font-size: 12px
  }

  .box-card {
    width: 100%;
    margin-bottom: 20px;
  }
  .pagination {
    text-align: center
  }
  .items {
    min-height: 500px
  }

  .time {
    font-size: 13px;
    color: #999;
    float:right;
  }

  .cardHeader {
    /* background-color:bisque; */
    height: 50px;
    margin: 10px;
   
  }
  .cardContent {
    padding:10px;
    margin: 10px;
    height: 80px;
  }
  .cardFooter {
    padding:10px;
    height: 20px;
  }

</style>

<script>
export default {
  data() {
    return {
      pageSize : 10,
      page: 1,
      data: {
        items:[],
        total:0
      }
    }
  },
  props: ['tag','type'],
  created: function () {
    this.show();
  },
  computed: {
    pages () {
      const pages = [];

      if (this.type) {
        this.$site.pages.forEach(item => {

          if (item.frontmatter.type == this.type) {
            pages.push (item);
          }
        });

        return pages;
      }

      if (this.tag) {
        this.$site.pages.forEach(item => {
          if (item.frontmatter.tags) {
            let tags = item.frontmatter.tags.split("|");
            if (tags.indexOf(this.tag) >= 0 ) {
              pages.push (item);
            }
          }
        });

        return pages;
      }

      this.$site.pages.forEach(item => {

        if (item.frontmatter.type) {
          pages.push (item);
        }
      });

      return pages;
    },
  },
  methods: {
    show() {
     let startNo = this.pageSize * ( this.page - 1) ;
      let endNo = this.pageSize * this.page;
      this.data.items = this.pages.slice(startNo, endNo) ;
      this.data.total = this.pages.length;
    },
    gogogo (path) {
      window.location.href= path;
    },
    pageChange(thisPageNo){
      this.page = thisPageNo;
      this.show()
    },
    nextPage(thisPageNo) {
      this.pageChange(thisPageNo);
    },
    prevPage(thisPageNo) {
      this.pageChange(thisPageNo);
    }
  },
  watch: {
    tag(tag) {
      this.show()
    }
  }
}
</script>
