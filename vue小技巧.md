## 1.filters 过滤器判断内容是否大于10000改变

```html
<p>{{数据 | formatCount}}</p>
```
```js
filters: {
  formatCount (v) {
    if (v < 9999) {
      return v
    } else {
      return (v / 10000).toFixed(0) + '万'
    }
  }
}
```

## 2.截取指定长度的数据

```js
// 案例1
this.$http.get(api).then(response => {
    console.log(response);
    this.list = response.body.result.slice(0,6);
});

// 案例2
this.playList = data[0].result.length > 6 && data[0].result.slice(0, 6)
this.bannerList = data[1].banners
this.mvList = data[2].result.length > 6 ? data[2].result.slice(0, 6) : data[2].result
```

