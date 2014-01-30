Assignment 301 02 - Expanding the Child Theme
====================

### This lesson build off of the 301 01 lesson
Please use the same child theme you created for the 301 01 assignment as you will need the files you created to complete this assignment.

### Functions
In this assignment we will be covering the following functions and variables as we add on to the page templates we built in the [first assignment](https://github.com/wpedu/wp301ep01).

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

### Use is_page_template to add a custom field

1. With in the template file content-page.php find the custom field you added and wrap it with an if statement for the template file 'tmp-custom-page-one.php'.

This allows you to utilize a template part file that is used by other theme files and display text that will now only show on this specific template. Before the custom field was visible to all files using that template part.

2. Add get_post_meta to the if statement

Add the get_post_meta to the if statement will ensure that php will only try to echo the results if both conditions exist. This is matter of best practices. You should attempt to wrap code in conditional statements when applicable. There are to many variations to go into them so for now we'll leave that choice up to you.

```

if ( is_page_template('tmp-testing.php') AND get_post_meta( $post->ID, 'secondary-title', true ) ) {
	echo get_post_meta( $post->ID, 'secondary-title', true );
}

```

### Using advanced custom field

As a means to expodite the process of writing your own code for custom metaboxes we are going to introduce a plugin to help you utilize advanced custom fields. 

1. **Advanced Custom Fields** is a plugin build to allow you to add metaboxes to post-types for rapid development. You can download the plugin from the repository here: [http://wordpress.org/plugins/advanced-custom-fields/](http://wordpress.org/plugins/advanced-custom-fields/)

2. Once the plugin is installed please take some time to browse it's admin, and read everything it has to offer. Learning a new plugin with this much power requires reading as well as using.

3. Once you have a handle on what it says it does and it's options create some custom fields for pages. Keep it simple and create the following: Secondary title, Disclaimer text, Secondary featured image

4. Use the functions that come with the plugin to display the fields you have created. 

Using the functions they provide is important. Yes you can work around them and there may be reason with in some project, but for now we will use the functions that come with the plugin to display our new custom fields.

One major reason to always utilize a plugins function is to ensure that your code remains stable with in the confines of the plugin.

You can find the documentation at: [http://www.advancedcustomfields.com/resources/getting-started/displaying-custom-field-values-in-your-theme/](http://www.advancedcustomfields.com/resources/getting-started/displaying-custom-field-values-in-your-theme/)

**Some example code**  
This code is from the documentation page link above. Please always refer to the plugin documentation page as it will be the most up to date examples and code.

```
<?php
get_header();  
?>
 
<div id="primary">
	<div id="content" role="main">
 
		<?php while ( have_posts() ) : the_post(); ?>
 
			<h1><?php the_field('custom_title'); ?></h1>
 
			<img src="<?php the_field('hero_image'); ?>" />
 
			<p><?php the_content(); ?></p>
 
		<?php endwhile; // end of the loop. ?>
 
	</div><!-- #content -->
</div><!-- #primary -->

<?php get_footer(); ?>
```