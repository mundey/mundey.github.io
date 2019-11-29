---
published: false
layout: post
title: Woocommerce Storefront
categories: woocommerce
tags: woocommerce wordpress
author: Jags
---
## Checklist
- Cleanup: Delete all posts, pages, plugins, all themes except one
- General Settings:
    - Set Site Title, Purpose
    - Settings/Permalinks Change pages url: category/postname
- Permissions:
    - Ensure ro permissions once site is configured correctly
    - htaccess
        - no browsing
        - no display access to wp-config.php
        - http to https
        - htpasswd for dev and stg sites
        
## Plugins to install
- Woocommerce (Woocommerce admin, Woocommerce services, Jetpack)
- UI
    - Extras
        - Storefront add slider, Slider ultimate
    - Essentials
        - Homepage Control
- Functionality
    - Contact us Form
        - WPForms

## Astra Based (Step by Step)
- Install Theme: 
    - Astra
    - Activate
- Install Plugin: 
    - Astra Starter sites
        - Use Elementor
        - Import a starter site which will install required plugins, theme
    - Woo Bottom Bar

- Customize
    - Site Slogan
    - Site Logo: 
      - website logomakr.com
      - searhed by "art"
      - Font: Amaranth
    - Site Footer: WP Theme Customize global header/footer
      - Logo
      - Social Icons: Set for FB, IG. Remove rest
      - Some other Text
    


## Switch Between dev, stg, prd