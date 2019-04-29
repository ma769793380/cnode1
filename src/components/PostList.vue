<template>
    <div class="PostList">
      <!--加载动画-->
      <div class="loading" v-if="isLoading">
        <img src="../assets/loading.gif">
      </div>
      <!--文章列表-->
      <div class="posts" v-else>
        <ul>
          <!--顶部分类-->
          <li>
            <div class="toobar">
              <span>全部</span>
              <span>精华</span>
              <span>分享</span>
              <span>问答</span>
              <span>招聘</span>
            </div>
          </li>

          <li v-for="post in posts">
            <!--主题列表中的头像-->
            <img :src="post.author.avatar_url">
            <!--回复量/阅览量-->
            <span class="allcount">
              <span class="reply_count">{{post.reply_count}}</span>
              <span>/</span>
              <span class="visit_count">{{post.visit_count}}</span>
            </span>
            <!--帖子分类-->
            <span :class="[{put_good:(post.good === true),put_top:(post.top === true),
            'topiclist-tab':(post.good !== true&&post.top !==true)}]">
                {{post | tabFormatter}}
            </span>
            <!--主题标题-->
            <router-link :to="{
              name:'post_count',
              params:{
                id:post.id,
                name:post.author.loginname
              }
            }">
              <span>
                {{post.title}}
              </span>
            </router-link>

            <!--帖子最后回复的时间-->
            <span class="last_reply">
              {{post.last_reply_at | formatData}}
            </span>
          </li>
            <!--分页器-->
            <li>
                <pagination @handleList="renderList"></pagination>
            </li>
        </ul>
      </div>
    </div>
</template>

<script>
    import pagination from './Pagination'
  // 主题首页API： https://cnodejs.org/api/v1/topics
    export default {
        name: "PostList",
        data(){
          return {
            isLoading :false,
            posts:{},
            postpage:1
          }
        },
        methods:{
          getData(){
            this.$http.get('https://cnodejs.org/api/v1/topics',{
              params:{
                page:this.postpage,
                limit:20
              }
            }).then((res)=>{
              this.isLoading = false;
              this.posts = res.data.data
            })
              .catch((err)=>{
                console.log(err)
              })
          },
          renderList(value){
            this.postpage = value;
            this.getData()
          }
        },
        components:{
            pagination
        },
        // 数据加载前
        beforeMount() {
          this.isLoading = true;
          this.getData()
        }
    }
</script>

<style scoped>
  .PostList{
    background-color: #e1e1e1;

  }
  .posts {
    margin-top: 10px;

  }

  .PostList img {
    height: 30px;
    width: 30px;
    vertical-align: middle;
  }
  ul {
    list-style: none;
    width: 100%;
    max-width: 1344px;
    margin: 0 auto;
  }
  ul li:not(:first-child) {
    padding: 9px;
    font-size: 15px;
    font-family: "Helvetica Neue", "Luxi Sans", "DejaVu Sans", Tahoma, "Hiragino Sans GB", STHeiti, sans-serif !important;
    font-weight: 400;
    background-color: white;
    color: #333;
    border-top: 1px solid #f0f0f0;
  }
  li span{
    line-height: 30px;
  }
  li:not(:first-child):hover {
    background: #f5f5f5;;
  }
  li:last-child:hover {
    background: white;
  }
  .toobar{
    height: 30px;
    background-color: #f5f5f5;
    padding-bottom: 10px;
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
  }
  .toobar span{
    color: #80bd01;
    line-height: 40px;
    font-size: 14px;
    margin: 0 20px;
    cursor: pointer;
  }
  .toobar span:hover {
    color: #9e78c0;
  }
  .loading {
    text-align: center;
    padding-top: 300px;
  }
  .reply_count{
    color: #9e78c0;
    font-size: 14px;
  }
  .allcount {
    width: 70px;
    display: inline-block;
    text-align: center;
    font-size: 12px;
  }
  .last_reply {
    text-align: right;
    min-width: 50px;
    display: inline-block;
    white-space: nowrap;
    float: right;
    color: #778087;
    font-size: 12px;
  }
  .put_good,.put_top{
    background: #80bd01;
    padding: 2px 4px;
    border-radius: 3px;
    -webkit-border-radius: 3px;
    -moz-border-radius: 3px;
    -o-border-radius: 3px;
    color: #fff;
    font-size: 12px;
    margin-right: 10px;
  }
  .topiclist-tab {
    background-color: #e5e5e5;
    color: #999;
    padding: 2px 4px;
    border-radius: 3px;
    -webkit-border-radius: 3px;
    -moz-border-radius: 3px;
    -o-border-radius: 3px;
    font-size: 12px;
    margin-right: 10px;
  }
  a {
    text-decoration: none;
    color: black;
  }

  a:hover {
    text-decoration: underline;
  }

  .loading {
    text-align: center;
    padding-top: 300px;
  }
</style>
