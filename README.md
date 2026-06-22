# AI-Driven-Lithology-Prediction-from-Well-Logs (FORCE 2020 North Sea Dataset)
This project delivers a machine learning pipeline that automatically predicts subsurface rock types (lithology) directly from raw geophysical well log measurements, acting as an intelligent assistant to accelerate subsurface mapping and reduce human error in complex structural basins.

# Project Overview
Determining what lies thousands of meters beneath the earth's surface is one of the most challenging aspects of subsurface exploration. Traditionally, geologists manually interpret wireline logs—a process that is both time-consuming and prone to subjective bias.

This project develops an end-to-end machine learning pipeline that automatically predicts subsurface rock types (lithology) directly from raw geophysical well log measurements. By treating lithology classification as a supervised machine learning problem, this model acts as an automated "petrophysical assistant," accelerating subsurface mapping and reducing human error in complex structural basins.

# Dataset Description & Acquisition
The model is trained on the highly recognized FORCE 2020 Well Logging Dataset, which was acquired directly via Kaggle.
This data primarily focuses on the Hordaland Group in the Norwegian sector of the North Sea. The Hordaland Group is geologically famous for its thick, massive mudstone and shale sequences, interspersed with localized sandstone channels and carbonate streaks.

This dataset reflects true real-world conditions: it is highly imbalanced (dominated by massive shale sequences with very few rare rock types like coal or tuff) and contains realistic gaps in tool measurements (missing data matrix).

# Methodology
The pipeline is engineered to mimic a rigorous petrophysical workflow, ensuring data is conditioned properly before it ever reaches the algorithm:

6 core wireline logs are targeted that capture distinct physical properties of the formation: Gamma Ray (GR), Bulk Density (RHOB), Neutron Porosity (NPHI), Photoelectric Factor (PEF), Acoustic/Sonic Travel Time (DTC), and Medium Resistivity (RMED).

Since resistivity data naturally spans a massive exponential scale, I applied a log10 transformation to RMED to smooth out the range and make it easier for the model to handle. I also used a median-based SimpleImputer to clean up any missing data gaps caused by tool failures downhole.

To combat the massive class imbalance inherent to the North Sea geology, a Random Forest Classifier was trained using class_weight='balanced'. This forces the trees to penalize misclassifications on rare facies, preventing the model from simply guessing the dominant rock type.

# Results & Discussion
The baseline model achieved an exceptional Overall Validation Accuracy of 95.84%.

# The Confusion Matrix Analysis
While the overall metric is high, evaluating the confusion matrix reveals that the model is learning genuine sedimentary physics:
1. High-Stakes Targets: The model flawlessly isolates major shale sequences and clean reservoir sandstones. It even successfully identifies rare volcanic Tuff (99000) layers despite having minimal examples.
2. Geological Continuous Transitions: Minor misclassifications are concentrated where physical tool signatures naturally overlap in nature—such as mistaking Marl (80000) (clay-rich limestone) for pure Limestone (70000).

To ensure the model isn't a "black box," feature importance was extracted.

1. DTC (Sonic Travel Time) emerged as the primary feature, effectively capturing the structural compaction and depth-dependent hardness framework of the Hordaland Group.
2. GR (Gamma Ray) ranked as a close second, validating the model’s reliance on the classic petrophysical baseline to distinguish radioactive shales from clean reservoir facies.

# Sustainability and Future outlook
While lithology prediction has historical roots in fossil fuel extraction, this exact pipeline serves a critical role in the Green Energy Transition:

1. Carbon Capture & Storage (CCS): Safely storing CO2 underground requires finding perfect reservoirs (highly porous sandstones) trapped beneath completely impermeable seals (dense shales). This model drastically accelerates the scanning of depleted basins to find safe, leak-proof storage sites.
2. Geothermal Energy Exploration: Identifying high-porosity formations and highly conductive basement transitions is crucial for locating viable geothermal reservoirs.Subsurface
3. Hydrology: The ability to instantly map interbedded sandstone and shale sequences allows for better management of critical groundwater aquifers and helps mitigate contamination risks.

---------------------------------------------------------------*-----------------------------------------------------------------------------------------------
