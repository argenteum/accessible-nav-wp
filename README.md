# An accessible menu for WordPress themes
Use and adapt this responsive and accessible menu in your WordPress theme development. 

## Features
* Keyboard navigation using `tab`, `space`, `enter`, and arrow keys
* All elements have ARIA names, roles and attributes

[View demo](https://theme-smith.github.io/accessible-nav-wp/)

## Using in WordPress
1. Download [Font Awesome](http://fontawesome.io/) to your theme's directory
2. Replace 'yourtheme' with your theme's text domain
3. Add this to your HTML where you want the menu to appear
```php
  <?php if (has_nav_menu('primary')) : ?>
  <div class="menu-container">     
    <button class="menu-button"><?php _e('Menu','yourtheme'); ?></button>
      <div id="site-header-menu" class="site-header-menu">
        <nav id="site-navigation" class="main-navigation" role="navigation" aria-label="<?php esc_attr_e('Primary Menu', 'yourtheme'); ?>">
        <?php
          wp_nav_menu(array(
	        'theme_location' => 'primary',
	        'depth'          => 3,
	        ));
        ?>
        </nav>
      </div>
   </div>
  <?php endif; ?>
```
4. Do the following in your theme's `functions.php`
  * [Register the menu](https://codex.wordpress.org/Navigation_Menus)

```php
  function register_my_menu() {
  register_nav_menu('primary',__( 'Primary Menu', 'yourtheme' ));
  }
  add_action( 'init', 'register_my_menu' );
```
  * [Enqueue the script](https://developer.wordpress.org/reference/functions/wp_enqueue_script/) 

```php
  wp_enqueue_script( 'yourtheme-script', get_template_directory_uri() . 'menu.js', array('jquery'), '1.0', true );
```
  * [Localize the script](https://codex.wordpress.org/Function_Reference/wp_localize_script)
   
```php
  wp_localize_script( 'yourtheme-script', 'screenReaderText', array(
	   'expand'   => __( 'Expand child menu', 'yourtheme' ),
	   'collapse' => __( 'Collapse child menu', 'yourtheme' ),
  ));
```
This is optional (if your theme does not need to be [internationalized](https://developer.wordpress.org/themes/functionality/internationalization/)), but if you do not do this, then you need to uncomment this line in `menu.js`:
```javascript
  var screenReaderText = {"expand":"Expand child menu","collapse":"Collapse child menu"};
```
  * [Enqueue Font Awesome stylesheet](https://developer.wordpress.org/reference/functions/wp_enqueue_style/)
```php
  wp_enqueue_style('font-awesome', get_template_directory() . '/font-awesome/font-awesome.css'); 
```
## Using without WordPress
1. [Download Font Awesome](http://fontawesome.io/get-started/) or use the [Font Awesome CDN](https://cdn.fontawesome.com/)
2. Uncomment this line in `menu.js`
```javascript
  var screenReaderText = {"expand":"Expand child menu","collapse":"Collapse child menu"};
```
3. Construct your HTML using this example
```html
  <div class="menu-container">     
    <button class="menu-button">Menu</button>
      <div id="site-header-menu" class="site-header-menu">
        <nav id="site-navigation" class="main-navigation" role="navigation" aria-label="Primary Menu">
          <ul id="menu-main" class="primary-menu">
             <li class="menu-item"><a href="/">Menu-item 1</a></li>
             <li class="menu-item menu-item-has-children"><a href="/">Menu-item 2</a>
               <ul class="sub-menu">
                 <li class="menu-item"><a href="/">Menu-item 2.1</a></li>
                 <li class="menu-item menu-item-has-children"><a href="/">Menu-item 2.2</a>
                   <ul class="sub-menu">
                     <li class="menu-item"><a href="/">Menu-item 2.2.1</a></li>
                     <li class="menu-item"><a href="/">Menu-item 2.2.2</a></li>
                     <li class="menu-item"><a href="/">Menu-item 2.2.3</a></li>
                   </ul></li>
                 <li class="menu-item"><a href="/">Menu-item 2.3</a></li>
                </ul></li>
              <li class="menu-item menu-item-has-children"><a href="#">Menu-item 3</a>
                <ul class="sub-menu">
                  <li class="menu-item menu-item-has-children"><a href="#">Menu-item 3.1</a>
                    <ul class="sub-menu">
                      <li class="menu-item"><a href="/">Menu-item 3.1.1</a></li>
                      <li class="menu-item"><a href="/">Menu-item 3.1.2</a></li>
                      <li class="menu-item"><a href="/">Menu-item 3.1.3</a></li>
                      <li class="menu-item"><a href="/">Menu-item 3.1.4</a></li>
                    </ul></li>
                 </ul></li>
               <li class="menu-item"><a href="/">Menu-item 4</a></li>
            </ul>
          </nav>
       </div>
     </div>
```
