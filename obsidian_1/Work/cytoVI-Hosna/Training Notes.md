## Impossible to convert directly to AnnData format
	- Make it sparse matrix
	- Disregard metadata (delete)
	- split in chunks (worked with 25 chunks)
	- save in hd5a format
	- put them together using python
## Training model with whole dataset takes too long
	- increase batch size (set to 512)
	- set epochs to 100
	- increase workers in case of newer computer


# CytoVI Training and Transfer Learning Analysis

Looking at the CytoVI implementation, I can see that it supports **both full retraining** and **transfer learning** capabilities:

## Training Nature

The code shows that **CytoVI** is primarily set up for complete training on your dataset, not automatic fine-tuning. When you call:

```python
model = cytovi.CytoVI(adata)
model.train(max_epochs=100)
```

The model trains from scratch (random initialization) on your data.

## Transfer Learning Support

However, CytoVI *does* support transfer learning through multiple mechanisms:

1. **ArchesMixin Inheritance**: CytoVI inherits from `ArchesMixin`, which enables reference mapping capabilities from the scvi-tools ecosystem. This means it supports the [scArches](https://www.nature.com/articles/s41587-021-00867-x) paradigm.

2. **impute_categories_from_reference Method**: This function (lines 748-824) explicitly implements transfer learning for category annotation, allowing you to:
   ```python
   # Train on reference data
   model_ref = cytovi.CytoVI(adata_reference)
   model_ref.train()
   
   # Transfer annotations to new data
   model_query = cytovi.CytoVI(adata_query)
   model_query.train()
   imputed_categories = model_query.impute_categories_from_reference(
       adata_reference, 
       cat_key='cell_type'
   )
   ```

3. **Surgery-based Transfer Learning**: Although not explicitly shown in this snippet, the ArchesMixin generally provides for:
   - Freezing parts of the network
   - Extending encoders/decoders for new batches
   - Mapping new data to existing latent spaces

## How to Use Transfer Learning

With CytoVI, you would perform transfer learning by:

1. Training a reference model (done)
2. Saving it with `model.save()` (done)
3. Loading it with a new query dataset (done)
4. Either fine-tuning or using as-is for inference 
5. 
For this to work with your large dataset, you could:
5. Train on a well-annotated subset first
6. Use that model to analyze the full dataset with much lower memory requirements

This approach would be particularly valuable given your RAM constraints with a 10-million cell dataset.