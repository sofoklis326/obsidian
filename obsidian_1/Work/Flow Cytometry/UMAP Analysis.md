
### **🗺️ 1. What Does Each Point Represent?**

- Each **dot** = a **single cell** from your bone marrow sample.
- Dots are positioned based on **similarity** (cells with similar marker expression are closer).
- **Clusters = biologically distinct populations** (e.g., CD8+ T cells vs. NK cells).

### **📏 2. Axes in UMAP: What Do They Mean?**

Unlike PCA (which uses variance), **UMAP axes (UMAP-1, UMAP-2) do not correspond to specific markers.**

- **UMAP does not have a direct biological interpretation.**
- **Distance matters:** Closer clusters mean **similar phenotypes**, and further apart means **different populations**.
- **Local vs. Global Structure:**
    - Local distances reflect **cell similarity**.
    - Large-scale distances may be **less interpretable** (UMAP optimizes local relationships more than global ones).
### **🔍 3. How to Read UMAP Clusters?**

Clusters in a UMAP plot often **correspond to major cell populations**:

- **T Cells (CD3+ clusters)**
- **CD8+ Cytotoxic T Cells (CD8+, GZMB+)**
- **Exhausted T Cells (PD1+, TIM3+, TIGIT+)**
- **Memory T Cells (CD127+, CD27+)**
- **NK Cells (CD16+, GZMB+)**
- **Monocytes/Dendritic Cells (CD1c+, HLA-DR+)**

To confirm these identities, you overlay **marker expression** (coloring cells by intensity).

### **🎨 4. Using Marker Overlays to Define Populations**

💡 **Strategy: Overlay key markers to "paint" clusters with biological meaning.**

- **CD3 expression overlay** → Identifies T cells.
- **CD8 overlay** → Separates CD8+ from other T cells.
- **PD1, TIM3, TIGIT overlay** → Identifies exhausted T cells.
- **CD103, CD69 overlay** → Tissue-resident memory T cells (TRM).
- **GZMB overlay** → Cytotoxic potential (CD8+ T cells, NK cells).
- **CD16 overlay** → Helps separate NK cells and monocytes.

📌 **Approach:**

1. **Single marker overlay** (e.g., CD8 expression across all cells).
2. **Pairwise marker comparison** (e.g., CD8 vs. PD1).
3. **Multi-marker heatmaps** (e.g., CD3+ CD8+ GZMB+ → Cytotoxic T cells).

### **🛠 5. Identifying New or Unexpected Populations**

Once major populations are identified, check for:  
✅ **Intermediate populations** (e.g., partially exhausted T cells with PD1+ but low TIM3).  
✅ **Heterogeneity within known subsets** (e.g., multiple memory T cell states).  
✅ **Rare or unexpected populations** (e.g., regulatory T cells, myeloid-derived suppressor cells).

### **📊 6. Density-Based Clustering for More Insights**

To quantify clusters:

- **HDBSCAN** (Hierarchical Density-Based Clustering) → Identifies discrete populations.
- **FlowSOM** → Uses self-organizing maps for clustering FCS data.
- **K-means/GMM** → Works but less effective for nonlinear relationships.