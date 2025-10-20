---
title: programming/environmentdev
tags:
categories:
date: 2025-08-20
lastMod: 2025-08-20
--- 
Asked Claude how one could get set up to do genomics, bioinf, data science, and ML on a laptop with Python and R and shell utilization.  this note covers that onboarding process.
  

  
"essential resources:
  
  + [Bioconductor](https://bioconductor.org/)
  
  + [Galaxy Project](https://galaxyproject.org/)
  
  + [NCBI Datasets](https://www.ncbi.nlm.nih.gov/datasets/)
  
  + [Ensembl](https://ensembl.org/)
  
  + [10X Genomics Support](https://support.10xgenomics.com/)
  

  
## 1. Installing HomeBrew
  
  + easy, of course, but learned something important:
  
```sh
Run brew help to get started
Further documentation:
  https://docs.brew.sh
(base) dantericci@Dantes-MacBook-Pro ~ % brew help 
zsh: command not found: brew
```
  
  + even though i had installed `homebrew`, i had to add it to my `PATH` in order to be able to call it!
  
```sh
Run these commands in your terminal to add Homebrew to your PATH:
  echo >> /Users/dantericci/.zprofile
  echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/dantericci/.zprofile
  eval "$(/opt/homebrew/bin/brew shellenv)"
Run brew help to get started
Further documentation:
  https://docs.brew.sh

(base) dantericci@Dantes-MacBook-Pro ~ % brew help 
zsh: command not found: brew
(base) dantericci@Dantes-MacBook-Pro ~ %   echo >> /Users/dantericci/.zprofile
(base) dantericci@Dantes-MacBook-Pro ~ % echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/dantericci/.zprofile
(base) dantericci@Dantes-MacBook-Pro ~ % eval "$(/opt/homebrew/bin/brew shellenv)"
(base) dantericci@Dantes-MacBook-Pro ~ % brew help
Example usage:
brew search TEXT|/REGEX/
brew info [FORMULA|CASK...]
brew install FORMULA|CASK...
brew update
brew upgrade [FORMULA|CASK...]
brew uninstall FORMULA|CASK...
brew list [FORMULA|CASK...]
```
  

  

  

  
# Complete macOS Setup Guide for Bioinformatics & Data Science
  
  + ## Overview
  
    + This guide will set up your MacBook Pro for bioinformatics, genomics, and data science work with Python, R, and shell scripting, emphasizing ease of use and integration.
  
  + ## Section 1: Core Development Environment Setup
  
  + ### 1.1 Command Line Tools & Package Managers

**Install Homebrew (Essential macOS package manager)**

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

**Install essential command line tools:**

```
# Core development tools
brew install git
brew install wget
brew install curl
brew install tree
brew install htop
brew install jq  # JSON processor
brew install pandoc  # Document converter
```

**Install modern shell tools (optional but recommended):**

```
brew install zsh-syntax-highlighting
brew install zsh-autosuggestions
brew install fzf  # Fuzzy finder
brew install ripgrep  # Fast grep alternative
```
  
  + ### 1.2 Terminal Enhancement

**Install iTerm2 (Better terminal than default):**

```
brew install --cask iterm2
```

**Configure Oh My Zsh for better shell experience:**

```
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
  
  + ## Section 2: Python Environment Setup
  
  + ### 2.1 Python Version Management

**Install pyenv (Better than Anaconda for version management):**

```
brew install pyenv
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
source ~/.zshrc
```

**Install Python versions:**

```
pyenv install 3.11.9  # Latest stable
pyenv install 3.10.14  # For compatibility
pyenv global 3.11.9
```
  
  + ### 2.2 Virtual Environment Management

**Install pipenv (Easier than conda environments):**

```
pip install pipenv
```

**Or use poetry for more advanced dependency management:**

```
curl -sSL https://install.python-poetry.org | python3 -
```
  
  + ### 2.3 Essential Python Packages for Bioinformatics

**Create a base bioinformatics environment:**

```
mkdir ~/bioinformatics-env
cd ~/bioinformatics-env
pipenv install --python 3.11

# Core data science stack
pipenv install numpy pandas matplotlib seaborn plotly
pipenv install scipy scikit-learn
pipenv install jupyter jupyterlab
pipenv install ipywidgets

# Bioinformatics specific
pipenv install biopython
pipenv install pysam  # SAM/BAM file handling
pipenv install pyvcf3  # VCF file handling
pipenv install scanpy  # Single-cell analysis
pipenv install anndata  # Annotated data matrices
pipenv install pybedtools  # BED file operations

# Machine learning for bio
pipenv install tensorflow
pipenv install torch torchvision  # PyTorch
pipenv install transformers  # Hugging Face
pipenv install optuna  # Hyperparameter optimization

# Workflow management
pipenv install snakemake
pipenv install nextflow  # Alternative workflow manager

# Utilities
pipenv install click  # CLI creation
pipenv install tqdm  # Progress bars
pipenv install requests
pipenv install openpyxl  # Excel files
```
  
  + ## Section 3: R Environment Setup
  
  + ### 3.1 R Installation and Management

**Install R and RStudio:**

```
brew install --cask r
brew install --cask rstudio
```

**Install renv for R package management:**

```
install.packages("renv")
```
  
  + ### 3.2 Essential R Packages for Bioinformatics

**Install Bioconductor and core packages:**

```
# Install BiocManager
install.packages("BiocManager")

# Core Bioconductor packages
BiocManager::install(c(
  "Biobase", "BiocGenerics", "Biostrings", "GenomicRanges",
  "GenomicFeatures", "IRanges", "S4Vectors", "SummarizedExperiment",
  "MultiAssayExperiment", "SingleCellExperiment"
))

# Genomics analysis
BiocManager::install(c(
  "DESeq2", "edgeR", "limma",  # Differential expression
  "ChIPseeker", "DiffBind",    # ChIP-seq analysis
  "Seurat", "scater", "scran", # Single-cell analysis
  "GenomicAlignments", "Rsamtools", "VariantAnnotation"
))

# Data manipulation and visualization
install.packages(c(
  "tidyverse", "dplyr", "ggplot2", "plotly",
  "data.table", "readxl", "openxlsx",
  "knitr", "rmarkdown", "bookdown",
  "reticulate"  # Python integration
))

# Machine learning
install.packages(c(
  "caret", "randomForest", "xgboost",
  "glmnet", "e1071"
))
```
  
  + ## Section 4: Integrated Development Environment
  
  + ### 4.1 Visual Studio Code Setup

**Install VS Code (Recommended over separate IDEs):**

```
brew install --cask visual-studio-code
```

**Essential VS Code Extensions:**
  
  + Python (Microsoft)
  
  + R (REditorSupport)
  
  + Jupyter (Microsoft)
  
  + GitLens
  
  + Code Spell Checker
  
  + Markdown All in One
  
  + Remote - SSH
  
  + Docker
  
  + YAML
  
  + ### 4.2 Alternative: JupyterLab as Primary IDE

**Enhanced JupyterLab setup:**

```
pipenv install jupyterlab
pipenv install jupyterlab-git
pipenv install nbconvert
pipenv install jupytext  # Sync notebooks with .py files

# Extensions
pipenv install ipywidgets
pipenv install plotly
pipenv install bokeh
```
  
  + ## Section 5: File Organization System
  
  + ### 5.1 Directory Structure

**Create standardized project structure:**

```
mkdir -p ~/Projects/{bioinformatics,data-science,tools}
mkdir -p ~/Data/{raw,processed,external}
mkdir -p ~/Scripts/{python,r,shell}
mkdir -p ~/Notebooks/{templates,analyses}
mkdir -p ~/References/{genomes,annotations,databases}
```

**Project template structure:**

```
project_name/
├── data/
│   ├── raw/
│   ├── processed/
│   └── external/
├── notebooks/
├── scripts/
│   ├── preprocessing/
│   ├── analysis/
│   └── utils/
├── results/
│   ├── figures/
│   ├── tables/
│   └── reports/
├── docs/
├── environment/
├── README.md
├── requirements.txt (or Pipfile)
└── .gitignore
```
  
  + ### 5.2 Project Template Creation

**Create a project template script:**

```
# Save as ~/Scripts/shell/new_project.sh
#!/bin/bash
project_name=$1
mkdir -p ~/Projects/$project_name/{data/{raw,processed,external},notebooks,scripts/{preprocessing,analysis,utils},results/{figures,tables,reports},docs,environment}
cd ~/Projects/$project_name
git init
echo "# $project_name" > README.md
curl -o .gitignore https://raw.githubusercontent.com/github/gitignore/main/Python.gitignore
```
  
  + ## Section 6: Bioinformatics-Specific Tools
  
  + ### 6.1 Command Line Bioinformatics Tools

**Install via Homebrew:**

```
# Sequence analysis
brew install samtools
brew install bcftools
brew install bedtools
brew install seqtk
brew install minimap2
brew install bwa

# Quality control
brew install fastqc
brew install multiqc

# Other utilities
brew install parallel  # Parallel processing
brew install gnu-sed  # Better sed
brew install coreutils  # GNU core utilities
```
  
  + ### 6.2 Container Solutions

**Install Docker for reproducible environments:**

```
brew install --cask docker
```

**Install Singularity (alternative to Docker):**

```
brew install --cask singularity
```
  
  + ## Section 7: Notebook Templates and Workflows
  
  + ### 7.1 Jupyter Notebook Templates

**Create analysis templates in ~/Notebooks/templates/:**
  
  + **exploratory_analysis_template.ipynb**
  
  + **rna_seq_analysis_template.ipynb**
  
  + **single_cell_analysis_template.ipynb**
  
  + **genomics_quality_control_template.ipynb**
  
  + ### 7.2 R Markdown Templates

**Create R Markdown templates:**

```
# Install additional packages for reporting
install.packages(c("flexdashboard", "shiny", "DT", "crosstalk"))
```
  
  + ## Section 8: Git and GitHub Integration
  
  + ### 8.1 Git Configuration

**Configure Git:**

```
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --global init.defaultBranch main
git config --global core.editor "code --wait"  # Use VS Code as editor
```
  
  + ### 8.2 GitHub CLI

**Install GitHub CLI:**

```
brew install gh
gh auth login
```
  
  + ### 8.3 Git Workflow Templates

**Create standard .gitignore for bioinformatics projects:**

```
# Data files
*.fastq
*.fq
*.bam
*.sam
*.vcf
*.bed
*.gtf
*.gff
data/raw/
data/external/

# Results
results/
*.pdf
*.png
*.jpg

# Python
__pycache__/
*.pyc
.env
.venv/

# R
.Rproj.user/
.Rhistory
.RData
.Ruserdata
packrat/lib*/

# Jupyter
.ipynb_checkpoints/

# macOS
.DS_Store
```
  
  + ## Section 9: AI Tools Integration
  
  + ### 9.1 Claude Code Setup (Already completed!)

Your Claude Code is ready to use for:
  
  + Script development and debugging
  
  + Package creation
  
  + Code optimization
  
  + Documentation generation
  
  + ### 9.2 Other AI Tools

**GitHub Copilot (for VS Code):**
  
  + Install Copilot extension in VS Code
  
  + Provides code completion and suggestions

**Cursor AI (Alternative IDE with built-in AI):**

```
brew install --cask cursor
```
  
  + ## Section 10: Workflow Management
  
  + ### 10.1 Snakemake Setup

**Create Snakemake workflow template:**

```
# Save as ~/Notebooks/templates/Snakefile_template
rule all:
  input:
      "results/final_report.html"

rule quality_control:
  input:
      "data/raw/{sample}.fastq"
  output:
      "results/qc/{sample}_fastqc.html"
  shell:
      "fastqc {input} -o results/qc/"

rule process_data:
  input:
      "results/qc/{sample}_fastqc.html"
  output:
      "results/processed/{sample}_processed.txt"
  script:
      "scripts/process_sample.py"
```
  
  + ### 10.2 Workflow Validation

**Testing framework setup:**

```
pipenv install pytest
pipenv install pytest-cov  # Coverage reporting
```
  
  + ## Section 11: Data Management
  
  + ### 11.1 Cloud Storage Integration

**Install cloud storage tools:**

```
brew install --cask google-drive
brew install rclone  # Multi-cloud storage tool
```
  
  + ### 11.2 Large File Management

**Install Git LFS for large files:**

```
brew install git-lfs
git lfs install
```
  
  + ## Section 12: Final Setup and Validation
  
  + ### 12.1 Environment Testing

**Create test script to validate setup:**

```
# Save as ~/Scripts/python/test_setup.py
import sys
print(f"Python version: {sys.version}")

# Test core packages
packages = [
  'numpy', 'pandas', 'matplotlib', 'seaborn',
  'scipy', 'scikit-learn', 'biopython', 'pysam'
]

for package in packages:
  try:
      __import__(package)
      print(f"✅ {package} imported successfully")
  except ImportError:
      print(f"❌ {package} failed to import")
```
  
  + ### 12.2 Resource Links and Documentation

**Bookmark these essential resources:**
  
  + [Bioconductor](https://bioconductor.org/)
  
  + [Galaxy Project](https://galaxyproject.org/)
  
  + [NCBI Datasets](https://www.ncbi.nlm.nih.gov/datasets/)
  
  + [Ensembl](https://ensembl.org/)
  
  + [10X Genomics Support](https://support.10xgenomics.com/)
  
  + ## Quick Start Checklist

After completing the setup:
  
  + ✅ Test Python environment: `python --version`
  
  + ✅ Test R environment: Open RStudio
  
  + ✅ Test Jupyter: `jupyter lab`
  
  + ✅ Test Git: `git --version`
  
  + ✅ Test Claude Code: `claude-code --help`
  
  + ✅ Create first project using template
  
  + ✅ Clone a test repository from GitHub
  
  + ✅ Run test analysis notebook
  
  + ## Maintenance

**Weekly tasks:**
  
  + Update packages: `brew update && brew upgrade`
  
  + Update Python packages: `pipenv update` (in each project)
  
  + Update R packages: `update.packages()`

**Monthly tasks:**
  
  + Review and clean unused virtual environments
  
  + Archive completed projects
  
  + Update bioinformatics tools and databases
 