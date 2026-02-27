# Higgs Engine

Higgs is a lightweight C++ graphics, UI, and game engine built solely with Vulkan, GLFW, nlohmann/json, and the STL.  
Current development is focused on the custom UI framework, which aims to provide React-like ergonomics with native performance.

---

![Higgs demo](assets/higgs.gif)

NOTE - this video demonstrates the Grid display in depth: auto flows, fractional, fit, and defined tracks, cell-based percentage sizing, multi-grid item spanning, manual positioning, grid layout stacking (`justify-content: space-between`, `align-content: end`, `justify-items: end`, `justify-self: center`), nested grids, overflow handling, `Hello World!` text aligned middle, and Suzanne spinning.

On startup, an SDF glyph atlas texture `test.bmp` (for testing) is generated in `assets/textures/`, containing pre-rasterized SDFs for `[a-zA-Z]` and `!`. These are manually pre-queued (except for `!`) and instance-backed at runtime. The text rendering system automatically queues and flushes only what is required.

The framebuffer update propagation and callback system is not fully implemented yet. Image extents update correctly and the application should remain stable, but the UI may be incorrectly proportioned with some aspect ratio inconsistencies.

---

## Download

1. Open the Releases section  
2. Download the latest `.rar`  
3. Extract anywhere  
4. Run `higgs.exe`  
5. If Windows shows a warning:
   - Click More info  
   - Click Run anyway  

Platform: Windows only for now.

---

## UI Framework (Current Focus)

Most active development is directed at the UI framework, which behaves similarly to a small HTML/CSS layout and rendering engine.

## Implemented

### Rendering

- Vulkan renderer  
- Lightweight abstraction classes for required rendering objects: GraphicsPipeline, RenderPass, Framebuffers, DescriptorSets, BufferObjects, etc.  
- Directional lighting  
- Scene Manager  
- Multiple CPU and GPU resource managers, centralized per domain (engine, UI, game)  
- Glyphs and frames/rects are rendered separately but via a single batched instanced draw call using an instancing data structure that supports offset lookup across bindings from one or multiple SSBOs  

### Custom Work

- Custom math library including:
  - Templated linear algebra types (Vec, Mat, Quat)  
  - Ear-clipping triangulation  
  - Hole removal from simple polygons  
  - Geometric tests (point-in-shape for Bezier curves, polygons, triangles, circumcircles, relative orientation, winding order, etc)  
  - Delaunay-optimized N-point triangulation creation  
  - StarEdges creation and optimization from a random initial triangulation  
  - Bezier curve resolution (uniform and adaptive error-bounded)  
  - Bezier path ribbon generation with per-curve join logic  
  - Affine transformation helpers (translation, rotation, scaling)  
  - Floating-point comparator utilities  
- Custom file parsers for OBJ, GLB, PNG, TGA, BMP, and TTF  

### Tree-Based UI Architecture

- DOM-like node tree  
- Parent to child hierarchy  
- Cascading and inherited style properties  

### CSS-Inspired Style System

- Centralized style object manager supporting ID, Class, Tag, and Inline selectors with cascading  
- Core layout and styling implemented: display, positioning, box model (padding, margin, borders), basic text styling, overflow logic, etc
- Partial inheritance rules  
- Pseudo-style support (hover, focus, active)  

### Layout System (6-Pass Pipeline)

Originally a 3-pass system, layout pipeline was split between width and height (6 passes) since text intrinsic height depends on resolved width.

1. Intrinsic Sizing Measure: bottom-to-top computation of intrinsic sizes for nodes with undefined dimensions  
2. Resolve and Clamp Dimensions: top-to-bottom resolution and constraint application  
3. Position: top-to-bottom, final coordinate calculation  

### Displays

- Stack
   - Alternative to CSS block display. Children do not control their own positioning. Layout is parent-driven.

- Grid
   - Alignment: `justify-content`, `align-content`, `justify-items`, `align-items`,    `justify-self`, `align-self`  
   - Auto-flow and auto-density with row or column major placement, sparse or dense packing  
   - Track sizing with fixed (`px`), fractional (`fr`), and intrinsic (`fit-content`) tracks  
   - Configurable row and column gaps  
   - Multi-row and multi-column spanning with optional manual placement  
   - Explicit overlap support when positioned  

### Borders

Originally implemented through a geometry generation pipeline using multiple computational geometry algorithms. This was migrated to a shader-based approach to enable instance batching, significantly improving performance, and reduce memory usage.

### Overflow and Clipping

Originally used a stencil-buffer pipeline with cascading buffer values written onto a mask geo that then clears on the way back. This was replaced with shader-based local clipping (border to interior, not analytically perfect but visually pixel-accurate) and (not yet implemented) global clipping stage.

### Scroll System

- Wheel input handling  
- Scroll bounds and clamping  
- Vertical scrolling only (`overflow-y: scroll`)  
- No animation or momentum yet  
- No horizontal scrolling yet  

### Text Rendering and Layout

- LRU-cached glyph SDF atlas  
- Glyph rendering via sampled SDF sprites  
- TTF font loading  
- Font manager  
- Basic text layout and alignment  
- Font size, color, and family support  

---

## Upcoming UI Work

- Scrolling
   - Horizontal scrolling  
   - Smooth interpolation and momentum  

- HTML and CSS Codegen

   - Custom tokenizer and parser  
   - Mapping parsed structures into UI nodes  

- CPPX Codegen
   - Compile-time and potentially runtime JSX-like components named `cppx`  

- Reactive System
   - Signal-based reactivity model  

---

## Future Engine Work (Long-Term)

- PBR  
- Global illumination  
- Shadow mapping  
- Ray tracing  
- Scene and transform editor  
- Physics system  
- Engine to game-executable optimized build pipeline  
- Integrated UI and 3D editor interface  

---

## Project Status

This project's source is private, experimental, and actively evolving.  
It primarily serves as an R&D platform for custom UI systems, rendering pipelines, and engine architecture exploration.