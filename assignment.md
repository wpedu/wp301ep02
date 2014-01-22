Assignment 301 02 - Expanding the Child Theme
====================

In this assignment we will be coving the following functions and variables as we add on to the page templates we built in the [first assignment](https://github.com/wpedu/wp301ep01).

- [get_template_part()](http://codex.wordpress.org/Function_Reference/get_template_part)
- [is_page_template()](http://codex.wordpress.org/Function_Reference/is_page_template)
- [have_posts() - $wp_query](http://codex.wordpress.org/Function_Reference/have_posts)
- [the_post() - $post](http://codex.wordpress.org/Function_Reference/the_post)

Step 1: Create a testing area from a template page
------------------

Now that you have your child theme running and some custom page templates we have a place we can make some modifications. Templates are a little like a playground of sorts.

1. Create a new page template file and name it "tmp-testing.php". This file will be blank apart from the necessary opening <?php tag and the php comment to signify it is a template page.

```
<?php
/* Template Name: Testing Page */
?>
```

2. Create a new page in the wp-admin and set it to private. Give it the name "Testing Code". _We set the page to private so that only logged in admins can see it even though we are already in a save environment it is a good habit to be in when using test template pages like this._
3. Visit the page blank page. _Of course there is nothing there, the page is blank._
4. Open up the tmp-testing.php file and add the following line of code below the commented template name.

```
<?php
/* Template Name: Testing Page */
print_r($wp_query);
?>
```

This will print out all the values within the $wp_query variable. 

### Why did we do this?

The goal using a testing template is to allow you to try new code in an environment that is free from all other possible errors, html, design and a number of other factors that _may_ interrupt with your test.

Keep in mind that you are technically on a "page" so your actual query is will always be that of the testing page.

**As you run through future assignment** you may need a testing place to try out code and now you have it.

Step 2: is_page_template()
--------------------

The function [is_page_template()](http://codex.wordpress.org/Function_Reference/is_page_template) is a very handy function when dealing with page templates. It will allow you to check if the page you are on is using the page template you are looking for.

```
<?php
/* Template Name: Testing Page */

if ( is_page_template('tmp-testing.php') ) {
	echo 'yes this is the tmp-testing.php file';
}

?>
```

You may ask, "When would I need this? Wouldn't I always know what specific page template I'm using?". Through out your project you may need to reuse php files with in multiple page templates, and with in some of those files you may need code that should not exist on specific page templates.

We'll combined [is_page_template()](http://codex.wordpress.org/Function_Reference/is_page_template) with [get_template_part()](http://codex.wordpress.org/Function_Reference/get_template_part) in a later step.