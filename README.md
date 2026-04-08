# 6.s985_image_hallucination
**MIT 6.S985 Project | Spring 2026**

This repository contains the codebase and experimental framework for our mechanistic analysis of orthographic hallucinations in **Stable Diffusion XL (SDXL)**. Our research moves beyond black-box benchmarking to localize failure points within the text-encoding and cross-attention manifolds, proposing a targeted mitigation strategy based on these diagnostic findings.

## 🚀 Project Overview

Despite the high-fidelity outputs of latent diffusion models, they frequently fail at rendering precise text, producing "hallucinations" that are misspelled, garbled, or spatially drifted. We decompose this failure into two primary breakdown points:
1.  **Text-Encoding Bottleneck (Exp 1):** Information loss during BPE tokenization and embedding collapse.
2.  **Cross-Attention Misbinding (Exp 2):** Failure of the U-Net to spatially anchor tokens during a critical early denoising window ($t \in [1000, 700]$).

## 🛠️ Key Features

* **Factorial Prompt Suite:** 180 unique conditions across 360 generated images, varying string length, character type (alphanumeric vs. common words), scene complexity, and prompt formatting.
* **Mechanistic Instrumentation:** Custom hooks into the SDXL U-Net to extract:
    * **Spatial Attention Entropy ($H$):** Measuring the diffusion of generative "mass."
    * **Centroid Temporal Drift ($\Delta C$):** Tracking the stability of token-to-pixel grounding.
* **OCR Evaluation Pipeline:** Automated scoring using Normalized Edit Distance (NED) and Character Error Rate (CER) via EasyOCR.
* **Mitigation Strategy:** A proposed fine-tuning objective optimizing for OCR-perceptual feedback and penalizing "non-character" glyph hallucinations.

## 📊 Diagnostic Findings

Our analysis identified a **Critical Window of Stability** in the diffusion process. Success is determined by the model's ability to "lock" a spatial centroid early.
* **The $t=800$ Spike:** All sequences show a decision spike at $t=800$; however, failures exhibit sustained drift long after this window, especially in cluttered scenes.
* **Complexity Paradox:** Cluttered backgrounds compete for the "attention budget," leading to higher entropy and "wandering" text centroids.


## Samples of generated images by the baseline SDXL: 
Watermelon - simple, verbatim:
<img width="789" height="791" alt="Screenshot 2026-04-08 at 12 10 52 AM" src="https://github.com/user-attachments/assets/f5b792de-0571-4a14-8c03-91015977dfda" />

Watermelon - simple, quoted:
<img width="789" height="791" alt="Screenshot 2026-04-08 at 12 11 36 AM" src="https://github.com/user-attachments/assets/c6bfc8c5-69b5-4a8c-ada0-51e6c4bce8c3" />

Watermelon - simple, letterspaced
<img width="789" height="791" alt="Screenshot 2026-04-08 at 12 12 05 AM" src="https://github.com/user-attachments/assets/3abcecc2-db01-4a79-8e40-5273d9fe605a" />

Watermelon - cluttered, verbatim
<img width="789" height="791" alt="Screenshot 2026-04-08 at 12 12 22 AM" src="https://github.com/user-attachments/assets/823136cd-18ed-4af3-8ece-e5890e7e06ef" />

Watermelon - cluttered, letterspaced
<img width="789" height="791" alt="Screenshot 2026-04-08 at 12 12 44 AM" src="https://github.com/user-attachments/assets/feb0b474-4f1c-4dac-b96f-c8f42b177438" />

Watermelon - blank, unquoted
<img width="789" height="791" alt="Screenshot 2026-04-08 at 12 13 11 AM" src="https://github.com/user-attachments/assets/2d3ebca4-c5b8-4ac3-a43d-e91894edb575" />


## 🎓 Team
Nilay, Riddhi, Nicole 
Department of Electrical Engineering and Computer Science, MIT
6.S895 Multimodal AI | Spring 2026 
