---
layout: learn
title: add modal window for form from links in view
date: 2018-01-29 23:17:01 +0800
categories: learning
tags: drupal,views,form
keywords: jnjdemo,modal window, form,drupal
---

# add modal window for form from links in view

Spent so much time on investing this > <

{% highlight php linenos %}


//hook menu

  function happy_menu()
  {
  $items['modal/%ctools_js/%'] = array(
    'title' => 'Title of Modal',
    'page arguments' => array(1, 2), //Pass whether to use AJAX or JS and the nid
    'page callback' => '_custom_page_callback', //User defined function called when the link is clicked
    'access callback' => TRUE,
    'file' => 'happy.inc',
    'type' => MENU_NORMAL_ITEM, //Internal path menu, not a menu tab
  );
    return $items;
  }

{% endhighlight %}
