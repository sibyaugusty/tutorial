# Tutorial

# Building a WordPress Theme from Scratch

# Main Concepts of WordPress Themes

A WordPress theme controls the look, layout, and style of your website. Themes use a combination of PHP, HTML, CSS, and JavaScript to manage how content is displayed. Some primary aspects include:

-- **Template Files**: Define the structure of different parts of your website (like header, footer, homepage).
Styles: Control the appearance of the site (colors, fonts, layout).

-- **Functions**: Handle the logic, add support for different features, and enable interaction between WordPress and your theme.

An end-to-end guide on creating a custom WordPress theme, covering setup, file structure, creating templates, and adding dynamic functionality with PHP.

## 1. Initial Setup
- **Install WordPress**: [WordPress Download](https:wordpress.org/download/)
- **Set Up Development Environment**: Use tools like XAMPP, WAMP, or Local by Flywheel.

![WordPress Installation Screenshot](images/wordpress-setup.png)

## 2. Necessary Directories and Files
   
  In a custom theme, certain files and folders are essential. WordPress looks for specific files to recognize it as a valid theme:
  
  -- **style.css**: This is the primary stylesheet for your theme, which also contains metadata about the theme.
  
  -- **index.php**: The main template file; it’s required and serves as a fallback for any missing templates.
  
  -- **functions**.php: This file adds functionality, registers assets (like CSS and JS files), and enables theme features.
  
  -- **screenshot.png**: An optional image displayed in the WordPress theme selector.
  
    
  Additional files and folders may include:
  
  -- **header.php**: Defines the header section.
  
  -- **footer.php**: Defines the footer section.
  
  -- **sidebar.php**: Contains sidebar widgets or links.

  -- **page.php**: Template for static pages.
  
  -- **single.php**: Template for individual blog posts.
  

## 3. File and Folder Explanation with Examples

## File: `style.css`

The `style.css` file contains theme metadata and styles. The metadata at the top is required for WordPress to recognize the theme.

```css
/*
Theme Name: My Custom Theme
Theme URI: http:yourwebsite.com
Author: Your Name
Author URI: http:yourwebsite.com
Description: A custom WordPress theme built from scratch
Version: 1.0
License: GNU General Public License v2 or later
License URI: http:www.gnu.org/licenses/gpl-2.0.html
Text Domain: my-custom-theme
*/
```

## File: `index.php`
  This is the main template file for rendering content if other specific templates aren’t available
  
```css
<?php get_header(); ?>
<main>
    <?php if ( have_posts() ) : while ( have_posts() ) : the_post(); ?>
        <h2><?php the_title(); ?></h2>
        <?php the_content(); ?>
    <?php endwhile; endif; ?>
</main>
<?php get_footer(); ?>
```

## File: functions.php

This file is essential for adding theme support, registering menus, and including scripts or styles. Example:

```css
<?php
function mytheme_setup() {
    /* Enable support for Post Thumbnails*/
    add_theme_support('post-thumbnails');

    /* Register a navigation menu*/
    register_nav_menus(array(
        'primary' => 'Primary Menu',
    ));
}
add_action('after_setup_theme', 'mytheme_setup');

```

## 4. Organizing CSS, JS, and Images in an "assets" Folder ( optional put css and js but better if using a order for everything ) 

To create an assets folder, simply organize it within your theme’s directory like this:

``` css 
my-theme/
|-- assets/
|   |-- css/
|   |-- js/
|   |-- images/
|-- style.css
|-- index.php
|-- functions.php
```
## To load these files, use functions.php:

```css
<?php
function mytheme_enqueue_assets() {
    wp_enqueue_style('main-style', get_template_directory_uri() . '/assets/css/style.css');
    wp_enqueue_script('main-script', get_template_directory_uri() . '/assets/js/script.js', array(), false, true);
}
add_action('wp_enqueue_scripts', 'mytheme_enqueue_assets');

```
## 5. Basic Functionalities of a Theme

Custom theme’s functionalities are managed through functions.php. 
Key features include:

- **Menus**: Register navigation menus with register_nav_menus.
- **Widgets**: Register widget areas with register_sidebar.
- **Custom Logo**: Enable theme support for custom logos.
- **Post Formats**: Add support for post formats (like gallery, video, etc.).

## Here’s how to add support for these in functions.php

```css
<?php
function mytheme_basic_functions() {
    /* Enable custom logo support*/
    add_theme_support('custom-logo');

    /* Register widget area*/
    register_sidebar(array(
        'name' => 'Sidebar',
        'id' => 'sidebar-1',
        'description' => 'Widgets in this area will be shown in the sidebar.',
    ));
}
add_action('after_setup_theme', 'mytheme_basic_functions');
```

## 6. Other Necessary Files

-- **header.php**: Contains code for the top section of your website (navigation, logo).

-- **footer.php**: Contains code for the bottom section (footer widgets, copyright).

-- **sidebar.php**: Holds the sidebar section, where widgets are typically placed.

-- **page.php**: Template for static pages, like “About” or “Contact.”

-- **single.php**: Template for individual blog posts.

-- **archive.php**: Template for archive pages (categories, tags).

-- **search.php**: Template for search results.


## 1. header.php
   
The header.php file is responsible for the top part of your theme that appears on every page—usually the logo, navigation menu, and site title. This file is called at the top of each template to display a consistent header across the site.

Typical Contents of header.php:

The doctype declaration, meta tags, and links to CSS or JavaScript files.
Site logo and navigation menu.
Any other elements you want to appear consistently at the top.

```css
<!DOCTYPE html>
<html <?php language_attributes(); ?>>
<head>
    <meta charset="<?php bloginfo( 'charset' ); ?>">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <?php wp_head(); ?>
</head>
<body <?php body_class(); ?>>
    <header>
        <div class="site-logo">
            <?php the_custom_logo(); ?>
        </div>
        <nav class="main-nav">
            <?php
            wp_nav_menu(array(
                'theme_location' => 'primary',
                'container' => false,
            ));
            ?>
        </nav>
    </header>
```

## 2. footer.php
   
The footer.php file contains the bottom section of your theme and is generally used to display copyright information, links to privacy policies, and footer widgets.

Typical Contents of footer.php:

Copyright text.
Footer navigation or links.
Social media icons.
Calls to wp_footer(), which loads necessary WordPress scripts.

```css
<footer>
    <div class="footer-widgets">
        <?php if ( is_active_sidebar( 'footer-1' ) ) : ?>
            <?php dynamic_sidebar( 'footer-1' ); ?>
        <?php endif; ?>
    </div>
    <div class="site-info">
        <p>&copy; <?php echo date('Y'); ?> My Custom Theme. All rights reserved.</p>
    </div>
    <?php wp_footer(); ?>
</footer>
</body>
</html>
```

## 3. sidebar.php
   
The sidebar.php file is used for adding a sidebar to your theme. Sidebars commonly contain widgets like recent posts, categories, and search bars. You can place this file on pages where you want a sidebar, like blog or archive pages.

Typical Contents of sidebar.php:

Widgets registered in WordPress.
Search bar.
Links to recent posts, categories, and more.

```css
<aside class="sidebar">
    <?php if ( is_active_sidebar( 'sidebar-1' ) ) : ?>
         /* Display widgets assigned to sidebar-1*/
        <?php dynamic_sidebar( 'sidebar-1' ); ?>
    <?php else : ?>
        <p>Add widgets in the WordPress dashboard to appear here.</p>
    <?php endif; ?>
</aside>
```

## 4. page.php
   
The page.php file is a template used for static pages (like “About Us” or “Contact”). This template is generally less complex than the blog template (single.php) because static pages typically don’t include post dates, categories, or tags.

Typical Contents of page.php:

Displays the title and content of the page.
Basic layout without elements specific to posts (e.g., no categories or comments).

```css
<?php get_header(); ?>
<main>
    <?php if ( have_posts() ) : while ( have_posts() ) : the_post(); ?>
        <h1><?php the_title(); ?></h1>
        <div class="page-content">
            <?php the_content(); ?>
        </div>
    <?php endwhile; endif; ?>
</main>
<?php get_footer(); ?>
```

## 5. single.php
   
The single.php file is the template for individual blog posts. This is where you show the post title, date, author, categories, tags, content, and comment section.

Typical Contents of single.php:

Post title, content, and metadata (like date, author, and categories).
Comment section if comments are enabled.

```css
<?php get_header(); ?>
<main>
    <?php if ( have_posts() ) : while ( have_posts() ) : the_post(); ?>
        <h1><?php the_title(); ?></h1>
        <div class="post-meta">
            <span>Posted on <?php the_date(); ?> by <?php the_author(); ?></span>
            <span>Category: <?php the_category(', '); ?></span>
        </div>
        <div class="post-content">
            <?php the_content(); ?>
        </div>
        <?php comments_template(); ?>
    <?php endwhile; endif; ?>
</main>
<?php get_footer(); ?>
```

## 6. archive.php
   
The archive.php file is used to display a list of posts based on specific criteria, such as categories, tags, or authors. For example, when a user views all posts under a category, WordPress will use this template.

Typical Contents of archive.php:

A loop that displays excerpts of posts.
Metadata like post dates, categories, and authors.

```css
<?php get_header(); ?>
<main>
      /* Displays the category name*/
    <h1><?php single_cat_title(); ?></h1>
    <?php if ( have_posts() ) : while ( have_posts() ) : the_post(); ?>
        <article>
            <h2><a href="<?php the_permalink(); ?>"><?php the_title(); ?></a></h2>
            <div class="post-excerpt">
                <?php the_excerpt(); ?>
            </div>
        </article>
    <?php endwhile; else : ?>
        <p>No posts found.</p>
    <?php endif; ?>
</main>
<?php get_footer(); ?>
```

## 7. search.php
   
The search.php file is used to display search results when a user performs a search on your site. It lists posts or pages that match the search query.

Typical Contents of search.php:

The search query.
A loop to display relevant posts or pages.

```css
<?php get_header(); ?>
<main>
    <h1>Search Results for: <?php echo get_search_query(); ?></h1>
    <?php if ( have_posts() ) : while ( have_posts() ) : the_post(); ?>
        <article>
            <h2><a href="<?php the_permalink(); ?>"><?php the_title(); ?></a></h2>
            <div class="post-excerpt">
                <?php the_excerpt(); ?>
            </div>
        </article>
    <?php endwhile; else : ?>
        <p>No results found for "<?php echo get_search_query(); ?>".</p>
    <?php endif; ?>
</main>
<?php get_footer(); ?>
```

## Advanced Optional
## Adding Customizer for custom theme

-- The WordPress Customizer is a feature in WordPress that allows users to modify various aspects of their theme and see these changes in real-time before they’re published. When you add options to the Customizer, you’re enabling theme users to adjust settings like colors, logos, fonts, or layouts easily through the WordPress dashboard.

-- **Where to Access the Customizer**
To see and use the Customizer, go to your WordPress dashboard:

-- **Go to Appearance > Customize**
This opens the Customizer panel, where you’ll see sections and controls based on the options you’ve defined in your theme.
The settings you add to the Customizer (like colors, layout options, etc.) will show up as panels, sections, or individual controls on the left side. As you make changes, the preview on the right will update in real time, allowing you to see how the adjustments affect your site.

Example of Adding a Custom Color Option to the Customizer
Let’s walk through an example of adding a color setting for the header background in the Customizer.

Add Code to functions.php

In your theme’s **functions.php**, add this code:

```css
function mytheme_customize_register($wp_customize) {
    /* Add a new section in the Customizer*/
    $wp_customize->add_section('mytheme_colors', array(
        'title' => __('Theme Colors'),
        'description' => 'Customize theme colors',
        'priority' => 30,
    ));

    /* Add setting for the header background color*/
    $wp_customize->add_setting('mytheme_header_color', array(
        'default' => '#333',
        'sanitize_callback' => 'sanitize_hex_color',
    ));

    /* Add control for the header background color*/
    $wp_customize->add_control(new WP_Customize_Color_Control(
        $wp_customize,
        'mytheme_header_color',
        array(
            'label' => 'Header Background Color',
            'section' => 'mytheme_colors',
            'settings' => 'mytheme_header_color',
        )
    ));
}
add_action('customize_register', 'mytheme_customize_register');
```

Use the Setting in Your Theme Files

Once you have registered this setting, you’ll need to use it in your theme to see the effect. For example, let’s apply the header color in header.php:

```css
<header style="background-color: <?php echo get_theme_mod('mytheme_header_color', '#333'); ?>;">
    /*<!-- Header content here -->*/
</header>
```

Here, get_theme_mod('mytheme_header_color', '#333') fetches the color selected in the Customizer. The second argument, '#333', is the default color if no selection is made.

Go to the Customizer to See the Change

After adding this code, go to **Appearance > Customize** in your WordPress dashboard.
Find the **Theme Colors** section, where you should now see an option to select the Header Background Color.
Select a new color, and you’ll see the header background update in real time in the Customizer preview.
