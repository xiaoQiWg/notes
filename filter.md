## 使用js中的迭代函数filter
    filter():对数组中的每一项运行给定函数，返回该函数会返回true的项组成员的数组。

####实例1

```html
<div>
  Filter Key : <input type="text" v-model="key">
  <ul>
    <li v-for="item in filterList">
      {{item}}
    </li>
  </ul>
</div>
```
```js
export default {
  data(){
    return{
      list:['AAA','VVV','bbb','rgw','werw','iytui','uyja','aefa','awraw','wqnn','retyer','sers','mki','sfvgs'],
      key:''
    }
  },
  computed:{
    filterList(){
      var list = this.list;
      var key = this.key;
      return list.filter(item => {
        return item.toLowerCase().indexOf(key.toLowerCase()) != -1;
      })
    }
  }
}
```
    其他的一些Js 迭代方法——filter()、map()、some()、every()、forEach()、lastIndexOf()、indexOf()

#### 实例2
```html
<div>
    <form id="main" v-cloak>
      <div class="bar">

        <input type="text" v-model="searchString" placeholder="Enter your search terms" />
      </div>
      <ul>

        <li v-for="article in filteredArticles">
          <a v-bind:href="article.url" rel="external nofollow" ><img v-bind:src="article.image" /></a>
          <p>{{article.title}}</p>
        </li>
      </ul>
    </form>
  </div>
```
```js
export default {
    data(){
      return{
        searchString:'',
        articles:[
          {
            "title": "What You Need To Know About CSS Variables",
            "url": "http://tutorialzine.com/2016/03/what-you-need-to-know-about-css-variables/",
            "image": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQmBuM7hlJpdELwq0BSo01For8Ed0wCXQAHV9jHq-_PzRH6wF91"
          },
          {
            "title": "Freebie: 4 Great Looking Pricing Tables",
            "url": "http://tutorialzine.com/2016/02/freebie-4-great-looking-pricing-tables/",
            "image": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTbH-xAQQDlwpR_Nig66fspeYA2QvSAoZmwn6RNgIk7aigHxBEi"
          },
          {
            "title": "20 Interesting JavaScript and CSS Libraries for February 2016",
            "url": "http://tutorialzine.com/2016/02/20-interesting-javascript-and-css-libraries-for-february-2016/",
            "image": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQWIbs1cmJ4QeVKRQE4c_A_RZ_HJvkHRKudCBcTgerI7kmw0yPjSg"
          },
          {
            "title": "Quick Tip: The Easiest Way To Make Responsive Headers",
            "url": "http://tutorialzine.com/2016/02/quick-tip-easiest-way-to-make-responsive-headers/",
            "image": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQltg_0PzWsXoBeIg7iqNwbruKI9WgXT2AzhR1BZM7Mim2TMdH0cA"
          },
          {
            "title": "Learn SQL In 20 Minutes",
            "url": "http://tutorialzine.com/2016/01/learn-sql-in-20-minutes/",
            "image": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRZaAHyHFL4NobdtmsGDoEUovpEptRWqTlvmiUCyf0jfG4bW-Pa4A"
          },
          {
            "title": "Creating Your First Desktop App With HTML, JS and Electron",
            "url": "http://tutorialzine.com/2015/12/creating-your-first-desktop-app-with-html-js-and-electron/",
            "image": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQApR5hqB7iBddDFcXRprwlk60yfBk9dOxpAHcAC_4rDl27sYj-"
          }
        ]
      }
    },
    computed:{
      filteredArticles:function () {
        var articles_array = this.articles, searchString = this.searchString;
        if(!searchString){
          return articles_array;
        }

        searchString = searchString.trim().toLowerCase();
        articles_array = articles_array.filter(function (item) {
          if (item.title.toLowerCase().indexOf(searchString) != -1){
            return item;
          }
        })

        return articles_array;
      }
    }
  }
```

## Vue实现搜索 和新闻列表功能简单范例

```html
<div>
    <div class="box">
      <div class="left">
        <input type="text" placeholder="输入编号" v-model="id" />
        <input type="text" placeholder="输入名称" v-model="name" />
        <input type="button" value="添加数据" @click="add()" />
        <input type="text" placeholder="搜索数据" v-model="search" />
      </div>
      <div class="right">
        <table>
          <tr>
            <th>编号</th>
            <th>品牌名称</th>
            <th>创建时间</th>
            <th>操作</th>
          </tr>
          <tr v-for="item in searchData">
            <td>{{item.id}}</td>
            <td>{{item.name}}</td>
            <td>{{item.time | datefmt('yyyy-mm-dd HH:mm:ss')}}</td>
            <td>
              <a href="javascript:void(0)" rel="external nofollow" @click="del(item.id)">删除</a>
            </td>
          </tr>
        </table>
      </div>
    </div>
  </div>
```
全局定义过滤器
```js
Vue.filter('datefmt',(input,formatstring) => {
  var result = '';
  var year = input.getFullYear();
  var month = input.getMonth() + 1;
  var day = input.getDate();
  var hour = input.getHours();
  hour = hour < 10 ? '0' + hour : hour;

  var minute = input.getMinutes();
  minute = minute < 10 ? '0' + minute : minute;

  if(formatstring == 'yyyy-mm-dd'){
    result = year + '-' + month + '-' + day;
  }else {
    result = year + "-" + month + "-" + day + " " + hour + ":" + minute;
  }
  return result;

})
```
```js
 export default {
    data(){
      return{
        id:'',
        name:'',
        search:'',
        list:[
          {
            'id':1,
            'name':'宝马',
            'time':new Date()
          },
          {
            'id':2,
            'name':'奔驰',
            'time':new Date()
          }
        ]
      }
    },
    methods:{
      del: function (id) {
        if(!confirm('是否删除数据？')){
          return;
        }

        // 调用list.findIndex()方法，根据传入的id获取到这个要删除数据的索引值
        var index = this.list.findIndex(function (item) {
          return item.id == id;
        });

        // 调用list.splice(删除的索引,删除的元素个数)
        this.list.splice(index,1);
      },
      add(){
        // 包装成list要求的对象
        var tem = {
          id:this.id,
          name:this.name,
          time:new Date()
        };

        // 将tem追加到list数组中
        this.list.push(tem);

        //清空页面上的文本框中的数据

        this.id = '';
        this.name = '';
      },

    },
    computed:{
      searchData:function(){
        var search = this.search;
        if(search){
          return this.list.filter((name) => {
            return Object.keys(name).some((key) => {
              return String(name[key]).toLowerCase().indexOf(search) != -1;
            })
          })
        }
        return this.list;
      }
    }

  }
```

```css
  *{padding:0;margin:0;font-size: 14px;}
  .box{width:700px;margin:50px auto 0;display: flex;}
  .left{width:200px;border:1px solid #222;box-sizing: border-box;padding:15px 9px 7px;margin-right:20px;}
  .left input{width:100%;margin-bottom:8px;box-sizing: border-box;height:30px;padding:0 5px;border-radius:5px;border-width: 1px;outline: none;}
  .left input[type='button']{color:#fff;background-color:green;border:0;margin-bottom:15px;}
  .right{width:480px;}
  .right table{width:100%;border-collapse: collapse;}
  .right table th,.right table td{border:1px solid #222; height:30px;text-align: center;}
  .right table th{color:#fff;background:#4855b0;}
```