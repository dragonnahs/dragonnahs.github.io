---
title: 一些算法和封装的代码
date: 2016-17-12 10:10:04
tags: [js,封装,代码片段,算法]
categories: js代码片段
---
现在网上的方案都是生成一个新的dist目录，里面包含了要发布的html,js,css等文件。但是在实际的公司的项目中，会有情况不能生成新的HTML进行发布，需要在原来的HTML文件上进行js ,css版本的替换. 这里分享下我在实际项目中通过改动插件然后在原目录结构下进行版本的控制方案
<!-- more -->
### 一些算法和封装的代码


1. 字符串中各个字符串出现的次数
```
var arr = 'abcdaabc';

var info = arr
    .split('')
    .reduce((p, k) => (p[k]++ || (p[k] = 1), p), {});

console.log(info); //{ a: 3, b: 2, c: 2, d: 1 }

```
reduce 对于低版本兼容性不是很好，
可以用下面的方法

```
var temp = {};
'abcdaabc'.replace(/(\w{1})/g,function($1){
    temp[$1] ? temp[$1]+=1 : temp[$1] = 1;
})
console.log(temp) // {a: 3, b: 2, c: 2, d: 1}

// 或者
function getTimesO(str){
  var obj = {}
  str.split('').map(function(val,index){
    if(!obj[val]){
      obj[val] = 1 
    }else{
      obj[val] += 1
    }
  })
  return obj
}

```

2. 阻止事件冒泡
```
function stopBubble(e)
{
    if (e && e.stopPropagation)
        e.stopPropagation()
    else
        window.event.cancelBubble=true
}

```

3. 判断数据类型，
- typeof 
> `typeof 变量`  返回的是变量的数据类型，但是不能区分数组和对象
- instanceof 
> `变量 instanceof Object||Array` 判断变量是数组还是对象，返回true和false
- Array.isArray()
> `Array.isArray(变量)`  判断变量是不是数组，返回true和false

4. 在console.log（）中加上前缀，‘iphone’

封装log函数
- 初步封装
```
function log(){
  console.log.apply(console,arguments)
}

```
- 第二次封装，怎么才能在参数前面加前缀

```
function log(){
  var newArguments = []
  if(arguments.length > 0){
    for(var i = 0; i < arguments.length; i++){
      newArguments.push('iphone',arguments[i])
    }
  }
  console.log.apply(console,newArguments)
}

```
> 也可以下面的写法

```
function getLog(){
  var args = Array.prototype.slice.call(arguments) // 把arguments伪数组转化为真数组
  args.unshift('(app)') // 调用数组的方法
  console.log.apply(console,args)
}
getLog('df') // (app) df



```

4. 数组排序

- 第一种
```
function sortMany(arr){
  if(arr.length <= 1){
    return arr
  }
  var left = [], right = []
  var middleIndex = Math.floor(arr.length/2)
  var middleValue = arr.splice(middleIndex,1)[0]
  for(var i = 0; i < arr.length; i++){
    if(arr[i] < middleValue){
      left.push(arr[i])
    }else{
      right.push(arr[i])
    }
  }
  return sortMany(left).concat(middleValue,sortMany(right))

}

```

- 第二种

```
function sortTwo(arr){
  for(var i=0;i<arr.length-1;i++){
    for(var j=i+1;j<arr.length;j++){
      if(arr[i]>arr[j]){
        var temp = arr[j]
        arr[j] = arr[i]
        arr[i] = temp
      }
    }
  }
  return arr
}

```
5. 数组的去重

```
function deletMany(arr){
  var obj = {}
  var newArr = []
  for(var i=0; i<arr.length-1;i++){
    if(!obj[arr[i]]){
      newArr.push(arr[i])
      obj[arr[i]] = 1
    }
  }
  return newArr
}

```


6. 对象的深拷贝问题
> 代码如下，实现对象的深拷贝

```
function deepCopy(p, c){
      var c = c || {}
      for(var i in p){
        if(typeof p[i] === 'object'){
          c[i] = (p[i].constructor === Array) ? [] : {}
          deepCopy(p[i], c[i])
        }else{
          c[i] = p[i]
        }
      }
      return c
    }

```
 >拷贝分为深拷贝和浅拷贝，拷贝就是把父对象的属性全部拷贝给子对象。
- 浅拷贝只是把对象的第一层属性拷贝下来，如果第一层中有复杂数据类型，只是拷贝的指针，如果父属性的属性变化也会导致拷贝的子对象的属性变化，这有时是不需要的。
- 上面的代码实现的是使用递归实现的深拷贝，也可以使用`JSON.stringfy`先转成简单类型，再使用`JSON.parse`转换成复杂类型。
> 另外一种对象深拷贝

```
function copyObject(orig){
  var copy = Object.create(Object.getPrototypeOf(orig))
  copyOwnPropertiesFrom(copy, orig)
  return copy
}

function copyOwnPropertiesFrom(target, source){
  Object
    .getOwnPropertyNames(source)
    .forEach(function(val){
      var desc = Object.getOwnPropertyDescriptor(source, val)
      if(typeof desc.value === 'object'){
        target[val] = copyObject(source[val])
      }else{
        Object.defineProperty(target, val, desc)
      }
    })
    return target
}

```


7. 判断类型的封装
```
let type = (o) => {
    const s = Object.prototype.toString.call(o)
    return s.match(/\[object (.*?)\]/)[1].toLowerCase()
}

[
    "Undefiend",
    'Null',
    'Object',
    'Array',
    "String",
    "Boolean",
    'RegExp',
    'Function'
].forEach(t => {
    type['is'+ t] = (o) => {
        return type(o) === t.toLowerCase()
    }
});
type.isArray([]) //true

```

8. 金额格式化

```

function toThousands(num) {
    var potStr = '.00'
    num = (num||0).toString()
    if(num.indexOf('.') !== -1){
       potStr = num.substr(num.indexOf('.'),3)
    }
    
    var result = [ ], counter = 0;
    num = num.substring(0,num.indexOf('.')).split('');
    for (var i = num.length - 1; i >= 0; i--) {
        counter++;
        result.unshift(num[i]);
        if (!(counter % 3) && i != 0) { result.unshift(','); }
    }
    return result.join('')+potStr;
}

```


