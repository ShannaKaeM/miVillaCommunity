# Villa Community Site Cleanup Documentation

## Date: January 6, 2025

This document captures the functionality being removed during the site cleanup to enable future recreation.

## Dashboard Implementation

### Architecture
- **Shortcode**: `[villa_dashboard]` 
- **Pattern**: Singleton with Timber/Twig templating
- **Structure**: Tab-based navigation (Overview, Properties)
- **Access**: No authentication required - public facing

### Key Components

#### 1. Main Dashboard (`villa-dashboard.php`)
- Singleton class `VillaDashboard`
- Handles shortcode registration, assets, AJAX
- Tab navigation: Overview, Properties
- URL-based routing: `?tab=overview`, `?tab=properties`

#### 2. Controller System (`villa-dashboard-controller.php`)
- Abstract `VillaDashboardController` base class
- `VillaPropertiesController` for property management
- Common methods: rendering, AJAX, pagination

#### 3. Data Transformers (`villa-data-transformers.php`)
- `VillaPropertyTransformer`: WP posts → component data
- `VillaUserTransformer`: User objects → display data
- `VillaDashboardStatsTransformer`: Generate statistics

### Features
- Property statistics (available/occupied/maintenance)
- Community metrics (members/projects/tickets)
- Property grid/list views with filtering
- Status filtering and pagination
- AJAX component loading
- Beta/version indicators

### Dashboard Variants (Disabled)
- `villa-dashboard-minimal.php`: Simplified version
- `villa-dashboard-properties.php`: Properties-only view
- `villa-dashboard-announcements.php`: News/announcements
- `villa-dashboard-tickets.php`: Support ticket management
- `villa-frontend-dashboard.php`: Frontend implementation
- `villa-profile-dashboard.php`: User profile dashboard

## Design Book System

### Main File (`design-book.php`)
- Standalone design system documentation
- Component library showcase
- Live editing capabilities for typography
- AJAX handlers for style updates
- Integration with theme.json

### Components Documented
- Primitive books: colors, typography, spacing, layout, borders, shadows, animations
- Element books: text, buttons, badges, avatars, meta-info
- Component books: cards, stat-cards, grids, property-cards

## User/Membership System

### Membership Integration (`villa-membership-integration.php`)
- Ultimate Member plugin integration
- Custom roles: owner, bod, committee, staff, dov, partner, community_member
- Profile fields: property_address, owner_since, phone, emergency_contact
- Membership pages: login, register, members, profile
- Content restriction based on membership

### User Setup (`villa-setup-admin-owner.php`)
- Creates user_profile CPT entries
- Test property creation
- Helper function: `villa_get_user_profile($user_id)`
- Admin UI for manual setup

### Role Management (`villa-fix-user-roles.php`)
- Maps villa roles to WordPress roles
- Fixes users without proper roles
- Admin tool for role management

## Navigation & Templates

### Navigation Setup (`villa-setup-navigation.php`)
- Creates "Main Navigation" menu
- Default items: Home, Properties, Test
- Dashboard link for logged-in users
- Auto-creates missing pages

### Template Fixes (`villa-fix-templates.php`)
- Forces template recognition
- Enables component test template
- Refreshes template cache

## Custom Post Types

All CPTs are being KEPT:
- `property`: Property listings
- `business`: Business directory
- `villa_group`: Groups/Committees
- `user_profile`: Member profiles
- `villa_projects`: Projects system
- `article`: Articles/News

## Files Removed

### MU-Plugins (26 files)
```
Dashboard:
- villa-dashboard.php
- villa-dashboard-controller.php
- villa-create-dashboard-page.php
- villa-dashboard-additional.php.disabled
- villa-dashboard-announcements.php.disabled
- villa-dashboard-minimal.php.disabled
- villa-dashboard-properties.php.disabled
- villa-dashboard-tickets.php.disabled
- villa-frontend-dashboard.php.disabled
- villa-profile-dashboard.php.disabled
- zz-villa-dashboard-refactored.php.disabled
- 99-villa-dashboard-test.php.disabled

Design System:
- design-book.php

Core Functions:
- villa-data-transformers.php
- villa-membership-integration.php
- villa-setup-admin-owner.php
- villa-setup-navigation.php
- villa-fix-user-roles.php
- villa-fix-templates.php
- flush-rewrites.php
- 00-villa-autoloader.php

Utilities:
- villa-cleanup-and-restructure.php
- villa-sample-users.php
- 00-debug-test.php
```

### Theme Files
```
Dashboard Templates:
- templates/design-book/dashboard.twig
- templates/design-book/typography.twig
- templates/dashboard/home.twig
- templates/dashboard/overview.twig
- templates/dashboard/properties-grid.twig

Dashboard Assets:
- assets/css/villa-dashboard.css
- assets/js/villa-dashboard.js
- assets/css/design-book.css
- assets/js/design-book.js

PHP Files:
- inc/design-book-router.php
- page-design-system.php
```

## Files Kept

### MU-Plugins (7 files)
```
CPT Registration:
- villa-cpt-registration.php
- villa-groups-cpt.php
- villa-projects-cpt.php
- villa-projects-fields.php

CMB2 Setup:
- villa-community-core.php
- cmb2-setup.php
- cmb2-property-fields.php
```

### Theme Components
All Twig component books preserved:
- Primitive books (7 files)
- Element books (5 files)
- Component books (4 files)
- Base templates (3 files)

Helper functions preserved in:
- inc/template-functions.php
- Component-related functions in functions.php

## Key Patterns for Recreation

1. **Component Architecture**: Atomic design with Twig templates
2. **Data Flow**: WordPress → Transformer → Twig Context → Component
3. **AJAX Pattern**: Nonce security, JSON responses, component rendering
4. **Tab Navigation**: URL parameters, state management
5. **Permissions**: Role-based access using custom villa roles
6. **Styling**: theme.json integration, CSS custom properties

## Database Considerations

Custom tables/options that may need cleanup:
- Dashboard page (if created)
- Navigation menu items
- User meta for villa roles
- CMB2 field data (preserved with CPTs)