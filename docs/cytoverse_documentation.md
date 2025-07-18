# CytoVerse Documentation

**An Interactive Flow Cytometry Analysis Platform**

---

## Table of Contents

1. [Introduction](#introduction)
2. [Getting Started](#getting-started)
3. [Settings](#settings)
4. [Spillover Compensation](#spillover-compensation)
5. [Interactive Gating](#interactive-gating)
6. [Raw Data Analysis](#raw-data-analysis)
7. [Batch Analysis](#batch-analysis)
8. [Processed Data](#processed-data)
9. [Troubleshooting](#troubleshooting)
10. [FAQ](#faq)

---

## Introduction

CytoVerse is a powerful, web-based flow cytometry analysis platform designed to streamline your cytometry workflow from raw data processing to publication-ready results. Whether you're analyzing single samples or processing large batch experiments, CytoVerse provides the tools you need for flow cytometry analysis in an interactive platform.

### Key Features

- **📊 Comprehensive Analysis Pipeline**: From spillover compensation to advanced clustering
- **🔧 Interactive Gating**: Intuitive hierarchical gating with real-time statistics
- **📈 Advanced Visualization**: Multiple plot types optimized for flow cytometry data
- **⚡ Batch Processing**: Analyze dozens of samples simultaneously with standardized parameters
- **🎨 Customizable Plots**: Publication-ready figures with extensive customization options
- **💾 Template System**: Save and reuse analysis workflows for consistent results

### Typical Workflow

1. **Upload & Preprocess**: Load raw FCS files and apply quality control
2. **Compensation**: Remove fluorophore spillover using control files
3. **Gating**: Define cell populations through hierarchical gating
4. **Analysis**: Apply dimensionality reduction and clustering algorithms
5. **Export**: Generate publication-ready results and statistics

---

## Getting Started

### System Requirements

CytoVerse runs in your web browser and supports:
- **Browsers**: Chrome, Firefox, Safari, Edge (latest versions)
- **File Formats**: .fcs, .csv, .tsv, .xlsx
- **File Size**: Up to 250MB per upload session

### Quick Start Guide

1. **Access CytoVerse** through your web browser
2. **Start with Settings** to configure global plot preferences
3. **Upload your data** in the Raw Data tab
4. **Apply compensation** if using multi-color panels
5. **Gate your populations** using Interactive Gating
6. **Analyze and export** your results

---

## Settings

### Global Plot Settings

This allows the plots to be visually adjusted. The width and height of the plot can be changed accordingly by dragging the pointer along the scale. Similarly, by dragging on the pointer on the scale, moving left or right the font size as well as the sizes of the points on the graph can be changed. Finally, the color palette can be customized by selecting the color circle next to the palette selector. The tool offers a variety of options, including colorblindfriendly palettes, as well as categorical, sequential, and diverging schemes to enhance data interpretation.

**Plot Dimensions:**
- **Width/Height**: Drag the pointer along the scale to adjust plot size (default: 800x600 pixels)
- **Optimal for presentations**: 1024x768 pixels
- **Optimal for publications**: 600x400 pixels (fits journal requirements)

**Typography:**
- **Font Size**: Drag the pointer on the scale left or right to adjust text size for better readability (range: 8-24px)
- **Point Size**: Drag the pointer to control data point visibility (range: 1-12px)
- **Recommended for dense data**: Smaller point sizes (2-4px)
- **Recommended for presentations**: Larger point sizes (6-8px)

**Color Palettes:**
Customize by selecting the **color circle next to the palette selector**. Choose from scientifically-optimized color schemes:
- **Viridis/Plasma/Magma**: Perceptually uniform, colorblind-friendly
- **Sequential palettes**: Best for density plots and continuous data
- **Categorical palettes**: Ideal for discrete populations
- **Diverging palettes**: Perfect for fold-change and comparison data

---

## Spillover Compensation

### Overview

**What is spillover compensation?**
Spillover occurs when fluorophores emit light that bleeds into adjacent detection channels, creating false positive signals. Compensation mathematically corrects this by subtracting the spillover signal from each channel based on control measurements.

### Step 1: Upload Files

1. Click **"Browse FCS Files"** to upload:
   - **Unstained control** (required): Cells with no fluorescent staining - establishes baseline autofluorescence
   - **Single-stain controls** for each fluorophore (minimum 2 required): Cells stained with only one fluorophore each - measures spillover from that specific fluorophore into other channels
   - **Experimental samples**: Your actual samples with multiple fluorophores

2. **Auto-detected channel formats:**
   - FL formats: FL1-A, FL2-H, FL3-W
   - Laser wavelength: 405 D 525_50-A, 488/530-A
   - FJComp formats: FJ-Comp-A, Comp-PE-A
   - Fluorophore names: FITC-A, PE-H, BV421-A
   - Marker combinations: CD3-FITC-A

### Step 2: Assign File Roles

1. **Select unstained control** from uploaded files
2. **Assign single-stain controls** to each detected channel
3. Click **"Validate File Assignment"** to save assignments

### Step 3: Generate Compensation Matrix

**What is a compensation matrix?**
A mathematical matrix that defines how much signal from each fluorophore spills into other channels. The system uses this to subtract spillover signals from your experimental data.

**Option A: Auto-compute**
- Click **"Compute Spillover Matrix"**
- System automatically calculates using **median method** (uses median fluorescence values from single-stain controls to be robust against outliers)

**Option B: Import existing matrix**
- Upload .csv or Excel (.xlsx) file with pre-calculated compensation values
- Matrix must be square with fluorophores as row/column names
- Useful when you have standardized compensation from instrument software

### Step 4: Review & Edit Matrix

- **Color coding:**
  - 🟢 Green: Low spillover (0-1%)
  - 🟡 Yellow: Moderate (1-5%)
  - 🟠 Orange: High (5-10%)
  - 🔴 Red: Very high (>10%)
- Enable editing to modify values manually
- Click **"Reset to Original"** to undo changes

### Step 5: Quality Control

1. **Select channels** to analyze (subset of compensated channels)
2. **Set sample size** (1,000-50,000 events) - smaller samples = faster processing
3. Click **"Run QC Analysis"**

**Key QC metrics explained:**
- **Negative events percentage**: Should be <5% after compensation. High percentages indicate over-compensation or poor controls
- **Signal spread (CV)**: Coefficient of variation measures how tight your positive population is. Lower CV = better separation
- **Before/after comparison**: Visual check that compensation improved channel separation without creating artifacts

**What good compensation looks like:**
- Positive populations shift toward axes (less spillover)
- Negative populations stay near zero
- No new negative populations created

### Step 6: Export Results

- **Compensated FCS files**: Download with "_compensated" suffix
- **Spillover matrix**: Export as CSV or Excel
- **Session data**: Save complete workflow for later use

---

## Interactive Gating

### Overview

**What is gating?**
Gating is the process of selecting specific cell populations based on their fluorescence or scatter properties. You draw boundaries (gates) around populations of interest to separate them from other cells for analysis.

**Why use hierarchical gating?**
Start with broad populations (e.g., live cells) and progressively refine to specific subsets (e.g., CD4+ T cells). This ensures accurate population identification and reduces background interference.

### Step 1: Setup Data Source

**Choose one:**
- Use preprocessed data from Raw Data tab
- Load new FCS files directly

**Select parameters:**
- Sample from dropdown
- X and Y axis channels for 2D plots

### Step 2: Create Gates

1. **Enter population name**
2. **Select gate type**
3. Click **"Start Gating"**
4. **Draw gate:**
   - **Static mode**: Click points or use brush selection
   - **Interactive mode**: Use plotly toolbar (box/lasso select)
5. Click **"Save Gate"** when complete

### Step 3: Visualization Options

**Plot modes explained:**
- **Static mode**: Shows all events simultaneously, better performance for large datasets (>10,000 events). Recommended for most gating tasks
- **Interactive mode**: Limited to 10,000 randomly sampled events but provides full zoom, pan, and selection tools. Use when you need precise navigation

**Plot types and when to use them:**
- **Scatter plot**: Basic dot plot showing individual events. Best for small datasets or when you need to see every single event
- **Density hotspots**: Points colored by local cell density (red = high density, blue = low). Excellent for identifying main populations and rare events
- **Hotspots + contours**: Combines density coloring with population boundary lines. Ideal for complex samples with multiple overlapping populations
- **Hexagon plot**: Divides plot into hexagonal bins showing event counts. Essential for very large datasets (>100,000 events) where individual points would overlap

### Step 4: Hierarchical Gating

**How hierarchy works:**
- **Start with "root"** (all events in your sample)
- **Select parent population** for sub-gating (e.g., gate lymphocytes from root, then CD4+ cells from lymphocytes)
- **View hierarchy tree** with real-time counts showing how populations relate to each other
- **Edit/delete gates** - changes automatically update all downstream populations

**Understanding population statistics:**
- **Event count**: Absolute number of events in this population
- **% of parent**: What percentage of the immediate parent population this represents
- **% of total**: What percentage of all original events this represents
- **Hierarchy depth**: Shows how many gating steps deep you are (root → lymphocytes → CD4+ T cells = 3 levels)

### Step 5: Population Analysis

**Real-time statistics:**
- Event counts per population (updates as you modify gates)
- Percentage of parent and total events
- Hierarchical organization showing parent-child relationships

**Data extraction explained:**
- **Select specific populations**: Choose which gated populations to export for further analysis
- **Extract as flowSet objects**: FlowSet is a standard R/Bioconductor data structure containing flow cytometry data that can be used in downstream analysis software
- **Apply all gates**: Ensures your extracted data includes all gating decisions in the hierarchy

### Step 6: Export & Templates

**Export options:**
- **Gated FCS files**: Individual populations as new files
- **Gate definitions**: Coordinates and parameters (CSV)
- **Population statistics**: Counts and percentages

**Template management:**
- Save gating strategies for reuse
- Load templates for standardized workflows

---

## Raw Data Analysis

The Raw Data module serves as your starting point for flow cytometry analysis, providing essential preprocessing and initial visualization capabilities.

### File Upload

**Upload Data Tab:**
Click on the **grey tab** to upload a raw file with an **.fcs, .tsv or .csv extension**.

**Supported Formats:**
- **.fcs**: Flow Cytometry Standard files (recommended)
- **.csv/.tsv**: Comma/tab-separated values with proper headers

**Upload Process:**
1. Click the **grey upload tab**
2. Select your file using the file browser
3. Wait for upload confirmation
4. Verify file contents in the Data Preview tab

### Spillover Compensation

**When to use:** Multi-color flow cytometry panels with potential fluorophore overlap.

**Enable compensation:**
- Click on the **empty box** to enable/apply spillover compensation to the raw data
- Requires pre-computed compensation matrix from Spillover Compensation module
- Applied automatically to all selected channels

### Data Transformation

**Arcsinh Transformation:**
Flow cytometry data often requires transformation to handle the wide dynamic range and improve visualization.

**Configuration:**
- **Enable transformation**: Click on the box to apply the arcsinh transformation
- **Cofactors**: To edit the transformation cofactors and number of events to analyze, **manually type in the desired number** or **increase/decrease the amount by clicking on the up or down arrow** beside the listed number
- **Events to analyze**: Set sampling size for performance optimization

**When to adjust cofactors:**
- **High cofactors (500-1000)**: For dim markers or autofluorescence
- **Low cofactors (50-150)**: For bright, well-separated populations

### Dimensionality Reduction

**Method Selection:**
Select the dimensionality reduction method(s) to apply to the raw data. **To apply multiple methods, check the corresponding boxes** for each desired option.

**Available Methods:**

**t-SNE (t-Distributed Stochastic Neighbor Embedding):**
- **Best for**: Revealing local population structure and rare cell types
- **Perplexity**: This can be adjusted by **typing in the preferred perplexity**
- **Barnes-Hut approximation**: Can be **added or removed by clicking on the box** - this speeds up t-SNE on large datasets
- **Barnes-Hut theta**: Can be adjusted between 0-1 by **dragging the pointers on the scale** towards the desired number. This tuning parameter allows for better accuracy-speed trade-off in the Barnes-Hut approximation in t-SNE. **Increased number = better approximation** during t-SNE processing
- **Max iterations**: The maximum number of iterations can be adjusted either by **entering a desired value manually** or by **using the up/down arrows** to increase or decrease the value

**UMAP (Uniform Manifold Approximation and Projection):**
- **Best for**: Preserving both local and global structure
- **N-neighbors**: Can be adjusted either by **entering a desired value manually** or by **using the up/down arrows** to increase or decrease the value
- **Faster than t-SNE** for large datasets

**PCA (Principal Component Analysis):**
- **Best for**: Linear dimensionality reduction and noise reduction
- **Number of components**: Can also be adjusted either by **entering a desired value manually** or by **using the up/down arrows** to increase or decrease the value
- **Linear method**: Preserves linear relationships

### Quality Control and Gating

**Debris Removal:**
**Debris and dead cell gating can be enabled by selecting the checkbox** next to the option.

**Configuration:**
- **FSC/SSC Parameters**: **Specify the forward and side scatter parameters using commas to separate each one**
  - Example: "FSC-A, SSC-A" or "Forward Scatter, Side Scatter"
- **Live/Dead Parameter**: **Select the desired live/dead parameters from the dropdown list**
  - **If neither live nor dead parameter is required, click "none"**

### Clustering Analysis

**Enable Clustering:**
**By clicking on 'enable clustering'** more clustering options will become available.

**Clustering Methods:**
**By clicking on the dropdown list**, there are options to choose the type of clustering methods to apply to the dataset.

**K-means:**
- **Number of clusters**: **Can be manually put in** - allows the number of clusters to be predefined
- **Best for**: Well-separated, spherical populations
- **Tip**: Start with expected number of major populations

**DBSCAN:**
- **Epsilon and Min pts**: **Can be set individually to the desired number manually**
- **Epsilon**: Controls density sensitivity 
- **Min pts**: Min number of points required within the radius to be considered a cluster 
- **Best for**: Irregularly shaped populations
- **Handles noise**: Automatically identifies outliers

**FlowSOM:**
- **SOM Grid X dimension**: **Can input the desired number of nodes horizontally by entering a desired value manually** or by **using the up/down arrows** to increase or decrease the value
- **SOM Grid Y dimension**: **Can input the desired number of nodes vertically by entering a desired value manually** or by **using the up/down arrows** to increase or decrease the value
- **Metacluster**: **Can input the number of meta clusters by entering a desired value manually** or by **using the up/down arrows** to increase or decrease the value. **Controls second level of clustering**
- **Training iterations**: **Define the numbers of how many times the SOM training algorithm will update** - by **entering a desired value manually** or by **using the up/down arrows** to increase or decrease the value
- **Best for**: Flow cytometry-specific hierarchical analysis

---

## Batch Analysis

### Overview

**What is batch analysis?**
Batch analysis allows you to process multiple flow cytometry samples simultaneously with standardized parameters. This ensures consistent analysis across experimental groups and enables statistical comparisons between samples and conditions.

**Why use batch analysis?**
- **Consistency**: Apply identical processing parameters across all samples
- **Efficiency**: Process dozens of samples at once instead of one by one
- **Comparison**: Generate standardized results for statistical analysis between groups
- **Reproducibility**: Save processing templates for future experiments

### Step 1: Sample Management

1. **Upload multiple files**:
   - Click **"Browse Files"** to select multiple .fcs, .csv, or .tsv files
   - Files can be from different experimental groups or conditions
   - Each file becomes a separate sample in your batch

2. **Automatic grouping** (optional):
   - **Filename pattern grouping**: Files are automatically assigned to groups based on naming patterns
   - **Control pattern**: Enter text pattern that identifies control samples (e.g., "ctrl", "control")
   - **Treated pattern**: Enter text pattern that identifies treated samples (e.g., "treat", "stim")
   - **Manual grouping**: Assign groups manually if automatic detection doesn't work

3. **Sample list management**:
   - View all uploaded samples with their assigned groups
   - **Remove individual samples** or **clear entire batch**
   - Check sample details before processing

### Step 2: Configure Batch Processing Parameters

**Preprocessing options:**
- **Spillover compensation**: Apply compensation matrices to all samples (requires pre-computed matrix)
- **Data transformation**: Choose arcsinh transformation with configurable cofactors
- **Channel selection**: Select which fluorescence channels to include in analysis
- **Event sampling**: Set number of events to analyze per sample (for performance)

**Quality control gating:**
- **Debris removal**: Automatically gate out debris based on FSC/SSC parameters
- **Dead cell exclusion**: Use live/dead markers to exclude non-viable cells
- **FSC/SSC parameters**: Specify forward and side scatter channel names
- **Live/dead parameter**: Select viability marker from dropdown

### Step 3: Dimensionality Reduction

**Choose reduction method** for visualization:

**t-SNE parameters:**
- **Perplexity**: Controls local vs. global structure balance (default: 30, range: 5-50)
- **Barnes-Hut approximation**: Speeds up processing for large datasets
- **Barnes-Hut theta**: Accuracy vs. speed trade-off (0-1, higher = faster but less accurate)
- **Max iterations**: Number of optimization steps (default: 1000)

**UMAP parameters:**
- **N-neighbors**: Controls local neighborhood size (default: 15, affects local vs. global structure)
- **Min distance**: Minimum distance between points in embedding
- **Metric**: Distance metric for high-dimensional space

**PCA parameters:**
- **Number of components**: How many principal components to calculate (default: 2 for visualization)

### Step 4: Clustering Analysis

**Enable clustering** to identify cell populations automatically:

**Clustering methods:**

**K-means:**
- **Number of clusters**: Pre-define how many populations to find
- **Best for**: Well-separated, roughly spherical populations
- **When to use**: When you know approximately how many populations to expect

**DBSCAN:**
- **Epsilon**: Controls density sensitivity (neighborhood size)
- **MinPts**: Minimum points required to form a cluster core
- **Best for**: Populations with varying densities and shapes
- **When to use**: When populations have irregular shapes or unknown numbers

**FlowSOM:**
- **SOM grid X/Y dimensions**: Size of self-organizing map grid
- **Metaclusters**: Number of final population groups (second-level clustering)
- **Training iterations**: How many times the algorithm updates
- **Best for**: Flow cytometry-specific analysis with hierarchical population structure

**Phenograph:**
- **k (nearest neighbors)**: Number of neighbors for graph construction
- **Best for**: Identifying rare populations and complex population structures
- **When to use**: When you want to detect subtle population differences

### Step 5: Population Identification

**Automatic population naming** based on marker expression:

1. **Enable population identification** to automatically name clusters
2. **Expression thresholds**:
   - **High expression threshold**: Level considered "positive" for a marker (default: 0.5)
   - **Low expression threshold**: Level considered "negative" for a marker (default: -0.5)
3. **Confidence threshold**: Minimum confidence required for population assignment (default: 30%)

**How it works:**
- System analyzes mean marker expression for each cluster
- Compares to thresholds to determine positive/negative markers
- Generates population names like "CD4+CD8-" or "B cells"
- Assigns confidence scores based on separation from thresholds

### Step 6: Visualization and Results

**Plot options:**
- **Show cluster labels**: Display cluster numbers on plots
- **Show population labels**: Display identified population names
- **Color by**: Choose to color by cluster ID, population, or sample group
- **Point density visualization**: Show cell density within populations

**Cluster management:**
- **Merge clusters**: Combine similar clusters manually if needed
- **Edit population names**: Modify automatic population assignments
- **View cluster statistics**: See event counts and percentages per cluster/population

### Step 7: Comparative Analysis

**Group comparisons:**
- **Population frequencies**: Compare population percentages between experimental groups
- **Statistical testing**: Automatic statistical comparisons (t-tests, ANOVA)
- **Fold change analysis**: Calculate population changes between conditions
- **Visualization**: Generate comparison plots and summary tables

**Batch-wide statistics:**
- **Consistency metrics**: Measure how similar samples are within groups
- **Quality control metrics**: Identify outlier samples
- **Population correlation**: See which populations change together across samples

### Step 8: Export and Templates

**Export options:**
- **Processed sample data**: Download all samples with cluster assignments
- **Population statistics**: Export population counts and percentages for all samples
- **Batch summary**: Combined statistics across all samples and groups
- **Cluster definitions**: Save cluster centers and parameters
- **Visualization plots**: Export plots as PDF or PNG

**Template management:**
- **Save processing template**: Save all parameters for reuse on future experiments
- **Load template**: Apply saved parameter sets to new batches
- **Template library**: Organize templates by experiment type or research question

---

## Processed Data

This tab provides a range of visualizations for the processed data. The sidebar includes adjustable parameters that allow users to customize and generate the desired plot. Upon uploading a file in .fcs, .csv, or .xlsx format, the data can be explored using the selected dimensionality reduction method. By clicking on the drop down menu, dimensionality reduction methods such as tSNE, UMAP, PCA or MDS can be chosen. Based on the dimensionality reduction technique chosen, additional parameters can be set. For example, if tSNE is selected as the dimensionality reduction method, the perplexity parameter and number of clusters can be adjusted accordingly. The plot width and length can also be adjusted by dragging the pointer along the scale. 

### Side Panel Controls

**File Upload and Exploration:**
Upon uploading a file in **.fcs, .csv, or .xlsx format**, the data can be explored using the selected dimensionality reduction method.

**Dimensionality Reduction Selection:**
By clicking on the **dropdown menu**, dimensionality reduction methods can be chosen:
- **t-SNE**: Best for revealing local structure and rare populations
- **UMAP**: Balances local and global structure preservation
- **PCA**: Linear method for noise reduction and overview
- **MDS**: Classical multidimensional scaling for distance preservation

**Method-Specific Parameters:**
Based on the dimensionality reduction technique chosen, additional parameters can be set. For example, if **t-SNE is selected** as the dimensionality reduction method, the **perplexity parameter and number of clusters** can be adjusted accordingly.

**Plot Customization:**
- **Plot dimensions**: The plot width and length can be adjusted by **dragging the pointer along the scale**
- **Visual parameters**: Modify point size, colors, and other aesthetic elements
- **Real-time updates**: Parameters apply immediately to visualization

### Data Preview

The Data Preview tab displays your uploaded dataset with the parameters that were chosen and applied to the dataset. This allows you to:
- **Verify data integrity**: Ensure your data loaded correctly
- **Check transformations**: See the effects of applied preprocessing steps
- **Review parameters**: Confirm that chosen parameters are appropriate for your data
- **Quality assessment**: Identify any issues before proceeding with analysis

---

## Troubleshooting

### Compensation Issues

**Diagonal matrix values ≠ 1.0:**
- **Cause**: Poor single-stain control quality
- **Solution**: Check that controls have bright, positive populations

**Negative spillover values:**
- **Cause**: Incorrect file assignment or poor controls
- **Solution**: Verify file assignments and control quality

**Spillover levels >50%:**
- **Cause**: Spectral overlap too high for reliable compensation
- **Solution**: Consider different fluorophore combinations

**High negative events after compensation:**
- **Cause**: Over-compensation
- **Solution**: Reduce spillover values manually in matrix editor

### Gating Issues

**Slow performance:**
- **Solution**: Use Static mode for datasets >10,000 events

**Population counts not updating:**
- **Solution**: Click "Refresh display" to recalculate hierarchy

**Can't see populations clearly:**
- **Solution**: Try density hotspots or hexagon plots for better visualization

**Gates not saving:**
- **Solution**: Ensure you click "Save Gate" after drawing each gate

**Sub-gates appearing empty:**
- **Solution**: Check that parent population selection is correct

### File Format Issues

**Channels not detected:**
- **Cause**: Non-standard channel naming
- **Solution**: Ensure FCS files use standard naming conventions (FL1-A, FITC-A, etc.)

**Import failures:**
- **Cause**: Corrupted files or invalid format
- **Solution**: Verify FCS files contain actual flow cytometry data

### Performance Issues

**Slow processing:**
- **Solution**: Reduce number of events analyzed or use sampling
- **Solution**: Enable Barnes-Hut approximation for t-SNE

**Browser freezing:**
- **Solution**: Use smaller datasets or increase browser memory allocation
- **Solution**: Close other browser tabs and applications

---

## FAQ

### General Questions

**Q: What file formats does CytoVerse support?**
A: CytoVerse supports .fcs (Flow Cytometry Standard), .csv, .tsv, and .xlsx files. FCS files are recommended for best compatibility across all features.

**Q: What's the maximum file size I can upload?**
A: The current limit is 250MB per upload session. For larger datasets, consider using the batch analysis features or data sampling.

### Technical Questions

**Q: How does the automatic population identification work?**
A: The system analyzes mean marker expression for each cluster and compares values to user-defined thresholds. Populations are named based on positive/negative marker combinations with confidence scores.
However, we are currently working on a way to allow users to specify their own populations to allow for a wider coverage of markers.

**Q: Can I export my gating strategy for use in other software?**
A: Yes, you can export gate definitions as CSV files and population statistics for analysis in other platforms like FlowJo or FCS Express.

**Q: How do I choose between t-SNE and UMAP for dimensionality reduction?**
A: Use t-SNE for discovering local structure and rare populations. Use UMAP when you need to preserve both local and global relationships, or for faster processing of large datasets.

### Workflow Questions

**Q: Do I need to compensate my data before gating?**
A: Yes, compensation should always be performed before gating when using multi-color panels. This removes fluorophore spillover that could affect population identification.

**Q: Can I apply the same gating strategy to multiple samples?**
A: Yes, use the template system in Interactive Gating to save gating strategies and apply them to new samples. For automated processing, use the Batch Analysis module.

**Q: How do I know if my compensation is working correctly?**
A: Check the QC metrics: negative event percentage should be <5%, and you should see improved separation between positive and negative populations in before/after plots.

---
