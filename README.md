# 🔌 wp-plugin-boilerplate-pro

> **Production-ready WordPress plugin boilerplate with OOP architecture, REST API endpoints, admin UI, and full test suite.**

[![PHP](https://img.shields.io/badge/PHP-8.1+-777bb4?style=flat&logo=php&logoColor=white)](https://php.net)
[![WordPress](https://img.shields.io/badge/WordPress-6.4+-21759b?style=flat&logo=wordpress&logoColor=white)](https://wordpress.org)
[![PHPUnit](https://img.shields.io/badge/PHPUnit-10.x-366488?style=flat)](https://phpunit.de)
[![License: GPL2](https://img.shields.io/badge/License-GPL2-blue.svg)](LICENSE)

---

## Overview

A battle-tested WordPress plugin boilerplate built for developers who want to skip the scaffolding and start building. Everything is wired up — activation hooks, admin menus, REST endpoints, WP-CLI commands, and a full PHPUnit test suite.

Stop copying and pasting from old projects. Clone this, rename, and ship.

---

## Features

- ✅ OOP architecture with autoloading (PSR-4 via Composer)
- ✅ Custom REST API endpoints with authentication
- ✅ Admin settings page with tabbed UI
- ✅ Custom post types and taxonomies scaffold
- ✅ WP-CLI commands for common operations
- ✅ PHPUnit test suite pre-configured
- ✅ Webpack build pipeline for JS/CSS assets
- ✅ Internationalization (i18n) ready
- ✅ Multisite compatible

---

## Project Structure

```
wp-plugin-boilerplate-pro/
├── includes/
│   ├── class-plugin.php          # Main plugin class
│   ├── class-activator.php       # Activation/deactivation hooks
│   ├── class-deactivator.php
│   ├── admin/
│   │   ├── class-admin.php       # Admin menu and pages
│   │   └── class-settings.php    # Settings API wrapper
│   ├── api/
│   │   ├── class-rest-controller.php  # Base REST controller
│   │   └── endpoints/            # Individual endpoint classes
│   ├── post-types/
│   │   └── class-custom-post-type.php
│   └── cli/
│       └── class-cli-commands.php
├── admin/
│   ├── css/
│   ├── js/
│   └── partials/                 # Admin page templates
├── public/
│   ├── css/
│   └── js/
├── languages/                    # .pot file for translations
├── tests/
│   ├── bootstrap.php
│   └── test-sample.php
├── composer.json
├── package.json
├── webpack.config.js
└── plugin-name.php               # Main plugin file
```

---

## Quick Start

### 1. Clone and rename

```bash
git clone https://github.com/TradeStackDev/wp-plugin-boilerplate-pro.git my-plugin
cd my-plugin

# Run the rename script (replaces all placeholder strings)
php rename.php --name="My Plugin" --slug="my-plugin" --prefix="mp"
```

### 2. Install dependencies

```bash
composer install
npm install
```

### 3. Build assets

```bash
npm run build        # Production build
npm run dev          # Development with watch
```

### 4. Activate

Upload to `/wp-content/plugins/` or symlink for local dev, then activate in WP Admin.

---

## REST API Endpoints

The boilerplate includes a base REST controller you extend:

```php
class My_Endpoint extends REST_Controller {

    public function register_routes() {
        register_rest_route( $this->namespace, '/items', [
            [
                'methods'             => WP_REST_Server::READABLE,
                'callback'            => [ $this, 'get_items' ],
                'permission_callback' => [ $this, 'get_items_permissions_check' ],
                'args'                => $this->get_collection_params(),
            ],
            [
                'methods'             => WP_REST_Server::CREATABLE,
                'callback'            => [ $this, 'create_item' ],
                'permission_callback' => [ $this, 'create_item_permissions_check' ],
            ],
        ] );
    }

    public function get_items( $request ) {
        // Your logic here
        return rest_ensure_response( $data );
    }
}
```

---

## Admin Settings Page

Settings are registered via the WordPress Settings API with a clean tabbed interface:

```php
$settings = new Settings( [
    'tabs' => [
        'general' => [
            'label'  => __( 'General', 'my-plugin' ),
            'fields' => [
                'api_key'   => [ 'type' => 'text', 'label' => 'API Key' ],
                'enable_x'  => [ 'type' => 'checkbox', 'label' => 'Enable Feature X' ],
                'mode'      => [ 'type' => 'select', 'label' => 'Mode', 'options' => ['live', 'test'] ],
            ],
        ],
        'advanced' => [ ... ],
    ],
] );
```

---

## WP-CLI Commands

```bash
# List all plugin items
wp my-plugin items list

# Create a new item
wp my-plugin items create --title="My Item" --status=publish

# Run plugin diagnostics
wp my-plugin doctor

# Flush plugin cache
wp my-plugin cache flush
```

---

## Testing

```bash
# Install WordPress test suite
bash bin/install-wp-tests.sh wordpress_test root '' localhost latest

# Run tests
composer test

# Run with coverage
composer test-coverage
```

---

## Rename Placeholders

The boilerplate uses these strings throughout — the rename script replaces them all:

| Placeholder | Replace With |
|-------------|-------------|
| `Plugin_Name` | Your plugin class name |
| `plugin-name` | Your plugin slug |
| `plugin_name` | Your plugin prefix |
| `PLUGIN_NAME` | Your plugin constant prefix |
| `Your Name` | Your name |
| `yourplugin.com` | Your website |

---

## License

GPL-2.0-or-later © Adam Johnson
