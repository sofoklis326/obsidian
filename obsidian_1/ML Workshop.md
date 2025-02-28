#### Free Response Operating Characteristic (FROC) Curve[](https://monkey.grand-challenge.org/evaluation-ranking-2/#free-response-operating-characteristic-froc-curve "Permanent link")

The FROC curve plots the **true positive rate (TPR, a.k.a. sensitivity or recall) on the y-axis** against the **average number of false positives (FP) per mm² over all slides on the x-axis.** It is thus an alternative to the ROC curve, where the x-axis plots the false positive rate instead. Based on this definition, we will compute the TP, FP, and false negatives (FN) and use them in the FROC analysis. The TPR is defined as TP/(TP+FN).

The score computation may be fine-tuned during the challenge to compare the best methods better.
https://en.wikipedia.org/wiki/Periodic_acid%E2%80%93Schiff_stain
https://en.wikipedia.org/wiki/Immunohistochemistry
https://github.com/facebookresearch/detectron2

Selfsupervised Learning/Foundation Models/Existing segmentation models
https://medium.com/@anuj.dutt9/emerging-properties-in-self-supervised-vision-transformers-dino-paper-summary-4c7a6ed68161