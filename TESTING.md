# Testing Guide - Pagination Feature for Product Export Modal

## Overview
This guide provides instructions for testing the new pagination feature implemented for the WooCommerce product export modal.

## Prerequisites
- WordPress installation with WooCommerce active
- OdooFlow plugin installed and activated
- Odoo connection configured
- Test store with products (ideally 100+ products for thorough testing)

## Test Scenarios

### 1. Basic Pagination Functionality

#### Test 1.1: Modal Opening
**Steps:**
1. Navigate to Products > All Products in WordPress admin
2. Click the "Export to Odoo" button
3. Verify the modal opens

**Expected Result:**
- Modal opens successfully
- First 25 products are displayed (default per_page)
- Search bar is visible
- Per-page selector shows "25" selected
- Pagination controls are visible (if more than 25 products exist)
- Page indicator shows "1 / X" where X is total pages

#### Test 1.2: Next Page Navigation
**Steps:**
1. Open the export modal
2. Click the "Next" button

**Expected Result:**
- Products from page 2 are loaded
- Page indicator updates to "2 / X"
- "Previous" button is now enabled
- "Next" button is disabled if on last page
- Loading spinner appears briefly during load

#### Test 1.3: Previous Page Navigation
**Steps:**
1. Navigate to page 2 or later
2. Click the "Previous" button

**Expected Result:**
- Products from previous page are loaded
- Page indicator decrements
- "Previous" button is disabled if on page 1
- Loading spinner appears briefly during load

### 2. Per-Page Selector

#### Test 2.1: Change to 50 Products Per Page
**Steps:**
1. Open the export modal
2. Select "50" from the per-page dropdown

**Expected Result:**
- Modal reloads with 50 products per page
- Returns to page 1
- Total pages calculation updates
- Previously selected products remain selected

#### Test 2.2: Change to 100 Products Per Page
**Steps:**
1. Open the export modal
2. Select "100" from the per-page dropdown

**Expected Result:**
- Modal reloads with 100 products per page
- Returns to page 1
- Total pages calculation updates
- Previously selected products remain selected

### 3. Search Functionality

#### Test 3.1: Search by Product Name
**Steps:**
1. Open the export modal
2. Type a product name in the search box
3. Wait 500ms for debounce

**Expected Result:**
- Products list filters to show matching products
- Page resets to 1
- Total count updates to match search results
- Pagination adjusts for filtered results
- "No products found" message appears if no matches

#### Test 3.2: Search by SKU
**Steps:**
1. Open the export modal
2. Type a product SKU in the search box
3. Wait 500ms for debounce

**Expected Result:**
- Products list filters to show matching products
- Page resets to 1
- Total count updates accordingly

#### Test 3.3: Clear Search
**Steps:**
1. Perform a search
2. Clear the search box
3. Wait 500ms

**Expected Result:**
- All products are displayed again
- Returns to page 1
- Total count shows all products

### 4. Selection Persistence

#### Test 4.1: Select Products on Multiple Pages
**Steps:**
1. Open the export modal
2. Select 3 products on page 1
3. Navigate to page 2
4. Select 2 products on page 2
5. Navigate back to page 1

**Expected Result:**
- The 3 products selected on page 1 are still checked
- Navigate to page 2 again
- The 2 products selected on page 2 are still checked
- Total selection count: 5 products

#### Test 4.2: Deselect Products Across Pages
**Steps:**
1. Select products on pages 1 and 2
2. Navigate to page 1
3. Deselect 1 product
4. Navigate to page 2
5. Navigate back to page 1

**Expected Result:**
- Deselected product remains unchecked
- Other selections remain checked

#### Test 4.3: Select All on Current Page
**Steps:**
1. Open the export modal
2. Click the "Select All Products" button

**Expected Result:**
- All products on current page are selected
- Checkboxes are checked
- Products are added to selection state

#### Test 4.4: Deselect All on Current Page
**Steps:**
1. Select some products
2. Click the "Deselect All Products" button

**Expected Result:**
- All products on current page are deselected
- Checkboxes are unchecked
- Products are removed from selection state

### 5. Export Functionality

#### Test 5.1: Export Products from Single Page
**Steps:**
1. Open the export modal
2. Select 5 products from page 1
3. Click "Export Selected Products"

**Expected Result:**
- Export process starts
- Success/failure message appears
- Modal closes on success
- Selected products are exported to Odoo

#### Test 5.2: Export Products from Multiple Pages
**Steps:**
1. Open the export modal
2. Select 3 products from page 1
3. Navigate to page 2
4. Select 2 products from page 2
5. Click "Export Selected Products"

**Expected Result:**
- All 5 selected products are exported
- Success message confirms export
- Modal closes on success

#### Test 5.3: Export with No Selection
**Steps:**
1. Open the export modal
2. Don't select any products
3. Click "Export Selected Products"

**Expected Result:**
- Alert message: "Please select at least one product to export"
- Export does not proceed
- Modal remains open

### 6. Performance Testing

#### Test 6.1: Large Product Catalog (1000+ products)
**Steps:**
1. Create or import 1000+ products
2. Open the export modal
3. Navigate through multiple pages
4. Perform searches
5. Select products across pages

**Expected Result:**
- Modal loads quickly
- Page navigation is smooth
- Search is responsive
- No performance degradation
- Memory usage remains stable

#### Test 6.2: Search Performance
**Steps:**
1. Open the export modal with 1000+ products
2. Type a common search term
3. Observe response time

**Expected Result:**
- Search completes within 1-2 seconds
- Results load without delay
- No browser lag or freezing

### 7. Edge Cases

#### Test 7.1: Single Product
**Steps:**
1. Test with a store having only 1 product
2. Open the export modal

**Expected Result:**
- Modal displays the single product
- No pagination controls visible
- Product can be selected and exported

#### Test 7.2: Empty Search Results
**Steps:**
1. Open the export modal
2. Search for a non-existent product

**Expected Result:**
- "No products found" message displays
- Pagination controls hide
- Search can be cleared to show all products

#### Test 7.3: Network Error
**Steps:**
1. Open browser dev tools
2. Throttle network to simulate slow connection
3. Navigate between pages

**Expected Result:**
- Loading spinner appears
- Eventually loads (or times out gracefully)
- Error message displays if request fails

### 8. Responsive Design

#### Test 8.1: Mobile View (< 480px)
**Steps:**
1. Open modal on mobile device or resize browser
2. Test all functionality

**Expected Result:**
- Modal is responsive
- Search bar is full width
- Per-page selector is accessible
- Pagination controls stack vertically
- All buttons are tappable

#### Test 8.2: Tablet View (481px - 782px)
**Steps:**
1. Open modal on tablet or resize browser
2. Test all functionality

**Expected Result:**
- Layout adjusts appropriately
- All controls remain accessible
- Text is readable

### 9. Security Testing

#### Test 9.1: Permission Check
**Steps:**
1. Login as a user without 'manage_woocommerce' capability
2. Attempt to access the modal

**Expected Result:**
- AJAX request returns permission denied error
- Products don't load

#### Test 9.2: Nonce Verification
**Steps:**
1. Open browser dev tools
2. Attempt AJAX request without valid nonce
3. Observe response

**Expected Result:**
- Request is rejected
- Security check failed message

### 10. Browser Compatibility

Test the feature in:
- [ ] Chrome (latest)
- [ ] Firefox (latest)
- [ ] Safari (latest)
- [ ] Edge (latest)
- [ ] Mobile Safari (iOS)
- [ ] Chrome Mobile (Android)

## Bug Reporting Template

When reporting bugs, please include:

```
**Bug Title:** [Brief description]

**Steps to Reproduce:**
1. [First step]
2. [Second step]
3. [...]

**Expected Behavior:**
[What should happen]

**Actual Behavior:**
[What actually happened]

**Environment:**
- WordPress Version: 
- WooCommerce Version: 
- OdooFlow Version: 
- Browser: 
- OS: 
- Total Products in Store: 

**Screenshots/Recordings:**
[If applicable]

**Console Errors:**
[Any JavaScript errors from browser console]

**Additional Context:**
[Any other relevant information]
```

## Success Criteria

All tests should pass with:
- ✅ No JavaScript errors in console
- ✅ No PHP errors in debug log
- ✅ Smooth user experience
- ✅ Accurate product counts
- ✅ Reliable selection persistence
- ✅ Successful exports
- ✅ Responsive design works on all devices
- ✅ Security checks function properly

## Notes for Developers

- Check browser console for errors during testing
- Monitor network tab for AJAX requests/responses
- Verify nonce is included in all requests
- Check that selected product IDs are correctly maintained
- Ensure no memory leaks during extended use
