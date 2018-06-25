---
layout: learn
title: The Understanding of Closure
date: 2018-06-19 15:21:43 +0800
categories: learning
tags: js, closure
keywords: js, closure
---
这篇文章是为了总结一下闭包，以及顺便提一下函数柯里化。

### 闭包
闭包是指有权访问另一个函数作用域中的变量的函数。(Mozilla)[https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures]中说，闭包是指函数以及创建该函数的词法环境组合而成的。这个环境包含了这个闭包创建是所能访问的所有局部变量。

有一个比较有意思的示例是 - makeAdder函数：
{% highlight javascript linenos%}
  function makeAdder(x) {
    return function(y) {
      return x + y;
    };
  }

  var add5 = makeAdder(5);
  var add10 = makeAdder(10);

  console.log(add5(2));  // 7
  console.log(add10(2)); // 12
{% endhighlight %}

从本质上来说，makeAdder(x)是一个函数工厂 - 他创建了将指定的值和它的参数想家求和的函数。<mark>add5</mark>和<mark>add10</mark>都是闭包。他们共享相同的函数定义，但保存了不同的词法环境。
使用只有一个函数的对象可以使用闭包。
下面这段话把面向对象编程和闭包做类比。
> Closures are useful because they let you associate some data (the lexical environment) with a function that operates on that data. This has obvious parallels to object-oriented programming, where objects allow us to associate some data (the object's properties) with one or more methods.

#### 闭包模拟私有方法（模块模式）
JS 可以用闭包来模仿私有方法（private function）的功能。私有方法不仅有利于限制对代码的访问，他们也提供了管理全局命名空间的强大能力，避免了非核心的方法弄乱代码的公共接口。下面这个例子比较有趣。叫做模块模式(module pattern)。

{% highlight javascript linenos%}
  var Counter = (function() {
    var privateCounter = 0;
    function changeBy(val) {
      privateCounter += val;
    }
    return {
      increment: function() {
        changeBy(1);
      },
      decrement: function() {
        changeBy(-1);
      },
      value: function() {
        return privateCounter;
      }
    }
  })();

  console.log(Counter.value()); // logs 0
  Counter.increment();
  Counter.increment();
  console.log(Counter.value()); // logs 2
  Counter.decrement();
  console.log(Counter.value()); // logs 1
{% endhighlight %}

以上的例子中我们创建了一个词法环境让三个函数共享：counter.increment, counter.decrement 和 counter.value。词法环境包含了两个私有item：变量privateCounter和函数changeBy，这从外部无法调用。必须通过匿名函数的三个公共函数使用。每个闭包都是引用自己词法环境中的变量。在一个闭包内对变量的修改不会影响了另一个闭包中的变量。

> Using closures in this way provides a number of benefits that are normally associated with object-oriented programming -- in particular, data hiding and encapsulation.(数据的隐藏和封装)

#### 闭包与变量
作用域链的这种配置机制有一个副作用就是，闭包只能取得包含函数中任何变量的最后一个值。
有一个例子。

{% highlight javascript linenos%}
  function createFunctions() {
    var result = new Array();

    for (var i=0; i < 10; i++) {
      result[i] = function() {
        return i;
      };
    }
    return result;
  }
{% endhighlight %}

这个函数会返回一个函数数组。原本想要实现的功能是把每个函数都返回自己的索引值。但实际上每个函数都返回10。因为每个函数的作用域中都保存在着createFunctions()函数的活动对象，所以他们引用的都是同一个变量i。 当createFunctions()函数返回后，变量i的值是10，此时每个函数都引用着保存变量i的同一个变量对象，所以在每个函数内部i的值都是10。

可以改成下面这样。创建另一个匿名函数强制让闭包行为符合预期。
{% highlight javascript linenos%}
  function createFunctions() {
    var result = new Array();

    for (var i=0; i < 10; i++) {
      result[i] = function(num) {
        return function() {
          return num;
        };
      }(i);
    }
    return result;
  }
{% endhighlight %}

这个重写了的函数相当于在调用每个匿名函数时，我们传入了变量i。由于函数参数是按照值传递的，所以就会将变量i的当前值赋值给参数num。而这个匿名函数的内部又创建并返回了一个nun的闭包。这样result数组的每一个函数都有自己num变量的一个副本，因此也可以返回各自不同的数值了。

#### 关于this对象
在全局函数中，this等于window，而当函数被作为某个对象的方法调用时，this等于那个对象。不过匿名函数的执行环境具有全局性。因此其this对象通常指向window。

this和argument存在同样的问题。如果想访问作用域中的arguments对象，必须将对该对象的引用保存到另一个闭包能访问的变量中。

#### 内存泄露
闭包在ie9以前的版本会导致一些特殊的问题。如果闭包的作用域链中保存着一个html元素。那么意味着该元素将无法被销毁。
下面是个例子。

{% highlight javascript linenos %}
 function assignHandler() {
   var element = document.getElementById("someElement");
   element.onclick = function() {
     alert(element.id);
   };
 }

 //这里创建了一个element的闭包->这个闭包有创建了一个循环引用->所以element占用的内存永远不会被回收。

{% endhighlight %}

可以这么重写。

{% highlight javascript linenos %}
 function assignHandler() {
   var element = document.getElementById("someElement");
   var id = element.id;
   element.onclick = function() {
     alert(id);
   };
   element = null;
 }

 //这里首先把副本保留在变量中，并在闭包中引用该变量消除了循环引用。
 //并且把element变量设置为null来解除对DOM对象的引用，确保正常回收其占用的内存。

{% endhighlight %}

### 模仿块级作用域
JS是没有块级的概念的。在块语句中定义的变量实际上是包含在函数中而非语句中创建的。匿名函数可以用于模仿块级作用域。也就是让变量在执行结束时被销毁。
用作块级作用域（通常称为私有作用域）的匿名函数的语法如下：

{% highlight javascript linenos %}
  (function() {
  //这里是块级作用域
    })();
{% endhighlight %}

以上代码定义并调用了另一个匿名函数。将函数声明包含在一对圆括号中，表示它实际上是一个函数表达式。而紧随其后的另一对圆括号会立即调用这个函数。
这个过程是这样的。

首先，
{% highlight javascript linenos %}
  var someFunction = function() {
    //这里是块级作用域
  };
  someFunction();
{% endhighlight %}
这个例子就是定义一个函数然后立即调用它。定义函数的方式就是创建一个匿名函数，并把它的值付给someFunction这个变量。加圆括号把函数声明转化为函数表达式。函数表达式后面可以跟圆括号来调用它。
这种技术常在全局作用域中被用于函数外部，从而限制向全局作用域中添加过多的变量和函数。

### 性能考虑
如果不是某些特定任务需要使用闭包，在其他函数中创建函数是不明智的，因为他会携带包含它的函数的作用域，因此会比其他函数占用更多的内存。过度使用闭包会导致内存占用过多。在处理速度和内存消耗方面对脚本性能具有负面影响。

比如说，我们在创建一个新的对象或者class的时候，方法应该和object的prototype放在一起而不是直接在构造器里定义。因为如果这样，每次构造器被调用时，方法就会被重新定义一次。比如下面这个例子。
这是错误的。

{% highlight javascript linenos%}
  function MyObject(name, message) {
    this.name =  name.toString();
    this.message = message.toString();
    this.getName = function() {
      return this.name;
    };
    this.getMessage = function() {
      return this.message;
    };
  }
{% endhighlight %}

我们可以重写成这样:

{% highlight javascript linenos%}
  function MyObject(name, message) {
    this.name =  name.toString();
    this.message = message.toString();
  }

  MyObject.prototype = {
    this.getName = function() {
      return this.name;
    },
    this.getMessage = function() {
      return this.message;
    }
  };
{% endhighlight %}

但是重新定义prototype是不推荐的。我们可以写成下面这样。

{% highlight javascript linenos%}
  function MyObject(name, message) {
    this.name =  name.toString();
    this.message = message.toString();
  }

  MyObject.prototype.getName = function() {
    return this.name;
  };

  MyObject.prototype.getMessage = function() {
    return this.message;
  };
{% endhighlight %}
