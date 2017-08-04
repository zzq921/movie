<template>
  <div class="home">
    <h1>{{ msg }}</h1>
    <ul>
      <li v-for="article in articles">
          <div class="m-img inl-block">< img :src="article.images.small"/></div>
       <div class="m-content inl-block">
          <div>{{article.title}}</div>
        <div>年份：{{article.year}}</div>
         <div>类型：{{article.subtype}}</div>
       </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'home',
  data () {
    return {
      msg: '电影之家',
      articles: [
        {
          images: {
            small: 'https://img.yzcdn.cn/upload_files/2017/06/28/FqntPSLkMV5IDhMl24v97ZOMTeTq.jpg?imageView2/2/w/200/h/200/q/75/format/webp',
          },
          
          title: '一个不要钱的石榴',
          year: 2017,
          subtype: 'wahaha'
        }
      ]
    }
  },
    created: function() { // 这里mounted和created生命周期函数区别
     this.$http.jsonp('https://api.douban.com/v2/movie/top250?count=10', {}, {
        headers: {

        },
        emulateJSON: true
    }).then(function(response) {
      // 这里是处理正确的回调
        console.log(response);
        // this.articles = response.data.subjects
        // this.articles = response.data["subjects"] 也可以

    }, function(response) {
        // 这里是处理错误的回调
        console.log(response)
    });
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  ul{
    list-style: none;
    margin: 0;
    padding: 0;
  }
  ul li{
  border-bottom: 1px solid #999;
  padding: 10px 0;
  }
  
  .inl-block{
  display: inline-block;
  }
  
  .m-img{
    
  }
  .m-content{
  margin-left: 20px;
  }
</style>