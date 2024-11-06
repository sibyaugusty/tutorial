# tut

# Building a WordPress Theme from Scratch

An end-to-end guide on creating a custom WordPress theme, covering setup, file structure, creating templates, and adding dynamic functionality with PHP.

## 1. Initial Setup
- **Install WordPress**: [WordPress Download](https://wordpress.org/download/)
- **Set Up Development Environment**: Use tools like XAMPP, WAMP, or Local by Flywheel.

![WordPress Installation Screenshot](images/wordpress-setup.png)

## 2. Basic File Structure
Create essential files in your theme folder:
- `style.css`
- `index.php`
- `functions.php`

![Theme Folder Structure](images/theme-structure.png)

## 3. Enqueue Styles and Scripts
To enqueue files, add the following to `functions.php`:

```php
function my_custom_theme_scripts() {
    wp_enqueue_style('style', get_stylesheet_uri());
    wp_enqueue_script('script', get_template_directory_uri() . '/js/script.js', array(), '1.0.0', true);
}
add_action('wp_enqueue_scripts', 'my_custom_theme_scripts');
