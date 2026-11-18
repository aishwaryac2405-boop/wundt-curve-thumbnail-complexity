# Quantifying Visual Interestingness: A Computational Test of the Wundt Curve in Digital Media


**Authors:** M B Thejesshwar and Aishwarya Chakrabarti, Indian Institute of Technology Kharagpur, 2026.


The Wundt Curve proposes an inverted-U relationship between the complexity of a stimulus and its appeal. This project tests that idea on 93 YouTube thumbnails.


## Summary


- **Data:** 93 YouTube videos. For each: thumbnail, view count, channel subscriber count and channel name.
- **Engagement:** log-transformed viral ratio, `Y = log(1 + views / subscribers)`.
- **Complexity measures** (each standardized to a z-score):
  - Edge entropy (Sobel edge map, 10x10 grid)
  - Saliency entropy (spectral-residual saliency map, 50-bin histogram)
  - Object entropy (YOLOv8 detections, object centres over a 5x5 grid)
  - Color entropy (HSV hue distribution, 30 bins)
  - Baseline: raw grayscale pixel entropy (256 bins)
- **Method:** OLS of Y on the four standardized measures gives weights; their fitted value is the Composite Complexity Index E. Then the quadratic `Y = b0 + b1*E + b2*E^2` is estimated. LOWESS smoothers are used as a visual check.


## Results (as reported in the paper)


- Quadratic model in the composite index: F = 6.434, p = 0.00245, with b1 = 1.6467 (positive) and b2 = -1.2800 (negative), consistent with an inverted U. Turning point E* is about 0.64.
- Baseline model with raw pixel entropy: not significant (p = 0.267).
- Color entropy (p = 0.01) and saliency entropy (p = 0.04) are the strongest individual features.
- Because the index weights are estimated on the same outcome, the results are **exploratory**. The paper describes how they should be tested out of sample.


## Files


- `4-Quantifying_Visual_Interestingness_Wundt_Curve.pdf` - the paper.
- `wundt_analysis.py` - analysis code, exported from a Google Colab notebook.


## Running the code


The script was exported from Colab. It uses `google.colab` file upload and a `!pip install` line, so it runs as-is in Colab; elsewhere those parts need adapting. It expects an Excel (`.xlsx`) file of video links with view and subscriber counts, which is not included in this repository. Dependencies: opencv-python-headless, ultralytics (YOLOv8n), scikit-image, statsmodels, openpyxl, pandas, numpy, scipy, matplotlib.

