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

A very good reference could be [this one](https://www.drupal.org/forum/support/module-development-and-code-questions/2016-04-12/open-modal-pop-up-form-from-a-view) as well as [this one ](https://www.drupal.org/project/ctools/issues/1209472)

In the happy.module, the code are following:

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


  function _custom_page_callback($js = NULL, $nid = NULL)
  {


    //Include ctools iff path contains 'nojs' to work, else render page normally
    if($js)
    {
      ctools_include('modal');
      ctools_include('ajax');
      ctools_modal_add_js(); //Default CTools JS. This is a must if custom javascript is not available.

    }

    $form_state = array(
      'title' => 'this is a form',
      'ajax' => TRUE
    );

    $output = ctools_modal_form_wrapper('happy_form', $form_state);
    print ajax_render($output);
    exit;

  }
  
{% endhighlight %}


In the happy.inc, the code are:

{% highlight php linenos %}

function happy_form($form, &$form_state){
  $form['name'] = array(
    '#type' => 'textfield',
    '#title' => 'name',
    '#required' => TRUE,
  );

  $form['mobile'] = array(
    '#type' => 'textfield',
    '#title' => 'mobile',
    '#required' => TRUE,
  );

  $form['submit_button'] = array(
    '#type' => 'submit',
    '#value' => t('Click Here!'),
  );

  return $form;
}

function myform_form_validate($form, &$form_state) {
}

function myform_form_submit($form, &$form_state) {
}


{% endhighlight %}
