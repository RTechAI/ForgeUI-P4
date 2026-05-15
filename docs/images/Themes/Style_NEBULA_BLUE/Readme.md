// ============================================================
// ForgeUI Visual Styles.
// ============================================================
//
// File:
// 00_ForgeUI_Config.h
//
// Edit this config section to change
// ForgeUI themes and optional UI modules.
//
// Theme Selection:
//
// remove // to ENABLE a theme
// place // in front of themes you want DISABLED
//
// ONLY enable ONE theme at a time.
//
// CURRENT THEME:
// NEBULA_BLUE
//
// Optional UI modules:
//
// FORGEUI_ENABLE_HEADER
// 1 = header ON
// 0 = header OFF
//
// FORGEUI_ENABLE_DASHBOARD_TILES
// 1 = tiles ON
// 0 = tiles OFF
//
// Then clean build + flash.
//
// ============================================================

//#define FORGEUI_STYLE_ACTIVE             FORGEUI_STYLE_ATLAS_LIGHT
#define FORGEUI_STYLE_ACTIVE               FORGEUI_STYLE_NEBULA_BLUE
//#define FORGEUI_STYLE_ACTIVE             FORGEUI_STYLE_REACTOR

#define FORGEUI_ENABLE_HEADER              0
#define FORGEUI_ENABLE_DASHBOARD_TILES     1


// ============================================================
// Theme IDs - LEAVE THESE ALONE
// ============================================================

#define FORGEUI_STYLE_ATLAS_LIGHT          0
#define FORGEUI_STYLE_NEBULA_BLUE          1
#define FORGEUI_STYLE_REACTOR              2