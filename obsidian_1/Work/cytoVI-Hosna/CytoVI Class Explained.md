
### CytoVI Class

This is a deep learning model adapted from scVI (single-cell Variational Inference) for analyzing flow/mass cytometry data. It inherits from multiple base classes to implement a variational autoencoder (VAE) architecture.

### Key Methods in CytoVI

#### 1. [setup_anndata](vscode-file://vscode-app/usr/share/code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)

**Purpose**: 
- Prepares the AnnData object for model training by registering data fields and validating inputs.
**Key Parameters**:
- `adata`: AnnData object containing cytometry data
- `layer`: Specific data layer to use
- `batch_key`: Column in adata.obs for batch information
- `labels_key`: Column for cell type/condition labels
- `sample_key`: Column identifying biological samples
- `nan_layer`: Layer containing missing value masks
**What it does**:
1. Registers field types (Layer, Categorical, Numerical)
2. Validates input data structure
3. Sets up batch correction capabilities
4. Handles missing marker information

![[Drawing 2025-03-11 18.57.18.excalidraw]]

#### 2. [train](vscode-file://vscode-app/usr/share/code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)

**Purpose**: 
- Trains the variational autoencoder model using amortized inference.
**Key Parameters**:
- `max_epochs`: Maximum training iterations
- `lr`: Learning rate
- `batch_size`: Mini-batch size
- `train_size`: Fraction of data for training
- `early_stopping`: Whether to use early stopping
- `adversarial_classifier`: Whether to use adversarial training for batch correction
**What it does**:
1. Sets up data splitting for training/validation
2. Initializes training plan with KL divergence warmup
3. Handles batch effect correction through adversarial training
4. Monitors convergence and early stopping
5. Returns trained model
#### 3. [get_normalized_expression](vscode-file://vscode-app/usr/share/code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)

**Purpose**: 
- Retrieves decoded protein expression values from the model.
**Key Parameters**:
- `transform_batch`: Which batch to condition on
- `n_samples`: Number of posterior samples
- `protein_list`: Specific proteins to return
- `return_mean`: Whether to average samples
- `weights`: How to weight samples ("uniform" or "importance")
**What it does**:
1. Processes data through encoder and decoder
2. Handles batch effect correction
3. Can impute missing proteins
4. Returns normalized expression values
5. Supports importance sampling
#### 4. [differential_expression](vscode-file://vscode-app/usr/share/code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)

**Purpose**: 
- Performs differential expression analysis between groups.
**Key Parameters**:
- `groupby`: Column for grouping cells
- `group1/group2`: Groups to compare
- `mode`: Analysis mode ("vanilla" or "change")
- `batch_correction`: Whether to correct for batch effects
- `fdr_target`: False discovery rate target
**What it does**:
1. Computes Bayes factors for differential expression
2. Handles batch correction in comparisons
3. Implements multiple testing correction
4. Returns detailed statistics
5. Supports different comparison modes
#### 5. [differential_abundance](vscode-file://vscode-app/usr/share/code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)

**Purpose**: 
- Analyzes differences in cell population frequencies.
**Key Parameters**:
- `locs/scales`: Latent space parameters
- `sample_id`: Sample identifiers
- `batch_size`: Processing batch size
- `compute_log_enrichment`: Whether to compute enrichment scores
**What it does**:
1. Computes aggregated posterior distributions
2. Calculates log probabilities for populations
3. Handles batch processing for large datasets
4. Returns population frequency differences
#### 6. [impute_categories_from_reference](vscode-file://vscode-app/usr/share/code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)

**Purpose**: 
- Imputes missing categorical labels using a reference dataset.
**Key Parameters**:
- `adata_reference`: Reference dataset
- `cat_key`: Category to impute
- `n_neighbors`: Number of neighbors for imputation
- `return_uncertainty`: Whether to return uncertainty estimates
**What it does**:
1. Uses shared latent space representation
2. Performs k-nearest neighbor imputation
3. Handles category encoding/decoding
4. Can estimate imputation uncertainty
#### 7. [impute_rna_from_reference](vscode-file://vscode-app/usr/share/code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)

**Purpose**: 
- Imputes RNA expression data from a reference dataset.
**Key Parameters**:
- `reference_batch`: Reference batch identifier
- `adata_rna`: RNA expression data
- `layer_key`: Layer containing expression data
- `n_neighbors`: Number of neighbors for imputation
**What it does**:
1. Uses shared latent representation
2. Performs k-NN based expression imputation
3. Handles data integration
4. Returns imputed expression matrix

Each method includes extensive error checking and validation to ensure proper usage and data compatibility.

### Questions

Let me reorganize and answer your questions systematically:

#### 1. Batch Information and Data Preprocessing
##### Q: What is batch information and why use scaled layer?
**Batch effects** are technical variations between samples due to:
  - Different experimental runs
  - Different days of collection
  - Different machines/operators
  - Different reagent lots

##### A: Layer Selection
- The `scaled` layer is used after `arcsinh` because:
  - Scaling normalizes the range of markers across batches
  - Makes training more stable
  - Both transformations are typically needed:
    1. `arcsinh`: Handles initial data distribution
    2. `scaling`: Normalizes ranges across markers

#### 2. Batch Effect Correction
##### Q: How does the adversarial classifier work?
##### A: The adversarial training works by:
```markdown
1. Main VAE tries to encode data into batch-invariant representations
2. Adversarial classifier tries to predict batch from latent space
3. VAE is trained to "fool" the classifier
4. This creates batch-invariant representations
```

#### 3. Normalized Expression Method
##### Q: What can get_normalized_expression do?

##### A: Can do both:
  1. Generate new AnnData object with corrected expressions
  2. Impute missing values in existing data
  3. Transform data to reference batch conditions

Example:
````python
# Get normalized expression
norm_exp = model.get_normalized_expression()

# Create new AnnData
new_adata = anndata.AnnData(norm_exp)

# Or impute specific values
imputed_values = model.get_normalized_expression(transform_batch='batch1')
````

#### 4. Differential Expression Analysis
##### Q: How does differential_expression work?

##### A: Works within single AnnData object
- Groups are defined by column in `adata.obs`
- Common grouping examples:
  - Cell types
  - Treatment conditions
  - Time points

Example:
````python
# Compare groups within same AnnData
de_results = model.differential_expression(
    groupby='cell_type',
    group1='T cells',
    group2='B cells'
)
````

#### 5. Differential Abundance
##### Q: Is this separate from VAE?

##### A: Actually uses the VAE's latent space
- Analyzes cell population frequencies
- Leverages learned representations
- Different from traditional density-based approaches
#### 6. Category Imputation
##### Q: How does reference-based imputation work?
```markdown
1. Train model on reference dataset with known labels
2. Apply to query dataset
3. Can either:
   - Add new columns to query dataset
   - Generate predictions for new data
```

#### 7. RNA Imputation
##### Q: Requirements for RNA imputation?
##### A: Yes, requires trained model
- Process:
  1. Train CytoVI on protein data
  2. Use reference RNA dataset
  3. Map protein patterns to RNA expression
  4. Impute RNA values for new samples

Example workflow:
````python
# Train model first
model.train()

# Then impute RNA
rna_imputed = model.impute_rna_from_reference(
    adata_rna=reference_rna,
    reference_batch='batch1'
)
````

This is an integrated workflow where each method builds on the learned latent space representations from the VAE training. The batch correction and imputation capabilities are core features that leverage this learned representation.

Let me address your questions with proper formatting:

#### 8. Understanding Loss Values
##### Q: Why are loss values negative?
##### A: The negative values come from the Evidence Lower BOund (ELBO) loss function used in VAEs:
- ELBO = Reconstruction Loss + KL Divergence
- In CytoVI, the reconstruction term uses log-likelihood
- Log-likelihoods are often negative
- The more negative, the worse the fit
- As training progresses, values should increase (become less negative)