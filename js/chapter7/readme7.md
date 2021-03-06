###  js权威指南第7章  数组
####数组是值的有序集合。每个值叫做一个元素，而每个元素在数组中有一个位置，以数字表示，称为索引。javascript的数组是无类型的：数组元素可以是任意类型，并且同一个数组中的不同元素也可能有不同的类型。
##### 一 创建数组
使用数组直接量是创建数组最简单的方法，在方括号中将数组元素用逗号隔开即可。例如：  
```javascript
    var empty = [];              // 没有元素的数组
    var arr = [1, 2, 3];         // 有5个数值得数组
    var mix = [1, true, "a"];    // 3个不同类型元素
```
如果省略数组直接量中的某个值，省略的元素将被赋予undefined值。例如：
```javascript
    var count = [1, , 3];        // 数组有3个元素，第二个元素为undefined
```
调用构造函数Array()是创建数组的另一种方法。可以用三种方式：

调用时候没有参数
```javascript
    var a = new Array();
```
调用时有一个数值参数，它指定长度：
```javascript
    var a = new Array(10);
```
显式指定两个或多个数组元素或者数组的一个非数值元素：
```javascript
    var a = new Array(5, 4, 3, " test, test");
```
##### 二 数组长度
每个数组都有一个length属性，就是这个属性区别于常规的js对象。针对稠密数字，length属性值代表数组中元素的个数，其值比数组中最大的所以大1：
```javascript
    [].length                  // => 0: 数组没有元素
    ['a', 'b', 'c'].length     // => 3: 最大的索引为2，length为3
```
为了维持这一原则，数组有两个特殊行为：

1. 如果为一个数组元素赋值，它的索引i大于或等于数组长度时，length属性的值将 设置为i+1
2. 设置length属性为一个小于当前长度非负整数n时，当前数组中那些大于或等于n的元素从中删除。
    ```javascript
        var a = [1, 2, 3, 4];
        a.length = 3;    // 现在a为 [1, 2, 3]
    ```

##### 三 数组元素的添加和删除
push()方法在数组末尾增加一个或多个元素：
```javascript
    var arr = [];              // 创建一个空数组
    arr.push("a");             // 在末尾添加一个元素。arr = ["a"];
```
unshift()方法在数组首部插入一个元素，并且将其他元素依次移到更高的索引处：
```javascript
    var arr = [1, 2 ,3];
    arr.unshift(0);          // 此时arr = [0, 1, 2, 3]
```
pop()方法从末尾删除一个元素，并返回被删除的元素值。
shift()方法从数组头部删除一个元素。

##### 四 数组遍历
一般使用for循环来遍历数组元素。例如
```javascript
    var arr = [1, 2, 3];
    for(var i=0, len= arr.length; i<len; ++) {
        // 循环体
    }
```
#### 五 数组方法
1. join()

    Array.join()方法将数组中所有元素都转化为字符串并连接在一起，返回最后生成的字符串。如果不指定分隔符，默认使用逗号。
    ```javascript
        var a = [1, 2, 3];
        a.join();         // => "1,2,3"
        a.join(" ");      // => "1 2 3"
        a.join("");       // => "123"
    ```
    Array.join()与String.split()方法的逆向操作，后者是将字符串分割成数组。

2. reverse()
    
    Array.reverse()方法将数组中的元素颠倒顺序，返回逆向数组。例如：
    ```javascript
        var a = [1, 2, 3];
        a.reverse();     // => [3, 2, 1]
    ```

3. sort()
    
    Array.sort()将数组中的元素排序并返回排序后的数组。当不带参数调用sort()时，数组元素以字母表顺序排序。
    ```javascript
        var arr = ["banana", "cherry", "apple"];
        a.sort();                    // a = ["apple", "banana", "cherry"]
    ```
    如果数组中包含undefined元素，它们会被排到数组的尾部。更多例子在index.js中。

4. concat()
    
    Array.concat()创建并返回一个新数组，它的元素包括调用concat()的原始数组的元素和concat()的每个参数。如果这些参数中的任何一个自身是数组，则连接的是数组的元素，而非数组本身。
    ```javascript
        var a = [1, 2, 3];
        a.concat(4,5)                    // => [1,2,3,4,5]
        a.concat([4,5], [6,7]);          // => [1,2,3,4,5,6,7]
    ```
5. slice()

    Array.sliece方法返回指定数组的一个片段或者子数组。它的两个参数分别制定了片段的开始和结束位置。返回的数组包含第一个参数指定的位置和所有到但不包含第二个参数指定位置之间的所有数组元素。如果只指定一个参数，返回的数组将包含从开始位置到数组结尾的所有元素。
    ```javascript
        var a = [1,2,3,4,5];
        a.slice(0, 3);       // => [1,2,3]
        a.sliece(3);         // => [4,5]
    ```
6. splice()
    
    Array.splice()在数组中插入或删除元素的通用方法。第一个参数制定了插入或者删除的起始位置，第二个参数制定了应该从数组中删除的元素个数，如果省略第二个参数，从起始位置到结尾的所有元素都将被删除。返回一个由删除元素组成的数组。
例如：
    ```javascript
        var _arr = [1, 2, 3, 4, 5, 6, 7, 8];
        _arr.splice(4);
        console.log(_arr);
        // 返回[5, 6, 7, 8];_arr是[1,2,3,4]
        _arr.splice(1, 2);
        console.log(_arr);
        // 返回[2, 3];_arr是[1,4]
    ```
    splice()的前两个参数制定了需要删除数组元素。后面的任意个数的参数指定了需要插入到数组中的元素，从第一个参数指定的位置开始插入。

    ```javascript
        var a = [1, 2, 3, 4, 5];
        a.splice(2, 0 , 'a', 'b');               // 返回[],a = [1, 2, 'a', 'b', 3, 4, 5];
        a.splice(2, 2, [1,2], 3);                // 返回['a','b'],a = [1,2,[1,2],3,3,4,5];
    ```
    注意：区别于concat(),splice()会插入数组本身而非数组的元素。
    
7. push()和pop():

    push()在数组尾部添加一个或多个元素，并返回数组新的长度。
    
    pop()删除数组的最后一个元素，减小数组长度并返回它删除的值。

8. unshift()和shift()
    
    unshift()在数组的头部添加一个或多个元素，并将已存在的元素移到更高索引的位置来获得足够的空间，最后返回数组新的长度。
    
    shift()删除数组的第一个元素并将其返回，然后把所有随后的元素下移一个位置来填补头部的空缺。
    
#####六 ECMAScript 5中的数组方法

1. forEach()
    
    从头到尾遍历数组，为每个元素调用指定的函数。使用三个参数调用该函数：数组元素、数组元素索引和数组本身。
    ```javascript
        var data = [1,2,3,4,5];
        var sum = 0;
        data.forEach(function(value){
            sum += value;
        });
        console.log(sum);    // => 15
    ```
2. map()

    将调用的数组的每个元素传递给指定的函数，并返回一个数组，它包含该函数的返回值。例如：
    ```javascript
        var a_arr = [1, 2, 3];
        var b = a_arr.map(function(x){
            return x*x;
        })
        console.log(b);  // =>b = [1, 4, 9]
    ```
3. filter()
    
    filter()方法返回的数组元素是调用的数组的一个子元素。传递的函数是用来逻辑判定的：该函数返回true或false。

    ```javascript
        var a = [1,2,3,4,5];
        var smalls = a.filter(function(x){
            return x < 3;
        });
        // => smalls = [1,2]
    ```
    
4. every()和some()

    every()和some()方法是数组的逻辑判定：它们对数组元素应用指定的函数进行判定，返回true或false。
    
    every()针对数组中的所有元素调用判定函数都返回true，它才返回true。
    
    somt()数组中只杀有一个元素调用函数判定返回true，它就返回true。
    
    注意：一旦every()和some()确认该返回什么值它们就会停止遍历数组元素。
    
5. reduce()和reduceRight()

    reduce()和reduceRight()方法使用指定的函数将数组元素进行组合，生成单个值。
    ```javascript
        var _data = [1,2,3,4,5];
        var sum = _data.reduce(function (x, y) {
           return x+y;
        }, 0);
        // 求和 => 15
        var product = a.reduce(function (x, y) {
            return x*y;
        }, 1);
        // 求积 => 120
        var max = a.reduce(function (x, y) {
           return x>y ? x : y;
        });
        // 求最大值 => 5
    ```
    
    reduceRight()工作原理和reduce()一样，不同的是它按照数组索引从高到低处理数组。
    
6. indexOf()和lastIndexOf()  

    搜索整个数组红具有给定值的元素，返回找的第一份元素的索引或者如果没有找到就返回-1。indexOf()从头至尾搜索，lastIndexOf()则反向搜索。例如：
    
    ```javascript
        var a = [0, 1, 2, 1, 0];
        a.indexOf(1);         // => 1
        a.lastIndexOf(1);     // => 3
        a.indexOf(3);         // => -1      
    ```

##### 七 数组类型
使用Array.isArray()函数来判断是否为数组。
```javascript
    Array.isArray([]);            // => true
    Array.isArray({});            // => false
```
    
    