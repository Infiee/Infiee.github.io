title: js数组排序

tags: javascript
----------------

转载自:http://www.cnblogs.com/longze/archive/2012/11/27/2791230.html

sort()对数组排序，不开辟新的内存，对原有数组元素进行调换

1、简单数组简单排序

```javascript

 var arrSimple=new Array(1,8,7,6);

 arrSimple.sort();

 document.writeln(arrSimple.join());

```

2、简单数组自定义排序

```javascript

var arrSimple2=new Array(1,8,7,6);

 arrSimple2.sort(function(a,b){ return b-a});

 document.writeln(arrSimple2.join());

```

<!-- more -->

> 解释：a,b表示数组中的任意两个元素， 若return > 0 b前a后； reutrn < 0 a前b后； a=b时存在浏览器兼容 简化一下：a-b输出从小到大排序，b-a输出从大到小排序。

3、简单对象List自定义属性排序

```javascript
 var objectList = new Array();
 function Persion(name,age){ this.name=name; this.age=age; }
 objectList.push(new Persion('jack',20));
 objectList.push(new Persion('tony',25));
 objectList.push(new Persion('stone',26));
  objectList.push(new Persion('mandy',23));
  //按年龄从小到大排序
  objectList.sort(
      function(a,b){
          return a.age-b.age
      }
  );
  for(var i=0;i<objectList.length;i++){
    document.writeln('<br />age:'+objectList[i].age+' name:'+objectList[i].name);
}
```

4、简单对象List对可编辑属性的排序

```javascript

var objectList2 = new Array();

function WorkMate(name,age){
    this.name=name;
    var _age=age;
    this.age=function(){
        if(!arguments) { _age=arguments[0];
        } else {
            return _age;
        }
    }

objectList2.push(new WorkMate('jack',20));
objectList2.push(new WorkMate('tony',25));
objectList2.push(new WorkMate('stone',26));
objectList2.push(new WorkMate('mandy',23));

//按年龄从小到大排序

objectList2.sort(
    function(a,b){
        return a.age()-b.age();
     }
 );

for(var i=0;i<objectList2.length;i++){
    document.writeln('<br />age:'+objectList2[i].age()+' name:'+objectList2[i].name);
}

```
