# Changelog

All notable changes to the OdooFlow plugin will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- **Pagination for Product Export Modal**: The export modal now supports pagination, allowing users to browse through all WooCommerce products efficiently
  - Configurable page size: 25, 50, or 100 products per page
  - Search functionality to filter products by name or SKU
  - Previous/Next navigation buttons
  - Page indicator showing current page and total pages
  - Selection persistence across pages - selected products remain checked when navigating between pages
- Server-side pagination implementation using `wc_get_products`
- Client-side state management for maintaining product selections across page changes
- Responsive design for pagination controls

### Changed
- Modified `ajax_get_woo_products` handler to accept pagination parameters (page, per_page, search)
- Updated product export modal UI to include search bar and pagination controls
- Enhanced JavaScript to manage pagination state and preserve selections

### Fixed
- Removed the 100-product limit that previously restricted exports to only the first 100 products

## [1.0.2] - Previous Release

### Added
- Order synchronization with Odoo
- Customer import/export functionality
- Product synchronization features

## [1.0.0] - Initial Release

### Added
- Initial plugin release
- Basic Odoo connection settings
- Product import from Odoo to WooCommerce
- Product export from WooCommerce to Odoo
- Customer synchronization
- Secure XML-RPC communication
- Field mapping for products
- Connection testing and validation

[Unreleased]: https://github.com/nouveauxterritoires/odooflow-for-woocommerce/compare/v1.0.2...HEAD
[1.0.2]: https://github.com/nouveauxterritoires/odooflow-for-woocommerce/compare/v1.0.0...v1.0.2
[1.0.0]: https://github.com/nouveauxterritoires/odooflow-for-woocommerce/releases/tag/v1.0.0
