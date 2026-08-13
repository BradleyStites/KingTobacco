Project Specification: King Tobacco Dynamic Menu System
1. System Architecture Overview
The Workflow: The system uses a localized two-file static model. The client manages data locally via a secure admin panel (admin.html), which saves state locally and compiles/exports a fresh, standalone public display file (client.html) ready for static deployment (Netlify/GitHub Pages).

The NFC / QR Target: The physical NFC chip and printed QR code point strictly to client.html.

2. admin.html (The Control Panel)
Features & UI Requirements
Persistent Local Storage: Retains all brands, custom accent colors, logo asset paths, and flavor lists across browser sessions.

Brand Customization:

Ability to input or select a brand.

A brand-specific color picker to assign a unique border/accent color for each brand section (matching the dark theme aesthetic).

A logo management field to link or upload a custom logo graphic per brand.

Export Engine: A prominent "Export Client Menu" button that dynamically bundles the current JSON dataset, color styles, and templates into a clean, standalone client.html file download.

Core Admin Script Structure (Conceptual Markdown Template)
HTML
<!-- Admin Panel Structure Concept -->
<div class="admin-container">
    <h2>👑 King Tobacco - Admin Control Panel</h2>
    
    <!-- 1. Add / Configure Brand -->
    <div class="panel-section">
        <h3>Manage Brands & Custom Theming</h3>
        <input type="text" id="brandNameInput" placeholder="Brand Name (e.g., Fogger)">
        <label>Brand Accent Color:</label>
        <input type="color" id="brandColorInput" value="#d4af37">
        <input type="text" id="brandLogoInput" placeholder="Logo Image URL or Path">
        <button onclick="addNewBrand()">Save Brand Configuration</button>
    </div>

    <!-- 2. Add Flavor -->
    <div class="panel-section">
        <h3>Add Flavor</h3>
        <select id="targetBrandSelect"></select>
        <input type="text" id="newFlavor" placeholder="Flavor Name">
        <button onclick="addFlavor()">Add Flavor to Brand</button>
    </div>

    <!-- 3. Export Action -->
    <div class="panel-section">
        <h3>Publish Changes</h3>
        <button onclick="exportClientPage()" class="export-btn">Generate & Download client.html</button>
    </div>
</div>
3. client.html (The Public Display)
Features & UI Requirements
Strictly Read-Only: Zero administrative buttons, input forms, or modification capabilities. Completely clean interface optimized for customer mobile screens.

Visual Theme Alignment: Dark background mode (#121212) consistent with the branding, utilizing custom left-border accent coloring mapped dynamically per brand.

Header Logo Section: Displays the primary brand/shop logo at the top center of the mobile view.

Interactive Filtering: Includes a live search bar and a brand filter dropdown to instantly sort or locate products.

Auto-Alphabetized Display: Automatically sorts brand headers and individual flavor tags alphabetically.

Core Client Script Structure (Conceptual Markdown Template)
HTML
<!-- Client Display Structure Concept -->
<div class="client-container">
    <div class="logo-header">
        <img src="shop-logo.png" alt="King Tobacco Logo" id="mainShopLogo">
        <h1>King Tobacco Menu</h1>
    </div>

    <!-- Search & Filter Bar -->
    <div class="controls">
        <input type="text" id="searchInput" placeholder="Search flavors..." onkeyup="filterFlavors()">
        <select id="brandFilter" onchange="filterFlavors()">
            <option value="all">All Brands</option>
        </select>
    </div>

    <!-- Dynamic Menu Output Container -->
    <div id="menuContainer"></div>
</div>
4. Data Object Schema
To support custom brand colors and logos alongside the flavor arrays, the underlying data structure in localStorage scales to a nested object format:

JavaScript
let inventory = {
    "Fogger": {
        color: "#d4af37", // Custom brand accent color
        logo: "fogger-logo.png", // Brand-specific logo asset
        flavors: [
            "Blue Razz Ice", 
            "Strawberry Ice", 
            "Watermelon Ice"
            // ... sorted flavor list
        ]
    },
    "Geek Bar": {
        color: "#00ffcc",
        logo: "geekbar-logo.png",
        flavors: [
            "Miami Mint",
            "Watermelon Ice"
        ]
    }
};
