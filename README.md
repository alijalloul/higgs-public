# Higgs Engine

Higgs is a lightweight C++ engine built using Vulkan.  
Currently, development is focused on the custom UI framework, which aims to replicate a high-performance HTML/CSS-like runtime inside a native application.  
3D/Game-related word is currently on hold.

---

![Higgs demo](assets/higgs.gif)

---

## Download

1. Open the **Releases** section  
2. Download the latest `.rar`  
3. Extract anywhere  
4. Run **higgs.exe**  
5. If Windows warns you:
   - Click **More info**
   - Click **Run anyway**

**Platform:** Windows-only for now due to GLFW dependencies and platform-specific integrations.

---

# UI Framework (Current Focus)

The majority of active development is directed at the UI framework, which acts similarly to a small HTML/CSS layout and rendering engine.

## ✔ Implemented

### **Tree-Based UI Architecture**
- DOM-like tree of nodes  
- Parent → child hierarchy  
- Cascading/inherited style properties  

### **CSS-Inspired Style System**
- Central style manager  
- ~8% of CSS properties implemented (foundational subset)  
- Partial inheritance rules  
- Pseudo-style support (hover, focus, active)
- Current style coverage includes:  
  - Basic display properties  
  - Basic positional properties (position relative, absolute. Margin, padding, etc)  
  - Basic borders
  - Overflow system
- No text/glyph rendering yet (planned)

### **Layout System (3-Pass Pipeline)**
Layout currently operates in **three passes**:

1. **Measure (Fixed)**: compute static sizes  
2. **Measure (Dynamic)**: compute flexible sizes, flexbox propagation  
3. **Position**: assign final coordinates and bounding boxes

**Flexbox**  
- Partial implementation:  
  - direction  
  - alignment  
  - wrapping  
  - flexible children sizing  
- More advanced rules planned

### **Overflow + Clipping**
- GPU stencil-test pipeline for perfect clipping  
- Correct overflow masking behavior  
- Currently supports core overflow rules

### **Scroll System (Early)**
- Wheel input handling  
- Scroll bounds and clamping  
- Vertical scroll only (`overflow-y: scroll`)  
- **No interpolation / momentum yet**  
- **No horizontal scrolling yet**  
- Integration with overflow X not started

---

# Upcoming UI Work

### **Borders**
- Per-side border widths with interpolation
- Individual colors per side  
- GPU-computating for Bezier curves

### **Scrolling**
- Horizontal scroll  
- Smooth interpolation/momentum  
- Correct propagation  
- Linked scrolling and nested scrollboxes

### **Virtualized DOM-Like Optimization**
- Render-only visible children  
- Cull large UI trees  
- Virtualized list/scroll performance

### **HTML & CSS Parsing**
- Custom tokenizer and parser  
- Map parsed structure into the engine’s UI nodes  
- CSS cascading and specificity rules (subset)

### **JSX-Like Declarative Syntax**
- Compile-time JSX-like components  
- Direct mapping to UI nodes  
- Designed to speed up UI building

### **Text Rendering**
- Glyph atlas  
- Font loading  
- Unicode shaping  
- Text layout + inline formatting  
- Text nodes and inline box model

---

# 3D Engine (Paused)

The underlying 3D renderer remains functional but is **not** the current development target.

Included:
- Vulkan rendering pipeline  
- Depth testing & MSAA  
- Directional lighting  
- Scene graph  
- Custom math library (Vec/Mat/Quat)  
- Custom OBJ + GLB loader  
- PNG/TGA/BGA image loading  
- Camera + input system  
- Resource and material managers

---

# Future Engine Work (Long-Term)

- Full PBR materials (partially implemented)  
- Shadow mapping  
- Ray-tracing experiments  
- Scene & transform editor  
- Physics system  
- Engine→"game executable" optimized build pipeline  
- UI + 3D integrated editor interface  

---

# Project Status

This project's source is **private**, experimental, and actively evolving.  
It serves primarily as an R&D platform for custom UI engines, rendering pipelines, and engine architecture exploration.