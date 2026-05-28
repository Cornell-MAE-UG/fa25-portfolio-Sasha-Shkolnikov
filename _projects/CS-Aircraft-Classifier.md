---
layout: project
title: "Aircraft Image Classifier"
description: "ML Data Pipeline Architecture Study for Fine-Grained Aircraft Classification"
technologies:
  - Python
  - EfficientNet-B0
  - PyTorch
  - Data Engineering
  - FGVC-Aircraft Dataset
image: /assets/images/AI-Demo-SR20-Main.png
---

<br><br><br><br><br><br>

<details open>
<summary><strong>Overview</strong></summary>

<br>

This project explored the tradeoffs between three different data pipeline architectures for fine-grained aircraft image classification, applied to the FGVC-Aircraft 2013b dataset (70 aircraft families, ~7,500 images). The backbone model was EfficientNet-B0 pretrained on ImageNet, fine-tuned for the aircraft classification task.

The three pipelines — Main (on-the-fly augmentation), Augmented (pre-generated offline augmentation), and Feature-Cache (frozen backbone embeddings) — were implemented end-to-end with a consistent project structure modeled on production data pipeline stages: ingestion, processing, storage, analysis, visualization, and orchestration.

<p>

  <a href="https://github.com/Sasha-Shkolnikov/AircraftClassification/blob/main/aircraft_pipeline/pipeline_report.html" target="_blank"><i class="bi bi-bar-chart-fill"></i> Interactive Data Visualization Report</a>
</p>

</details>

---

<details open>
<summary><strong>Data Pipeline Architecture</strong></summary>

<br>

The pipeline was designed around standard ELT principles: transformations happen after loading, so changes to augmentation or preprocessing schemes don't require re-ingesting raw images. Each stage maps directly to a module in the project:

<figure style="text-align:center;">
  <img src="{{ '/assets/images/AI-Pipeline-Table.png' | relative_url }}"
       alt="Pipeline stage to file mapping"
       style="width:100%; max-width:700px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Pipeline stages and their corresponding implementation files
  </figcaption>
</figure>

<br>

Key design decisions:
<ul>
  <li><strong>ELT over ETL:</strong> Transformations applied post-load so augmentation schemes can be changed without re-ingestion.</li>
  <li><strong>DAG orchestration:</strong> Directed acyclic graph structure (analogous to Airflow) ensures no cyclic dependencies between pipeline stages.</li>
  <li><strong>Data virtualization ruled out:</strong> No control over the source image repository, so virtual pointers to source data were not feasible.</li>
</ul>

</details>

---

<details open>
<summary><strong>Dataset & Preprocessing</strong></summary>

<br>

Raw images from the FGVC-Aircraft 2013b dataset were ingested and resized to 224×224 to match the EfficientNet input resolution. Images failing quality filters were discarded during processing.

<div style="display:flex; gap:16px; justify-content:center; align-items:flex-end; flex-wrap:wrap; margin-bottom:0.5rem;">
  <figure style="text-align:center; margin:0;">
    <img src="{{ '/assets/images/AI-Raw-Sample.png' | relative_url }}" alt="Raw source image" style="height:180px; width:auto; display:block; margin:auto;">
    <figcaption style="font-size:0.85em; color:#555; margin-top:4px;">Raw source image</figcaption>
  </figure>
  <figure style="text-align:center; margin:0;">
    <img src="{{ '/assets/images/AI-Aug-Clean.png' | relative_url }}" alt="Processed 224×224" style="height:180px; width:auto; display:block; margin:auto;">
    <figcaption style="font-size:0.85em; color:#555; margin-top:4px;">Processed (224×224)</figcaption>
  </figure>
  <figure style="text-align:center; margin:0;">
    <img src="{{ '/assets/images/AI-Aug-1.png' | relative_url }}" alt="Augmented variant 1" style="height:180px; width:auto; display:block; margin:auto;">
    <figcaption style="font-size:0.85em; color:#555; margin-top:4px;">Augmented variant</figcaption>
  </figure>
  <figure style="text-align:center; margin:0;">
    <img src="{{ '/assets/images/AI-Aug-2.png' | relative_url }}" alt="Augmented variant 2" style="height:180px; width:auto; display:block; margin:auto;">
    <figcaption style="font-size:0.85em; color:#555; margin-top:4px;">Augmented variant</figcaption>
  </figure>
</div>

</details>

---

<details open>
<summary><strong>Three Pipeline Architectures</strong></summary>

<br>

<table style="width:95%; border:1px solid #000; border-collapse:collapse; text-align:left;">
  <tr>
    <th style="padding:6px;">Pipeline</th>
    <th style="padding:6px;">Approach</th>
    <th style="padding:6px;">Train Images</th>
    <th style="padding:6px;">Avg Epoch</th>
    <th style="padding:6px;">Val Accuracy</th>
  </tr>
  <tr>
    <td style="padding:6px;"><strong>Main</strong></td>
    <td style="padding:6px;">8 random augmentations applied live per batch (stochastic)</td>
    <td style="padding:6px;">~3,300</td>
    <td style="padding:6px;">~98 s</td>
    <td style="padding:6px;"><strong>77.7%</strong></td>
  </tr>
  <tr>
    <td style="padding:6px;"><strong>Augmented</strong></td>
    <td style="padding:6px;">4 augmented copies pre-generated per image, fixed before training</td>
    <td style="padding:6px;">~16,700</td>
    <td style="padding:6px;">~225 s</td>
    <td style="padding:6px;"><strong>83.7%</strong></td>
  </tr>
  <tr>
    <td style="padding:6px;"><strong>Feature-Cache</strong></td>
    <td style="padding:6px;">Backbone frozen; 1280-dim EfficientNet embeddings cached, only classifier head trained</td>
    <td style="padding:6px;">~7,500 embeddings</td>
    <td style="padding:6px;">~1.2 s</td>
    <td style="padding:6px;"><strong>51.0%</strong></td>
  </tr>
</table>

<br>

The Feature-Cache pipeline compresses each image into a 1280-dimensional EfficientNet embedding stored as a `.npy` file, enabling extremely fast training (23 seconds total) at the cost of accuracy — the frozen backbone cannot adapt its representations to the aircraft domain.

<figure style="text-align:center;">
  <img src="{{ '/assets/images/AI-Feature-Embedding.png' | relative_url }}"
       alt="1280-dim EfficientNet feature embedding for a sample aircraft image"
       style="width:100%; max-width:750px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    1280-dim EfficientNet embedding for a sample image — sparse activations with a heavy left-tail distribution
  </figcaption>
</figure>

<figure style="text-align:center; margin-top:1.5rem;">
  <img src="{{ '/assets/images/AI-Architecture-Comparison.png' | relative_url }}"
       alt="Architecture comparison table across all three pipelines"
       style="width:100%; max-width:800px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Full architecture comparison: dataset class, augmentation strategy, reproducibility, epoch time, and disk usage
  </figcaption>
</figure>

<figure style="text-align:center; margin-top:1.5rem;">
  <img src="{{ '/assets/images/AI-Learning-Curves.png' | relative_url }}"
       alt="Validation accuracy vs epoch for all three pipelines"
       style="width:100%; max-width:800px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Validation accuracy vs. epoch — backbone unfrozen at epoch 5 for Main and Augmented, driving the sharp accuracy jump. Feature-Cache stays flat as the backbone remains frozen throughout.
  </figcaption>
</figure>

</details>

---

<details>
<summary><strong>Classification Demo: SR-20</strong></summary>

<br>

The SR-20 is a visually ambiguous aircraft at fine-grained resolution. Only the Augmented pipeline correctly identified it — the Main pipeline confused it for a Cessna 172, and the Feature-Cache pipeline predicted a PA-28.

<div style="display:flex; flex-direction:column; gap:10px; max-width:700px; margin:auto;">
  <figure style="text-align:center; margin:0;">
    <img src="{{ '/assets/images/AI-Demo-SR20-Main.png' | relative_url }}" alt="Main pipeline: SR-20 predicted as Cessna 172" style="width:100%;">
    <figcaption style="font-size:0.85em; color:#555; margin-top:4px;">Main (77.7% val accuracy) — predicts Cessna 172 @ 18.1% confidence ✗</figcaption>
  </figure>
  <figure style="text-align:center; margin:0;">
    <img src="{{ '/assets/images/AI-Demo-SR20-Augmented.png' | relative_url }}" alt="Augmented pipeline: SR-20 correctly identified" style="width:100%;">
    <figcaption style="font-size:0.85em; color:#555; margin-top:4px;">Augmented (83.7% val accuracy) — predicts SR-20 @ 42.2% confidence ✓</figcaption>
  </figure>
  <figure style="text-align:center; margin:0;">
    <img src="{{ '/assets/images/AI-Demo-SR20-Cache.png' | relative_url }}" alt="Feature-Cache pipeline: SR-20 predicted as PA-28" style="width:100%;">
    <figcaption style="font-size:0.85em; color:#555; margin-top:4px;">Feature-Cache (51.0% val accuracy) — predicts PA-28 @ 56.8% confidence ✗</figcaption>
  </figure>
</div>

</details>

---

<details>
<summary><strong>Classification Demo: Boeing 747</strong></summary>

<br>

The 747 is visually distinctive and all three pipelines correctly identified it, but with very different confidence levels — illustrating how overall accuracy correlates with per-prediction confidence even on "easy" classes.

<div style="display:flex; flex-direction:column; gap:10px; max-width:700px; margin:auto;">
  <figure style="text-align:center; margin:0;">
    <img src="{{ '/assets/images/AI-Demo-747-Main.png' | relative_url }}" alt="Main pipeline: 747 at 28.7% confidence" style="width:100%;">
    <figcaption style="font-size:0.85em; color:#555; margin-top:4px;">Main — Boeing 747 @ 28.7% confidence ✓</figcaption>
  </figure>
  <figure style="text-align:center; margin:0;">
    <img src="{{ '/assets/images/AI-Demo-747-Augmented.png' | relative_url }}" alt="Augmented pipeline: 747 at 88.3% confidence" style="width:100%;">
    <figcaption style="font-size:0.85em; color:#555; margin-top:4px;">Augmented — Boeing 747 @ 88.3% confidence ✓</figcaption>
  </figure>
  <figure style="text-align:center; margin:0;">
    <img src="{{ '/assets/images/AI-Demo-747-Cache.png' | relative_url }}" alt="Feature-Cache pipeline: 747 at 15.4% confidence" style="width:100%;">
    <figcaption style="font-size:0.85em; color:#555; margin-top:4px;">Feature-Cache — Boeing 747 @ 15.4% confidence ✓</figcaption>
  </figure>
</div>

</details>

---

<details>
<summary><strong>Performance & Tradeoffs</strong></summary>

<br>

<figure style="text-align:center;">
  <img src="{{ '/assets/images/AI-Performance-Cards.png' | relative_url }}"
       alt="Performance summary across all three pipelines"
       style="width:100%; max-width:800px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Performance summary: accuracy, epochs, training time, and dataset size for each pipeline
  </figcaption>
</figure>

<figure style="text-align:center; margin-top:1.5rem;">
  <img src="{{ '/assets/images/AI-Tradeoff.png' | relative_url }}"
       alt="Accuracy vs training speed tradeoff across the three pipelines"
       style="width:100%; max-width:750px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Accuracy vs. training speed (log scale) — bubble size represents training dataset size. Augmented dominates on accuracy; Feature-Cache is ~100× faster but bottoms out at 51%.
  </figcaption>
</figure>

<figure style="text-align:center; margin-top:1.5rem;">
  <img src="{{ '/assets/images/AI-Confusion-Matrix.png' | relative_url }}"
       alt="Confusion matrices for all three pipelines"
       style="width:100%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Confusion matrices for Main (77.7%), Augmented (83.7%), and Feature-Cache (51.0%) — each showing top confused pairs and lowest per-class accuracy
  </figcaption>
</figure>

<br>

The Feature-Cache pipeline's low accuracy (~51%) reveals the cost of a frozen backbone: EfficientNet representations pretrained on ImageNet are not fine-grained enough to distinguish aircraft subcategories without end-to-end fine-tuning. The Augmented pipeline achieves the best accuracy (83.7%) by maximizing training data diversity, but requires 5× more storage and ~2.5× longer training per epoch. The Main pipeline offers the best balance for this task: reasonable accuracy (77.7%) with minimal overhead.

</details>

---

<details>
<summary><strong>Future Work</strong></summary>

<br>

<ul>
  <li><strong>Confidence floor / abstention:</strong> Add a minimum confidence threshold below which the model returns "uncertain" rather than a forced top-1 prediction. This improves reliability for ambiguous inputs and partially handles out-of-distribution cases — if a user uploads an aircraft family not in the 70 supported classes, the model's softmax scores will be spread thin and uniformly low, so a confidence floor would correctly decline to predict rather than returning a confidently wrong answer.</li>
</ul>

</details>
