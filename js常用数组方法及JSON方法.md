## JSON 方法混乱 小记

    stringify: 字符串化
    parse: 解析
```js
var json1 = '{"1":1,"2":2,"3":3}';
var json2 = {'one':1,'two':2,'three':3};

// 将字符串转换为对象        方法用来解析JSON字符串，构造由字符串描述的JavaScript值或对象。
console.log(JSON.parse(json1));
// 将对象转换为json数据      序列化成 一个JSON 字符串的值。
console.log(JSON.stringify(json2)); 
```

## js 常用原生数组方法 小记

### 合并数组 concat()
    描述：连接两个或更多的数组，并返回结果。
    语法：arrayObject.concat(arrayX,arrayX,……,arrayX)
    参数：必需。该参数可以是具体的值，也可以是数组对象。可以是任意多个。
    注意：该方法不会改变现有的数组，而仅仅会返回被连接数组的一个副本。

```js
var a = [1,2,3], b = [2,3,4];
console.log(a.concat(4,5));   // 1,2,3,4,5
console.log(a.concat(b));     // 1,2,3,2,3,4
console.log(a);   // 1,2,3
```
### 创建新数组 slice()
    描述：从已有的数组中返回选定的元素。
    语法：array.slice(start, end)
    参数： 
    start:必需。规定从何处开始选取。如果是负数，那么它规定从数组尾部开始算起的位置。也就是说，-1 指最后一个元素，-2 指倒数第二个元素，以此类推。 
    end:可选。规定从何处结束选取。该参数是数组片断结束处的数组下标。如果没有指定该参数，那么切分的数组包含从 start 到数组结束的所有元素。如果这个参数是负数，那么它规定的是从数组尾部开始算起的元素。
    注意：该方法不会改变现有的数组，而仅仅会返回一个新的数组。 不包括结束下标。
    
```js
var arr = [1,2,3,4];
console.log(arr.slice(0,2)); // [1,2]  不包括结束下标
```
### 连接数组 join()
    描述：将所有的数组元素连接成一个字符串。元素是通过指定的分隔符进行分隔的。
    语法：arrayObject.join(separator)
    参数：可选。指定要使用的分隔符。如果省略该参数，则使用逗号作为分隔符。
    注意：该方法不会改变现有的数组，而仅仅会返回一个字符串。
```js
var arr = ['George','John','Thomas'];
console.log(arr.join());      //George,John,Thomas
console.log(arr.join('_'))    //George_John_Thomas
```
### 删除数组元素

#### 删除数组最后一个元素 pop()
    描述：删除并返回数组的最后一个元素。
    语法：arrayObject.pop() 
    参数：无
    注意：该方法会修改原数组。但是如果数组已经为空，则 pop() 不改变数组，并返回 undefined 值。
```js
var arr = ['George','John','Thomas'];
console.log(arr.pop());     // Thomas
console.log(arr);           //["George", "John"]
```
#### 删除数组第一个元素 shift()
    描述：删除并返回数组的第一个元素。
    语法：arrayObject.shift()
    参数：无
    注意：该方法会修改原数组。但是如果数组已经为空，则 shift()不改变数组，并返回 undefined 值。
```js
var arr = ['George','John','Thomas'];
console.log(arr.shift());     //George
console.log(arr);             //["John", "Thomas"]
```
### 添加数组元素
#### 在数组末尾添加元素 push()

    描述：可向数组的末尾添加一个或多个元素，并返回新的长度。
    语法：arrayObject.push(arr1,arr2,….,arrx)
    参数：至少要有一个元素
    注意：该方法会修改原数组，并返回新数组的长度，而不是新的数组。
    
```js
var arr = ['George','John','Thomas'];
console.log(arr.length); // 3
console.log(arr.push('James')); // 4
console.log(arr);  // ["George", "John", "Thomas", "James"]
```
#### 在数组开头添加元素 unshift()
    描述：可向数组的开头添加一个或多个元素，并返回新的长度。
    语法：arrayObject.push(arr1,arr2,….,arrx)
    参数：至少要有一个元素
    注意：该方法会修改原数组。并返回新数组的长度，而不是新的数组。 
    unshift() 方法无法在 Internet Explorer 中正确地工作！
```js
var arr = ['George','John','Thomas'];
console.log(arr.length); // 3
console.log(arr.unshift('William')); // 4
console.log(arr);     // ["William", "George", "John", "Thomas"]
```

#### 插入数组元素 splice()
    描述：向数组中添加/删除项目，然后返回被删除的项目。
    语法：arrayObject.splice(index,howmany,item1,…..,itemX)
    参数： 
    index：必需。整数，规定添加/删除项目的位置，使用负数可从数组结尾处规定位置。 
    howmany：必需。要删除的项目数量。如果设置为 0，则不会删除项目。 
    item1, …, itemX：可选。向数组添加的新项目。
    注意：该方法会改变原始数组。如果从 arrayObject 中删除了元素，则返回的是含有被删除的元素的数组。
##### 插入数组元素：
```js
var arr = ['A','B','C','D','E'];
//在位置2插入“新”
console.log(arr.splice(2,0,'新'));
console.log(arr);  //["A", "B", "新", "C", "D", "E"]
```

##### 删除并插入数组元素：
```js
var arr = ['A','B','C','D','E'];
//从位置2开始，删除后面的1个元素，并插入“F”、“G”
console.log(arr.splice(2,1,'F','G'));  // ["C"]
console.log(arr);       // ["A", "B", "F", "G", "D", "E"]
```

### 数组排序 sort()
    描述：用于对数组的元素进行排序，该方法没有返回值。
    语法：arrayObject.sort(sortby)
    参数：可选。规定排序顺序。必须是函数。
    注意：该方法会改变原始数组。

#### 没参数时：
    注意！没参数时，sort()方法默认将所有的数组元素转化成字符串来进行比较排序，即按照字符编码的顺序进行排序！
```js
var a=[1,2,3,4,5,6,7,8,9,10];
console.log(a.sort())//1, 10, 2, 3, 4, 5, 6, 7, 8, 9
//比较是按照转化后的首个字符编码的大小来进行的
//"10"的话实际上比较的是"1"
console.log("1".charCodeAt());//49
console.log("10".charCodeAt());//49
console.log("2".charCodeAt());//50
```
#### 有参数时：
    如果想按照其他标准进行排序，就需要提供比较函数.
    
    该函数要比较两个值，然后返回一个用于说明这两个值的相对顺序的数字。比较函数应该具有两个参数 a 和 b，其返回值如下： 
    若 a 小于 b，在排序后的数组中 a 应该出现在 b 之前，则返回一个小于 0 的值。 
    若 a 等于 b，则返回 0。 
    若 a 大于 b，则返回一个大于 0 的值。
```js
function compare(a,b){
  if(a < b) {
    return -1;
  }
  if(a > b) {
    return 1;
  }
  return 0;
}
var a=[10,9,8,7,6,1];
console.log(a.sort(compare));//1, 6, 7, 8, 9, 10
```

### 倒置数组 reverse()
    描述：颠倒数组中元素的顺序。
    语法：arrayObject.reverse()
    参数：无
    注意：该方法会改变原来的数组，而不会创建新的数组。 
```js
var a = [1,2,3];
console.log(a.reverse());//3, 2, 1
```
### 查找数组元素
#### 查找指定元素 find()
    描述：返回传入一个测试条件（函数）符合条件的数组第一个元素。
    语法：array.find(function(currentValue, index, arr),thisValue)
    参数： 
    function(currentValue, index,arr)：必需。函数，数组中的每个元素都会执行这个函数。 
    
    函数参数：
        currentValue：必需。当前元素的值 
        index：可选。当期元素的索引值 
        arr ：可选。当期元素属于的数组对象
        
    thisValue: 可选。对象作为该执行回调时使用，传递给函数，用作 “this” 的值。如果省略了 thisValue ，”this” 的值为 “undefined”。 
    注意：该方法不会改变原来的数组。对于空数组，函数是不会执行的。

```js
function check(num){
  return num > 2;
}
var arr = [1,2,3,4];
console.log(arr.find(check));   // 3
console.log(arr);   //[1, 2, 3, 4]
```
#### 查找指定元素的索引 findIndex()

    描述：返回传入一个测试条件（函数）符合条件的数组第一个元素位置。如果没有符合条件的元素返回 -1。
    语法：array.findIndex(function(currentValue, index, arr),thisValue)
    参数： 
    function(currentValue, index,arr)：必需。函数，数组中的每个元素都会执行这个函数。 
    
    函数参数：
        currentValue：必需。当前元素的值 
        index：可选。当期元素的索引值 
        arr ：可选。当期元素属于的数组对象
    
    thisValue: 可选。对象作为该执行回调时使用，传递给函数，用作 “this” 的值。如果省略了 thisValue ，”this” 的值为 “undefined”。 
    注意：该方法不会改变原来的数组。对于空数组，函数是不会执行的。

```js
function check(num){
  return num>2;
}
var a = [1,2,3];
console.log(a.findIndex(check));//2
```
#### 从指定位置向后查找指定元素 indexOf()

    描述：返回某个指定元素在数组中首次出现的位置。如果没有符合条件的元素返回 -1。
    语法：array.indexOf(item,start)
    参数： 
    item：必须。查找的元素。 
    start：可选的整数参数。如省略该参数，则将从数组头部开始检索。
    注意：该方法不会改变原来的数组。

```js
var arr = ["a","b","c","b"];
console.log(arr.indexOf('b'));   // 1
console.log(arr.indexOf('a',3)); // -1
```
#### 从指定位置向前查找指定元素 lastIndexOf()

    描述：返回某个指定元素在数组中首次出现的位置。如果没有符合条件的元素返回 -1。
    语法：array.lastIndexOf(item,start)
    参数： 
    item：必须。查找的元素。 
    start：可选的整数参数。如省略该参数，则将从数组尾部开始检索。
    注意：该方法不会改变原来的数组
    
```js
var a = ["a","b","c","b"];
console.log(a.lastIndexOf("b"));//3
```
### 判断数组元素是否满足指定条件
#### 检测每个元素是否都符合条件 every()
    描述：检测数组所有元素是否都符合指定条件（通过函数提供），如果所有元素都通过检测返回 true，否则返回 false。
    语法：array.every(function(currentValue,index,arr), thisValue)
    参数： 
    function(currentValue, index,arr)：必需。函数，数组中的每个元素都会执行这个函数。 
    
    函数参数：
        currentValue：必需。当前元素的值 
        index：可选。当期元素的索引值 
        arr ：可选。当期元素属于的数组对象
    
    thisValue: 可选。对象作为该执行回调时使用，传递给函数，用作 “this” 的值。如果省略了 thisValue ，”this” 的值为 “undefined”。 
    注意：该方法不会改变原来的数组。不会对空数组进行检测。
```js
function check(num){
  return num>2;
}
var a = [1,2,3];
console.log(a.every(check));//false
```
#### 检测数组元素是否有符合条件的 some()
    描述：检测数组中的元素是否满足指定条件（函数提供），如果有元素通过检测返回 true（并停止检测），否则返回 false。
    语法：array.some(function(currentValue,index,arr), thisValue)
    参数： 
    function(currentValue, index,arr)：必需。函数，数组中的每个元素都会执行这个函数。 
    
    函数参数：
        currentValue：必需。当前元素的值 
        index：可选。当期元素的索引值 
        arr ：可选。当期元素属于的数组对象
    
    thisValue: 可选。对象作为该执行回调时使用，传递给函数，用作 “this” 的值。如果省略了 thisValue ，”this” 的值为 “undefined”。 
    注意：该方法不会改变原来的数组。不会对空数组进行检测。
```js
function check(num){
  return num>2;
}
var a = [1,2,3];
console.log(a.some(check));//true
```
### 过滤数组 filter()
    描述：创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素。如果没有符合条件的元素则返回空数组。
    语法：array.every(function(currentValue,index,arr), thisValue)
    参数： 
    function(currentValue, index,arr)：必需。函数，数组中的每个元素都会执行这个函数。 
    函数参数：
        currentValue：必需。当前元素的值 
        index：可选。当期元素的索引值 
        arr ：可选。当期元素属于的数组对象
    
    thisValue: 可选。对象作为该执行回调时使用，传递给函数，用作 “this” 的值。如果省略了 thisValue ，”this” 的值为 “undefined”。
    注意：该方法不会改变原来的数组。不会对空数组进行检测。
```js
function check(num){
  return num>2;
}
var a = [1,2,3,4];
console.log(a.filter(check));//[3, 4]
```

### 遍历数组
#### 无返回值 forEach()
    描述：调用数组的每个元素，并将元素传递给回调函数。该方法没有返回值。
    语法：array.forEach(function(currentValue, index, arr), thisValue)
    参数： 
    function(currentValue, index,arr)：必需。函数，数组中的每个元素都会执行这个函数。 
    
    函数参数：  
        currentValue：必需。当前元素的值 
        index：可选。当期元素的索引值 
        arr ：可选。当期元素属于的数组对象
    
    thisValue: 可选。对象作为该执行回调时使用，传递给函数，用作 “this” 的值。如果省略了 thisValue ，”this” 的值为 “undefined”。
    注意：该方法不会改变原来的数组。不会对空数组进行检测。

```js
var arr = [1,2,3,4], sum = 0;
function check(currentValue){
  return sum += currentValue;
}
console.log(arr.forEach(check));    // undefined
console.log(sum);    // 10
```
#### 有返回值 map()
    描述：返回一个新数组，数组中的元素为原始数组元素调用函数处理后的值。
    语法：array.map(function(currentValue,index,arr), thisValue)  
    参数： 
    function(currentValue, index,arr)：必需。函数，数组中的每个元素都会执行这个函数。 
    
    函数参数：
        currentValue：必需。当前元素的值 
        index：可选。当期元素的索引值 
        arr ：可选。当期元素属于的数组对象
    
    thisValue: 可选。对象作为该执行回调时使用，传递给函数，用作 “this” 的值。如果省略了 thisValue ，”this” 的值为 “undefined”。
    注意：该方法不会改变原来的数组。不会对空数组进行检测。
```js
var arr = [1,2,3,4], sum = 0;
function check(currentValue){
  return currentValue * 2;
}
// 便利输出
console.log(a.map(check)); // [2, 4, 6]
```
