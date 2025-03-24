
![[Pasted image 20250323131640.png]]

### **Cluster 1: Activated T Cell / NK-like T**

- **Top Markers:** IL_2, CD154, CD16, CD127, pPLCg
- **Analysis:**
    - IL_2 and CD154 indicate T cell activation.
    - CD16 suggests NK or NK-like T cells.
    - CD127 is found on T cells.
    - pPLCg points to cell activation.
- **Likely Cell Type:** Mixed population of activated T cells and NK-like T cells.
- **Recommendations:** Add CD56 to distinguish NK cells, and CD69 for activation confirmation.

### **Cluster 2: CD8+ T Cell (Effector Memory)**

- **Top Markers:** CD8, CD3, IFN_g, CD127, TNFa
- **Analysis:**
    - CD8 and CD3 confirm CD8+ T cell identity.
    - IFN_g and TNFa denote effector memory T cells.
    - CD127 is present on memory T cells.
- **Likely Cell Type:** CD8+ effector memory T cells.
- **Recommendations:** The current signature is accurate.

### **Cluster 3: B Cell (Mature/Memory B)**

- **Top Markers:** Ig_LC_kappa, CD45, LD, CD20, CD19
- **Analysis:**
    - CD19 and CD20 are B cell markers.
    - Ig_LC_kappa confirms B cell identity.
    - LD indicates metabolic activity.
- **Likely Cell Type:** Mature or memory B cells.
- **Recommendations:** Add CD27 to refine memory B cell identification.

### **Cluster 4: B Cell / Proliferating Immune Cells**

- **Top Markers:** p53, Bcl2, pS6, HLA_DR, BAFFR
- **Analysis:**
    - p53 and Bcl2 relate to cell survival.
    - pS6 indicates proliferation.
    - HLA_DR suggests antigen presentation.
    - BAFFR relates to B cell activation/survival.
- **Likely Cell Type:** Potential plasma B cells or regulatory B cells.
- **Recommendations:** Further characterization with plasma cell markers is needed.

### **Cluster 5: Regulatory T Cell (Treg) / B Cell Activation**

- **Top Markers:** CCR7, CD25, Ig_LC_kappa, CD70, BAFFR
- **Analysis:**
    - CCR7 and CD25 suggest Tregs.
    - Ig_LC_kappa, CD70 and BAFFR suggests B cell activation.
- **Likely Cell Type:** Likely needs a Treg rule, or a mix of Tregs and activated B cells.
- **Recommendations:** add CD4 and CD3 to confirm Treg identity, and IL-10 if available to confirm regulatory B cells.

### **Cluster 6: Regulatory T Cell / Activated Cell State**

- **Top Markers:** p38_MAPK, pS6, CCR7, p53, CD25
- **Analysis:**
    - p38_MAPK and pS6 indicate activation.
    - CCR7 and CD25 suggest Tregs.
    - p53 relates to cell cycle.
- **Likely Cell Type:** Tregs or proliferating T cells.
- **Recommendations:** A new Treg or proliferating T cell rule is needed.

### **Cluster 7: B Cell / Proliferating Cells**

- **Top Markers:** p21, Bcl2, CD19, NFAT1, Cyclin_B1
- **Analysis:**
    - CD19 is a B cell marker.
    - p21, Bcl2, NFAT1, and Cyclin_B1 indicate proliferation.
- **Likely Cell Type:** Proliferating B cells, possibly plasma B cells.
- **Recommendations:** A plasma B cell rule is needed.

**Cluster 8: Cytotoxic T Cell / Activated B Cell?**

- **Top Markers:** CD107a, NFAT1, pS6, Cyclin_D1, BAFFR
- **Analysis:**
    - CD107a indicates cytotoxic activity.
    - NFAT1, pS6, and Cyclin_D1 suggest activation.
    - BAFFR relates to B cell activation.
- **Likely Cell Type:** Possibly CD8 T cells or a cytotoxic B cell subset.
- **Recommendations:** Further CD8 T cell or cytotoxic subset characterization is required.

**Cluster 9: Memory B Cell?**

- **Top Markers:** p38_MAPK, Ig_LC_kappa, NFAT1, CD20, CCR7
- **Analysis:**
    - CD20 and Ig_LC_kappa are B cell markers.
    - CCR7 suggests memory cells.
    - p38_MAPK and NFAT1 indicate activation.
- **Likely Cell Type:** A unique memory B cell subset.
- **Recommendations:** Further subset characterization is needed.

**Cluster 10: B1 B Cell / Proliferating B?**

- **Top Markers:** CD5, Ig_LC_kappa, LD, CD70, CD25
- **Analysis:**
    - CD5 suggests a B1 B cell subset.
    - Ig_LC_kappa confirms B cell identity.
    - LD indicates metabolic activity.
    - CD70 and CD25 relate to activation.
- **Likely Cell Type:** B1 B cell or proliferating B cells.
- **Recommendations:** Further characterization is needed.

**Cluster 11: Activated B Cell / Monocyte-like B?**

- **Top Markers:** CD107a, p21, NFAT1, HLA_DR, CD19
- **Analysis:**
    - CD19 is a B cell marker.
    - CD107a, NFAT1, and HLA_DR suggest activation.
    - p21 relates to cell cycle.
- **Likely Cell Type:** Activated antigen-presenting B cells or monocyte-like B cells.
- **Recommendations:** Further characterization is needed.

**Cluster 12: Proliferating B Cell (Plasma Precursor?)**

- **Top Markers:** Bcl2, CD70, CCR7, Ki67, Ig_LC_lambda
- **Analysis:**
    - Ig_LC_lambda confirms B cell identity.
    - Ki67 indicates proliferation.
    - CD70 and CCR7 relate to activation.
    - Bcl2 relates to cell survival.
- **Likely Cell Type:** Proliferating B cells, possibly plasma precursors.
- **Recommendations:** A plasma B cell rule is needed.

**Cluster 13: Memory B Cell (BAFFR-Dependent?)**

- **Top Markers:** CD70, Ig_LC_lambda, CD27, BAFFR, CD19
- **Analysis:**
    - CD19 and Ig_LC_lambda confirm B cell identity.
    - CD27 and BAFFR suggest memory B cells.
- **Likely Cell Type:** B memory cells, possibly BAFFR-dependent.
- **Recommendations:** A new BAFFR+ rule may be needed.

**Cluster 14: Regulatory T or B1 B Cell?**

- **Top Markers:** CCR7, CD5, CD25, BAFFR, CD70
- **Analysis:**
    - CCR7 and CD25 suggest Tregs.
    - CD5 suggests B1 B cells.
    - BAFFR and CD70 relate to B cell activation.
- **Likely Cell Type:** A unique Treg or B1 B cell subset.
- **Recommendations:** Further characterization is needed.

**Cluster 15: Proliferating or Apoptotic B Cells**

- **Top Markers:** CD45, pH2AX, CD5, Bcl2, Ig_LC_kappa
- **Analysis:**
    - Ig_LC_kappa confirms B cell identity.
    - pH2AX indicates DNA damage.
    - Bcl2 relates to cell survival.
    - CD5 can be on B1 B cells.
- **Likely Cell Type:** Proliferating or apoptotic B cells.
- **Recommendations:** A proliferation/apoptosis rule is needed.

**Cluster 17: B Cell (IL-4 Induced?)**

- **Top Markers:** Ig_LC_lambda, IL_4, CCR7, CD20, NFAT1
- **Analysis:** Ig_LC_lambda and CD20 are B cell markers. IL_4 and NFAT1 indicate activation. CCR7 suggests memory.
- **Likely Cell Type:** IL-4 induced activated or memory B cells.
- **Recommendations:** Further characterization of activation state needed.

**Cluster 18: NK Cell (Cytotoxic)**

- **Top Markers:** Perforin, CD56, GRZB, CD38, GM_CSF
- **Analysis:** Perforin and GRZB indicate cytotoxicity. CD56 confirms NK cell identity. CD38 and GM_CSF relate to activation.
- **Likely Cell Type:** Cytotoxic NK cells.
- **Recommendations:** Accurate identification.

**Cluster 19: CD4+ T Cell (Inflammatory/Activated)**

- **Top Markers:** CD4, NFkB_p65, pH2AX, IL_6, pBTK_ITK
- **Analysis:** CD4 confirms CD4+ T cell identity. NFkB_p65, IL_6, and pBTK_ITK indicate inflammation and activation. pH2AX implies DNA damage.
- **Likely Cell Type:** Inflammatory/activated CD4+ T cells.
- **Recommendations:** Accurate identification.

**Cluster 20: Activated B Cell / Regulatory B?**

- **Top Markers:** NFkB_p65, CD27, Ig_LC_lambda, CD45RA, CD25
- **Analysis:** Ig_LC_lambda confirms B cell identity. CD27 and CD45RA relate to memory. CD25 and NFkB_p65 suggest activation.
- **Likely Cell Type:** Activated or regulatory B cells (Bregs).
- **Recommendations:** Add IL-10 to confirm Breg identity.

**Cluster 21: Memory B / Plasma Precursor?**

- **Top Markers:** Ig_LC_lambda, CD38, CD70, CD20, CCR7
- **Analysis:** Ig_LC_lambda and CD20 confirm B cell identity. CD38 suggests plasma cells. CD70 and CCR7 relate to activation and memory.
- **Likely Cell Type:** Memory B cells or plasma cell precursors.
- **Recommendations:** Further characterization needed.

**Cluster 22: Activated B Cell?**

- **Top Markers:** CD19, CD25, CD45RA, CD107a, pPLCg
- **Analysis:** CD19 confirms B cell identity. CD25, CD45RA and pPLCg indicate activation. CD107a implies activation.
- **Likely Cell Type:** Activated B cells.
- **Recommendations:** Accurate identification.

**Cluster 23: Gamma Delta (γδ) T Cell**

- **Top Markers:** TCRgd, KLRG1, IFN_g, TNFa, CD3
- **Analysis:** TCRgd and CD3 confirm γδ T cell identity. KLRG1, IFN_g and TNFa indicate activation.
- **Likely Cell Type:** Gamma Delta (γδ) T cells.
- **Recommendations:** Accurate identification.

**Cluster 24: NK-like T Cell / Adaptive NK?**

- **Top Markers:** KLRG1, GRZB, TNFa, IFN_g, CD56
- **Analysis:** KLRG1, GRZB, TNFa, IFN_g, and CD56 indicate NK or NK-like T cell identity.
- **Likely Cell Type:** NK-like T cells or adaptive NK cells.
- **Recommendations:** further differentiation needed.