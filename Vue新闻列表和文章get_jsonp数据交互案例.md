### App.vue
```html
<div class="top">
  <router-link :class="{on:'/home' === $route.path}" to="/home">首页</router-link>
  <router-link :class="{on:'/news' === $route.path}" to="/news">新闻</router-link>
  <router-link :class="{on:'/user' === $route.path}" to="/user">用户</router-link>
</div>
<hr>
<router-view></router-view>
```
```css
  body{
    padding:0;
    margin:0;
  }
  .top{

    text-align: center;
    background:#222;
    padding:1rem;
  }
  .top a{
    margin:0 2rem;
    color:#fff;
  }
  .top .on{color:#f00;}
```

### main.js 路由配置
```js
import Vue from 'vue'
import App from './App.vue'

Vue.config.productionTip = false

import VueResource from 'vue-resource'
Vue.use(VueResource)

import VueRouter from 'vue-router'
Vue.use(VueRouter);

// 引入组件
import Home from './components/Home'
import News from './components/News'
import User from './components/User'
import Content from './components/Content'

// 定义路由
const routes = [
  {path:'/home',component:Home},
  {path:'/news',component:News,name:'news'},
  {path:'/user',component:User},
  {path:'/content/:aid',component:Content}
];
// 实例化
const router = new VueRouter({
  routes
})
new Vue({
  router,
  render: h => h(App),
}).$mount('#app')

```

### 主页跳转
```html
<div>
    首页
    <hr>
    <button @click="goNews()">通过js跳转到新闻页面</button>
</div>
```

```js
methods:{
    goNews(){
        this.$router.push({name:'news'})
    }
}
```

### 新闻jsonp获取数据
```html
<div>
    <h3>新闻</h3>
    <hr>
    <ul>
        <li v-for="item in list">
            <router-link :to="'/content/' + item.aid">{{item.title}}</router-link>
        </li>
    </ul>
</div>
```
```js
export default {
    name: "News",
    data(){
        return{
            list:[]
        }
    },
    methods:{
        requestData(){
            let api = 'http://www.phonegap100.com/appapi.php?a=getPortalList&catid=20&page=1';
            this.$http.jsonp(api).then((response) => {
                console.log(response);
                this.list = response.body.result;
            },err => {
                console.log(err);
            });
        }
    },
    mounted(){
        this.requestData();
    }
}
```

### content 文章内容get获取数据内容

```html
<div>
    <h2>{{list.title}}</h2>
    <div v-html="list.content"></div>
</div>
```

```js
export default {
    data(){
        return{
            list:[]
        }
    },
    mounted(){
        console.log(this.$route.params); // 获取动态路由
        let aid = this.$route.params.aid;
        this.requestData(aid);
    },
    methods:{
        requestData(aid){
            let api = 'http://www.phonegap100.com/appapi.php?a=getPortalArticle&aid='+aid;
            this.$http.get(api).then(response => {
                console.log(response);
                this.list = response.body.result[0];
            })
        }
    }
}
```