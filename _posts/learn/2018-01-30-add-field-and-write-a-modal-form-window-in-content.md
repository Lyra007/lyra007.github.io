---
layout: learn
title: add field and write a modal form window in content
date: 2018-01-30 23:26:27 +0800
categories: learning
tags: drupal, form, modal window
keywords: jnjdemo,drupal,form
---

# add field and write a modal form window in content


## Module:

	* entity reference

### Need two content type to achieve this-write a modal form window in content
A is the one to display content and have a link linking to a modal form window
B is the one that stores form info which includes information submited by form

Basic steps could be:
1. Add an extra field in B with field type called entity reference and with widget called autocomplete (in order to bind A with B using node id)
2. Write code to add field which could be viewed in <mark>Manage Display</mark>
	* Use <mark>hook_field_extra_fields()</mark> and <mark>hook_node_view()</mark> to add extra field
	* In <mark>hook_node_view()</mark>, <mark>ctools_modal_text_button</mark> can be used to be the link inside the content
3. <mark>ctools_modal_text_button</mark> and <mark>ctools_modal_form_wrapper</mark> could be used to make a modal window
4. <mark>hook_menu()</mark> and a callback function are needed.
5. <mark>modal/form-modal/%ctools_js/%</mark> and <mark>modal/form-modal/nojs/' . $node->nid</mark> could be combined using 
6. submition could use <mark>entity_create</mark>, <mark>entity_metadata_wrapper</mark> as well as <mark> save</mark>.

## add more form 
- Basically, add more form is a form that has ability to add more rows and remove unwanted rows
- it use ajax to submit features

* The way using ajax to submit:

{% highlight php linenos %}

  $form['info_fieldset']['add_row'] = array(
    '#type' => 'submit',
    '#value' => t('增加一组'),
    '#limit_validation_errors' => array(),       // No validation.
    '#submit' => array('add_row_add_one'),
    '#ajax' => array(
      'callback' => 'addone_callback',
      'wrapper' => 'info-fieldset-wrapper',
    ),
  );

{% endhighlight %}

* The way using normal submit to submit:

{% highlight php linenos %}

  $form['submit_button'] = array(
    '#type' => 'submit',
    '#value' => t('提交报名!'),
  );

{% endhighlight %}

There should be an ajax key in the array of submit

Also, we use tree to build different field with same values.

  <mark> $form['#tree'] = TRUE </mark>


