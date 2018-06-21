---
layout: learn
title: The understanding of closure
date: 2018-06-19 15:21:43 +0800
categories: learning
tags: js,closure
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
