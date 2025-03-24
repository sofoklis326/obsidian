cytoVI data mock dataset

![[Drawing 2025-03-06 11.31.23.excalidraw]]
heatmap imputed layer
200 markers 5 panels
T-NK panel, surface panel, cytokine panel, emv panel for bcells, sic panel for downstream of b cell receptor signaling

if we integrate all the panels, what results do we get.

single cell experiment values, not fcs.
4 experiments to be transformed to annData to work with cytoVI
exprs transfm are the data
look at gdrive file
there is a signaling panel



# 11/03/2025

  
Get familiar with the high dimensional cytometry data type and workflow 
Get familiar with CytoVI workflow 
Get familiar with the MCL cohort 
Convert sce to Anndata 
Integrate SUR, CYT, IMV, TNK panels - all cell types included 
Cluster and annotate the major cell types
B cells: CD19+, CD3-
CD4 T cells: CD19-, CD3+, CD4+, CD8-
CD8 T cells: CD19-, CD3+, CD4-, CD8+
NK cells: CD3-, CD56+
Myeloid cells: CD33+
Calculate proportion of T cells, NK cells and myeloid cells of total healthy immune cells (everything minus B cells) per patient and per sample
Test the proportion between healthy, MCL and other B-NHL 
Compare with what we got based on one panel (SUR)  
Send Sofoklis: 
- 4 panels 
- CSV file of proportions from one panel
# Next meeting
 
Either T cells only or CITE-seq data

### 2. Cross-Dataset Validation and Integration
Your approach is valid and here's a recommended workflow:

#### A. Initial Validation
```markdown
1. Train on Dataset A → Test on Dataset B
2. Train on Dataset B → Test on Dataset A
3. Evaluate imputation quality using shared markers
```

Here's example code:
````python
# Train on dataset A
cytovi.pp.arcsinh(adata_A, global_scaling_factor=2000)
cytovi.pp.scale(adata_A)
cytovi.CytoVI.setup_anndata(adata_A, layer='scaled', batch_key='batch')
model_A = cytovi.CytoVI(adata_A)
model_A.train()

# Test on dataset B
pred_B = model_A.get_normalized_expression(adata_B)

# Calculate metrics for shared markers
shared_markers = list(set(adata_A.var_names) & set(adata_B.var_names))
correlation_scores = compute_marker_correlations(adata_B, pred_B, markers=shared_markers)
````

#### B. Integration Strategies
If performance is satisfactory, you have several options:

1. **Concatenate and Retrain**:
````python
# Combine datasets with proper batch annotation
combined = ad.concat([adata_A, adata_B], join='outer')
cytovi.CytoVI.setup_anndata(combined, 
                           layer='scaled',
                           batch_key='batch',
                           nan_layer='missing_markers')
model_combined = cytovi.CytoVI(combined)
model_combined.train(use_adversarial_classifier=True)
````

2. **Transfer Learning Approach**:
````python
# Train reference model
ref_model = cytovi.CytoVI(adata_A)
ref_model.train()

# Update with new data using reference
updated_model = cytovi.CytoVI.load_query_data(
    adata_B,
    ref_model,
    use_adversarial_classifier=True
)
updated_model.train()
````

#### Best Practices
```markdown
1. Quality Control:
   - Check marker distributions before integration
   - Validate shared marker correlations
   - Use technical replicates if available

2. Batch Effect Mitigation:
   - Use adversarial training
   - Include proper controls
   - Monitor batch mixing metrics

3. Validation:
   - Use known population frequencies
   - Check biological markers
   - Validate with orthogonal methods
```

The key is to ensure that the datasets are compatible enough before integration, which your cross-validation approach helps determine. The adversarial training in CytoVI will help mitigate batch effects during integration.