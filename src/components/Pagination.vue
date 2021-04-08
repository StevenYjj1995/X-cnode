<template>
<div class="pagination">
  <button @click="changeBtn">首页</button>
  <button @click="changeBtn">上一页</button>
  <button v-if="jduge" class='pagebtn'>......</button>
  <!-- 页码等于current时使用样式-->
  <button v-for="btn in pagebtns"
  @click="changeBtn(btn)"
  :class="[{currentPage:btn==currentPage},'pagebtn']">
    {{btn}}
  </button>

  <button @click="changeBtn">下一页</button>

</div>
</template>

<script>
import $ from 'jquery'
export default {
  name: "Pagination",
  data(){
    return {
      pagebtns:[1,2,3,4,5,'......'],
      currentPage:1,
      jduge:false
    }
  },
  methods:{
    changeBtn(page){
      //点击上一页，下一页或首页
      if(typeof page != 'number'){
        switch (page.target.innerText){
          case '上一页':
            $('button.currentPage').prev().click()
            break;
          case '下一页':
            $('button.currentPage').next().click()
            break;
          case '首页':
            this.pagebtns=[1,2,3,4,5,'......']
            this.changeBtn(1)
            break;
          default:
            break
        }
        return
      }
      this.currentPage=page
      if(page>4){
        this.jduge=true
      }else{
        this.jduge=false
      }
      if(page === this.pagebtns[4]){
        this.pagebtns.shift() //移除第一个元素
        this.pagebtns.splice(4,0,this.pagebtns[3]+1) //添加最后一个元素
      }else if(page === this.pagebtns[0]){
        if(this.pagebtns[0]>1){this.pagebtns.splice(4,1) //移除最后一个元素
          this.pagebtns.unshift(this.pagebtns[0]-1) //添加第一个元素
        }
      }
      this.$emit('handleList',this.currentPage)
    }
  }
}
</script>

<style scoped>
.pagination {
  margin-top: 5px;
  margin-bottom: 5px;
  background-color: white;
  padding: 6px 20px;
}

button {
  background-color: #fff;
  border: 1px solid #ddd;
  color: #778087;
  border-radius: 3px;
  outline: none;
  height: 21px;
  cursor: pointer;
  padding: 0 2px;
  width: 55px;
  height: 29px;
}

.pagebtn {
  position: relative;
  bottom: 1px;
  width: 40px;
  margin: 0 4px;
}

.currentPage {
  color: white;
  background-color: #1f1b1b;

}
</style>
