# CRISPR Comparison

## Background
Off-target effects in CRISPR/Cas-associated gene editing occur when double-strand breaks (DSBs) are introduced at unintended DNA positions. This happens when the guide RNA (gRNA) of the CRISPR/Cas system pairs incorrectly or incompletely with non-target DNA, leading to "right activity at the wrong place." These off-target effects represent a major drawback of CRISPR/Cas technology.

To address this issue, researchers have developed CRISPR systems with enhanced fidelity (fewer off-target effects) and efficiency (higher cutting activity) through approaches like protein engineering and improved gRNA design. However, the performance of these modified systems depends not only on the system itself but also on the genomic region being targeted. As a result, the same system may perform differently when targeting different regions of the genome.

To evaluate system performance, researchers commonly analyse the frequency of DSBs at both on-target and off-target sites. These DSBs can be detected and quantified using wet-lab techniques such as GUIDE-seq or CIRCLE-seq, which utilize next-generation sequencing (NGS) to analyse the edited DNA fragments of the CRISPR-treated cells. These NGS results can be summarized in tables, listing the number of DSBs for each variant and specific target sequence.

In this context, on-target sites are identified as having 0 mismatches (MMs) between the gRNA and the target gene, while off-target sites have one or more mismatches.

## Tool
This repository contains an automation tool that enables you to quickly compare the fidelity and efficiency of different CRISPR/Cas systems and gRNAs based on indel count results derived from Next-Generation Sequencing (NGS) data.

### Data Frame Structure
To utilize the automation tool effectively, the input Data Frame must adhere to the following structure:
- **MMs**: A column indicating the presence of mismatches called ‘MMs’.
- **gRNA**: A column containing the names of the gRNAs including the term ‘gRNA’.
- **Variant Columns**: Columns for each variant, with the names including the term "Cas" or "Variant".

### MMs Column Explanation
The MMs column serves to indicate the presence of mismatches in the NGS data:
- A value of `0` indicates no mismatches (perfect match).
- A value of `!= 0` indicates the presence of mismatches (indicating potential off-target effects).

---

### Calculating Fidelity and Efficiency

#### For Variants
- **Fidelity**: Calculated as the ratio of summed on-target indels to the total summed indels (both on-target and off-target) for each variant:

$$
Fidelity = \frac{\text{Summed On-Target Indels}}{\text{Summed On-Target Indels} + \text{Summed Off-Target Indels}}
$$

- **Efficiency**: Measured as the ratio of summed on-target indels to the average on-target count across all variants:

$$
Efficiency = \frac{\text{Summed On-Target Indels}}{\text{Average On-Target Count per Variant}}
$$

#### For gRNAs
- **Fidelity**: Evaluated as the ratio of summed on-target indels generated by each gRNA to the total off-target indels:

$$
Fidelity = \frac{\text{Summed On-Target Indels (gRNA)}}{\text{Summed On-Target Indels (gRNA)} + \text{Summed Off-Target Indels (gRNA)}}
$$

- **Efficiency**: Calculated as the ratio of total on-target indels produced by a gRNA to the average on-target indel count:

$$
Efficiency = \frac{\text{Total On-Target Indels (gRNA)}}{\text{Average On-Target Count (gRNA)}}
$$

---

### Output Overview
- **On-Target Indels Table**: Summarizes the number of successful edits for each gRNA and variant.
- **Off-Target Indels Table**: Details potential unintended edits caused by each gRNA and variant.
- **Fidelity and Efficiency Plot**: A visual representation comparing the fidelity and efficiency of various variants.
- **gRNA Fidelity and Efficiency Table**: Lists the fidelity and efficiency metrics for each gRNA, aiding in the selection of optimal guide RNAs for targeted genome editing.

---

## How to Use

### Try the App
[Click here to use the app](https://crispr-comparison-fbvvn6l8s6vads2mvj5oag.streamlit.app)

#### Features
- Upload Excel files with CRISPR data.
- View dynamically generated plots for fidelity vs. efficiency.
- Download processed results.

#### Example Data Frame
To get started quickly, you can download an example Excel file that fits the required structure for this tool:

[Download Example Data Frame](https://raw.githubusercontent.com/Michaeog/CRISPR-Comparison/main/example_data.xlsx)

This file contains sample data with the correct columns (`gRNA`, `MMs`, and `variants`), and you can upload it directly to the app to test the tool's functionality.

### How to Start the App Locally
1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/your-repository.git
2. pip install -r requirements.txt
3. streamlit run app.py

#### Make sure your Data Frame fits the structure mentioned above









