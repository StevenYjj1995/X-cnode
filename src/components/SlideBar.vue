<template>

<div class="autherinfo">
    <!--数据未返回时显示的的载入动画-->
    <div class="loading" v-if="isLoading">
      <img src="../assets/loading.gif">
    </div>


  <div class="authersummay" v-else>
    <div class="topbar">作者</div>

    <router-link :to="{
            name:'user_info',
            params:{
              name:userinfo.loginname
            }
          }"><img :src="userinfo.avatar_url"></router-link>
    <span class="loginname">{{userinfo.loginname}}</span>
    <p style="margin: 10px;padding-bottom: 10px">积分：{{userinfo.score}}</p>
  </div>
  <div class="recent_topics">
    <div class="topbar">作者其他主题</div>
    <ul>
      <li v-for="item in topiclimitby5">
        <router-link :to="{
          name:'post_content',
          params:{
            id:item.id,
            name:item.author.loginname
          }
        }">
        {{item.title}}
        </router-link>
      </li>
    </ul>
  </div>
  <div class="recent_replies">
    <div class="topbar">作者最近回复</div>
    <ul>
      <li v-for="item in replylimitby5" :key="item.id">
        <router-link :to="{
          name:'post_content',
          params:{
            id:item.id,
            name:item.author.loginname
          }
        }">
        {{item.title}}
        </router-link>
      </li>
    </ul>

  </div>
</div>
</template>

<script>
export default {
  name: "SlideBar",
  data(){
    return{
      userinfo:{},
      isLoading:false
    }
  },
  methods:{
    //由于侧边栏所在的页面的是文章详情页，所以在由文章列表页点击过来的时候还需要传递username参数
    getUserinfoData(){
      this.$http.get(`https://cnodejs.org/api/v1/user/${this.$route.params.name}`)
        .then(res=>{
          this.isLoading=false
          this.userinfo = res.data.data
        })
        .catch(err=>{
          console.log(err)
        })
    }
  },
  computed:{
    topiclimitby5(){
      if(this.userinfo.recent_topics){
        return this.userinfo.recent_topics.slice(0,5)
      }
    },
    replylimitby5(){
      if(this.userinfo.recent_replies){
        return this.userinfo.recent_replies.slice(0,5)
      }
    }
  },
  beforeMount() {
    this.isLoading=true
    this.getUserinfoData()
  },

}
</script>

<style scoped>
*{
  margin: 0;
  padding: 0;
}
.authersummay, .recent_replies, .recent_topics {
  background-color: #fff;
}
.autherinfo {
  width: 328px;
  float: right;
  margin-top: 0;
}
li{
  padding: 3px 0 ;
}
.recent_replies ul, .recent_topics ul {
  margin-top: 0px;
  margin-bottom: 0px;
  list-style: none;
  padding-left: 14px;
}

ul a {
  font-size: 12px;
  text-decoration: none;
  color: #778087;
}

.topbar {
  padding: 10px;
  background-color: #f6f6f6;
  height: 16px;
  font-size: 12px;
  margin-top: 10px;
}

img {
  height: 48px;
  width: 48px;
  border-radius: 3px;
  margin: 10px;
}

.loginname {
  width: 100px;
  float: right;
  margin-top: 22px;
  margin-right: 159px;
  font-size: 14px;
}

.loginname a {
  text-decoration: none;
  color: #778087;
}

.authersummay .topbar {
  margin-top: 0px;
}
</style>
