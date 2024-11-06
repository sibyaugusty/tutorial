# Tutorial

# Building a WordPress Theme from Scratch

An end-to-end guide on creating a custom WordPress theme, covering setup, file structure, creating templates, and adding dynamic functionality with PHP.

## 1. Initial Setup
- **Install WordPress**: [WordPress Download](https://wordpress.org/download/)
- **Set Up Development Environment**: Use tools like XAMPP, WAMP, or Local by Flywheel.

![WordPress Installation Screenshot](images/wordpress-setup.png)

## 2. Basic File Structure

Create the following essential files inside your theme folder (`my-custom-theme`):


### File Descriptions

- **style.css**: This file contains the theme metadata and custom CSS styles. It’s required for WordPress to recognize the theme.
- **index.php**: The main template file that WordPress will fall back on if no other templates are available.
- **functions.php**: Used to add theme functions, enqueue styles and scripts, register menus, and more.
- **header.php**: Contains the `<head>` section and opening HTML tags. Included at the top of other template files.
- **footer.php**: Contains the closing HTML tags and is included at the bottom of other template files.
- **sidebar.php**: Sidebar template, often used to display widgets.
- **single.php**: Template for individual blog post pages.
- **page.php**: Template for static pages.
- **archive.php**: Template for category, tag, and date archive pages.

# Basic WordPress Theme File Structure and Content

In this section, you’ll find a description and sample code for each essential file in a WordPress theme.

---

## File: `style.css`

The `style.css` file contains theme metadata and styles. The metadata at the top is required for WordPress to recognize the theme.

```css
/*
Theme Name: My Custom Theme
Theme URI: http://yourwebsite.com
Author: Your Name
Author URI: http://yourwebsite.com
Description: A custom WordPress theme built from scratch
Version: 1.0
License: GNU General Public License v2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html
Text Domain: my-custom-theme
*/




