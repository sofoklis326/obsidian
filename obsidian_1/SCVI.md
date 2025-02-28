Generative model of scRNA-seq count data
The advantages of scVI are:
- Comprehensive in capabilities.
- Scalable to very large datasets (>1 million cells).
The limitations of scVI include:
- Effectively requires a GPU for fast inference.
- Latent space is not interpretable, unlike that of a linear method.

  
scVI takes as input a scRNA-seq gene expression matrix X with N cells and G genes. Additionally, a design matrix S containing p observed covariates, such as day, donor, etc, is an optional input. While S can include both categorical covariates and continuous covariates, in the following, we assume it contains only one categorical covariate with K categories, which represents the common case of having multiple batches of data.

### **1. scRNA-seq Gene Expression Matrix (Counts Table)**

Each row represents a **cell**, and each column represents a **gene**. The values indicate the expression levels (counts) for each gene in each cell.

| Cell ID | Gene A | Gene B | Gene C | Gene D | ... |
| ------- | ------ | ------ | ------ | ------ | --- |
| Cell_1  | 100    | 0      | 50     | 20     | ... |
| Cell_2  | 200    | 10     | 0      | 5      | ... |
| Cell_3  | 0      | 30     | 10     | 15     | ... |
| ...     | ...    | ...    | ...    | ...    | ... |
| Cell_N  | 5      | 100    | 20     | 0      | ... |
### **2. Design Matrix (Covariates Table)**

This table contains additional observed covariates like batch, donor, or experimental conditions.

| Cell ID | Batch | Donor | Timepoint |
| ------- | ----- | ----- | --------- |
| Cell_1  | A     | D1    | 0h        |
| Cell_2  | A     | D1    | 0h        |
| Cell_3  | B     | D2    | 24h       |
| ...     | ...   | ...   | ...       |
| Cell_N  | C     | D3    | 48h       |
- **Batch**: Categorical variable representing different experimental runs.
- **Donor**: Categorical variable indicating the individual from whom the sample was collected.
- **Timepoint**: Could be categorical or continuous, representing different collection times.

$$
 \begin{align}
 z_n &\sim {\mathrm{Normal}}\left( {0,I} \right) \\
 \ell_n &\sim \mathrm{LogNormal}\left( \ell_\mu^\top s_n ,\ell_{\sigma^2}^\top s_n \right) \\
 \rho n &= f_w\left( z_n, s_n \right) \\
 \pi{ng} &= f_h^g(z_n, s_n) \\
 x_{ng} &\sim \mathrm{ObservationModel}(\ell_n \rho_n, \theta_g, \pi_{ng})
 \end{align}
$$

### **1. Latent Variable for Cell Representation**

$$
z_n∼Normal(0,I)
$$

is a latent variable representing the underlying biological state of cell n.

- It is drawn from a standard **multivariate normal distribution** with mean **0** and identity covariance matrix **I**.
- Does that mean that all features of each cell are independent of the others ?
- This helps to learn a lower-dimensional representation of cells.