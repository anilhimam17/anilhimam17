# Strategic Plan: January - March 2026
**Godugu Anil Himam**

---

## Executive Summary

**Mission:** Build a compelling research portfolio while securing PhD admission through parallel execution of high-impact projects.

**Core Strategy:** Execute 4 parallel tracks with clear prioritization:
1. **MatterCLIP** (Primary - Novel Research)
2. **F1 Data Analysis** (Networking & Visibility)
3. **PhD Applications** (10+ programs)
4. **Kaggle Biomass Competition** (Income + Portfolio)

**Success Metrics by End of March 2026:**
- ✅ ArXiv preprint submitted (MatterCLIP)
- ✅ 3-4 F1 analysis posts (500+ views each)
- ✅ 10+ PhD applications submitted
- ✅ Top-10 Kaggle placement (target: Top-3)
- ✅ 2+ live demos on HuggingFace

---

## Priority Hierarchy

```
Priority 1: MatterCLIP (60 hours) - Publication target
Priority 2: F1 Analysis (24 hours) - Networking catalyst
Priority 3: PhD Applications (30 hours) - Career security
Priority 4: Kaggle Competition (80 hours in Dec-Jan) - Immediate income
```

---

## Track 1: MatterCLIP - Detailed Roadmap

### Project Overview
**Title:** "MatterCLIP: Graph Neural Networks with Natural Language Supervision for Molecular Property Prediction"

**Core Hypothesis:** By combining a GNN for molecular structures with a text Transformer, we can learn a shared embedding space using CLIP-style contrastive learning for zero-shot property prediction.

**Novelty:** First application of CLIP paradigm to molecular graphs + natural language property descriptions.

---

### Week-by-Week Breakdown

#### **Weeks 1-2: Literature Review & Data Exploration**
**Goal:** Understand domain and identify tractable dataset

**Key Papers to Read (10 total):**
1. CLIP: "Learning Transferable Visual Models From Natural Language Supervision" (Radford et al.)
2. MoleculeNet: "MoleculeNet: A Benchmark for Molecular Machine Learning" (Wu et al.)
3. GCN: "Semi-Supervised Classification with Graph Convolutional Networks" (Kipf & Welling)
4. GAT: "Graph Attention Networks" (Veličković et al.)
5. GraphSAGE: "Inductive Representation Learning on Large Graphs" (Hamilton et al.)
6. ChemBERTa: "ChemBERTa: Large-Scale Self-Supervised Pretraining for Molecular Property Prediction"
7. Molecular Transformers (2-3 recent papers from 2023-2024)

**Dataset Exploration:**
- **Primary:** MoleculeNet Tox21 (8,014 molecules, toxicity labels)
- **Backup:** ESOL (solubility), FreeSolv (hydration free energy)
- **Stretch:** PubChem subset with text descriptions

**Define Minimum Viable Experiment:**
```
Task: Binary classification via text matching
Input: Molecular SMILES string → Graph representation
Text: "This molecule is toxic" vs "This molecule is non-toxic"
Metric: Top-1 accuracy on 3-way matching task
Baseline: >60% accuracy (random = 33%)
```

**Deliverables:**
- [ ] 2-page research plan document
- [ ] Dataset selection justification
- [ ] Preliminary data analysis notebook

---

#### **Weeks 3-4: Baseline Implementation**
**Goal:** Prove concept with working prototype

**Architecture Components:**

1. **Text Encoder:**
   - Use pretrained DistilBERT (lightweight, fast)
   - Project to 512-dim embedding space
   - Freeze weights initially, fine-tune later

2. **Graph Encoder (Build from Scratch):**
   - Implement GCN (50-100 lines PyTorch)
   - Input: Molecule SMILES → RDKit → Graph (nodes=atoms, edges=bonds)
   - Output: 512-dim graph embedding
   - 2-3 GCN layers with ReLU activation

3. **Contrastive Loss:**
   - Adapt your CLIP implementation
   - InfoNCE loss with temperature parameter
   - Batch size: 32-64 pairs

**Training Setup:**
```python
# Pseudo-code structure
for batch in dataloader:
    molecule_graphs, text_descriptions = batch
    
    # Encode
    graph_embeddings = gnn_encoder(molecule_graphs)  # [B, 512]
    text_embeddings = text_encoder(text_descriptions)  # [B, 512]
    
    # Normalize
    graph_embeddings = F.normalize(graph_embeddings, dim=-1)
    text_embeddings = F.normalize(text_embeddings, dim=-1)
    
    # Contrastive loss
    loss = contrastive_loss(graph_embeddings, text_embeddings)
```

**Experiment:**
- Train for 20-30 epochs
- Validation: Given molecule, rank 10 candidate descriptions
- Target: >60% Top-1 accuracy

**Deliverables:**
- [ ] Working codebase on GitHub
- [ ] Training logs and loss curves
- [ ] Validation accuracy >60%
- [ ] 5-10 qualitative examples (success/failure cases)

---

#### **Weeks 5-6: Scaling & Ablation Studies**
**Goal:** Understand what components drive performance

**Ablation Experiments:**

1. **GNN Architecture Comparison:**
   - GCN (baseline)
   - GAT (with attention)
   - GraphSAGE (with sampling)
   - Measure: Accuracy, training time, memory usage

2. **Text Encoder Variations:**
   - DistilBERT (baseline)
   - BERT-base
   - GPT-2 small
   - Your from-scratch Transformer

3. **Training Strategy:**
   - From-scratch training
   - Fine-tuning with frozen text encoder
   - Fine-tuning with LoRA on text encoder

4. **Data Augmentation:**
   - SMILES randomization (different valid representations)
   - Text paraphrasing (GPT-4 to generate varied descriptions)

**Key Analysis Questions:**
- Which molecules/properties are hardest to predict?
- Does CLIP-style training outperform supervised classification?
- How does performance scale with dataset size?

**Deliverables:**
- [ ] Ablation results table
- [ ] Error analysis document
- [ ] Qualitative failure case analysis
- [ ] Performance vs. computational cost trade-off plot

---

#### **Weeks 7-8: Paper Writing & Deployment**
**Goal:** Package research for publication and public demo

**Paper Structure (4 pages for ArXiv):**

1. **Introduction (0.5 pages)**
   - Problem: Molecular property prediction requires expensive labels
   - Solution: Language supervision enables zero-shot learning
   - Contribution: First CLIP-style approach for molecular graphs

2. **Related Work (0.5 pages)**
   - Traditional molecular property prediction
   - Graph neural networks for chemistry
   - Vision-language models (CLIP, ALIGN)

3. **Methods (1.5 pages)**
   - Architecture diagram (GNN + Text Encoder)
   - Contrastive learning objective
   - Dataset and preprocessing details

4. **Experiments (1 page)**
   - Baseline comparisons
   - Ablation studies
   - Qualitative results

5. **Discussion & Future Work (0.5 pages)**
   - Limitations (dataset size, property coverage)
   - Future directions (generative models, larger scale)

**HuggingFace Demo:**
```
Interface:
1. Input: Molecule SMILES string (text box)
2. Output: 
   - Top-5 property descriptions with similarity scores
   - Molecular structure visualization (RDKit)
   - Confidence bar chart
```

**Promotional Materials:**
- **Twitter Thread (8-10 tweets):**
  - Hook: "I taught AI to understand chemistry using language 🧪"
  - Problem statement
  - Solution overview
  - Key results
  - Demo link + paper link
  
- **LinkedIn Post:**
  - Professional angle: "Bridging NLP and Chemistry"
  - Tag connections in pharma/biotech/ML
  
- **Blog Post (Medium/Personal Site):**
  - Deep dive: "How I Built MatterCLIP in 8 Weeks"
  - Code walkthrough
  - Lessons learned

**Deliverables:**
- [ ] ArXiv preprint submitted
- [ ] HuggingFace Space deployed
- [ ] GitHub repository (clean, documented)
- [ ] Twitter thread published
- [ ] LinkedIn post + blog post published

---

### Risk Mitigation & Pivot Plans

**If full CLIP training fails:**
- Pivot to: "GNNs with Natural Language Supervision" (drop image-text analogy)
- Focus on: Improving molecular property prediction with auxiliary text signals

**If dataset curation is too hard:**
- Use existing molecular datasets
- Manually create simple text descriptions (50-100 templates)
- Focus on: Methodology novelty over data scale

**If results are mediocre:**
- Position as: "Exploratory study identifying challenges"
- Emphasize: Novel methodology + thorough ablations
- Target: ArXiv preprint + workshop paper (not full conference)

---

## Track 2: F1 Data Analysis

### Strategic Goal
**Get on the radar of well-paid F1 professionals through visible analytical work.**

**Target Audience:**
- Your LinkedIn connections in lead/development roles (F1 paddock)
- Broader data science community
- Potential PhD supervisors interested in applied ML

---

### Execution Framework

#### **Phase 1: Foundation (January - Weeks 1-4)**

**Project 1: "Tire Degradation Patterns Across 2024 Season"**

**Data Pipeline:**
```python
# Using FastF1 library
import fastf1
import pandas as pd
import plotly.express as px

# Extract data for all 2024 races
races = ['Bahrain', 'Saudi Arabia', 'Australia', ...]
tire_data = []

for race in races:
    session = fastf1.get_session(2024, race, 'R')
    laps = session.load_laps()
    tire_data.append(extract_tire_degradation(laps))

# Analysis
degradation_by_compound = analyze_degradation(tire_data)
```

**Analysis Questions:**
- Which tire compound degrades fastest per track type?
- How does degradation vary by temperature/humidity?
- Which teams manage tire wear best?

**Outputs:**
- Interactive Plotly dashboard
- Kaggle notebook
- LinkedIn post tagging 2-3 F1 connections

**Time Budget:** 6 hours

---

#### **Phase 2: Advanced (February - Weeks 5-8)**

**Project 2: "Predicting Race Finish from Qualifying Position"**

**Model:**
```python
# Features
features = [
    'qualifying_position',
    'grid_position', 
    'weather_conditions',
    'track_type',
    'tire_strategy',
    'historical_team_performance'
]

# Target
target = 'race_finish_position'

# Model: XGBoost or LightGBM
model = train_gradient_boosting_model(features, target)

# Validation
compare_predictions_vs_actual(model, test_races)
```

**Analysis:**
- What % of races follow "qualifying determines race" pattern?
- When do underdogs (P10+) break into Top 5?
- Feature importance: What matters most?

**Outputs:**
- Streamlit/Gradio web app
- Blog post: "Can You Predict F1 Race Results?"
- Share in F1 analytics communities (Reddit, Discord)

**Time Budget:** 8 hours

---

#### **Phase 3: AI Strategy Predictor (March - If Time Permits)**

**Project 3: "My AI vs. Red Bull Strategists"**

**Concept:**
Train ML model to predict optimal pit stop timing, then backtest against actual team decisions.

**Features:**
```python
state_features = [
    'current_lap',
    'tire_age',
    'track_position',
    'gap_to_car_ahead',
    'gap_to_car_behind',
    'track_temperature',
    'weather_probability',
    'safety_car_likelihood'
]

action = 'pit_now' or 'stay_out'
```

**Training Data:**
- All 2023 Red Bull races (they won championship)
- Extract state-action pairs from telemetry

**Evaluation:**
- Compare your AI's pit calls vs. actual Red Bull decisions
- Metric: "Agreement rate" + "Alternative strategy outcome analysis"

**Outputs:**
- Technical blog post
- "Would my AI have made different calls in Monaco 2023?" case study
- LinkedIn post highlighting strategic decision-making skills

**Time Budget:** 10 hours (optional, only if MatterCLIP ahead of schedule)

---

### Publishing Cadence

| Week | Project | Platform | Expected Reach |
|------|---------|----------|----------------|
| 2 | Tire Degradation | LinkedIn + Kaggle | 500+ views |
| 4 | Race Prediction Model | Medium + HF Space | 1,000+ views |
| 8 | AI Strategist (optional) | Twitter thread + Blog | 2,000+ views |

**Networking Strategy:**
- Tag 1-2 F1 connections per post (personalized comment)
- Share in r/formula1, F1 Discord, Kaggle community
- Use hashtags: #F1 #DataScience #MachineLearning #Analytics

---

## Track 3: PhD Applications

### Target Programs (10+ Applications)

#### **UK Programs (Prioritized)**

| University | Program | Deadline | Status |
|------------|---------|----------|--------|
| UoE + HWU | CDT D2AIR | Nov 14, 2025 | ✅ Applied |
| UoE | CDT ML Systems | Dec 11, 2025 | ❌ Rejected |
| **UoE** | **IPAB: Robotics & CV** | **Dec 18, 2025** | **DUE SOON** |
| Bristol | UKRI CDT AI for Healthcare | TBD | To apply |
| Imperial | CDT Safe & Trusted AI | TBD | To apply |
| Cambridge | ML & MI MPhil→PhD | Jan 15, 2026 | To apply |
| UCL | CDT AI Healthcare Systems | TBD | To apply |
| Manchester | CDT Robotics & AI Net Zero | TBD | To apply |
| UoG | Glasgow Interactive Systems | Jan 31, 2026 | To apply |
| Oxford | ESPRC CDT AIMS | Jan 28, 2026 | To apply |

#### **EU Programs (English-taught)**

| University | Program | Deadline | Contact Required |
|------------|---------|----------|------------------|
| Amsterdam | Hyperbolic Deep Learning CV | Dec 31, 2025 | Email professor |
| ETH Zurich | AI Center Direct PhD | Rolling | Direct contact |
| EPFL | EDIC Doctoral Program | Jan 15, 2026 | Email labs |
| TU Delft | 3ME/DCSC Robotics | Rolling | Direct contact |
| MPI-IS Tübingen | Robotics/AI positions | Rolling | Direct contact |

---

### Application Strategy

**Phase 1: Immediate (Dec 15-17)**
- **CRITICAL:** Apply to IPAB by Dec 15 (NOT Dec 18)
- Reason: Buffer for system issues, late references

**Phase 2: Early January (Jan 1-15)**
- Amsterdam, Cambridge, EPFL
- Template emails to 2-3 professors per program

**Phase 3: Late January (Jan 16-31)**
- Glasgow, Oxford, remaining programs
- Leverage any Kaggle wins in applications

---

### Cold Email Template

```
Subject: PhD Application - Morphology-Aware VLA Research

Dear Professor [Name],

I am Anil Himam, a recent BSc Computer Science graduate from Heriot-Watt 
University (2:1 Honors) applying to [Program Name]. I have been following 
your work on [specific paper/project], particularly [specific contribution].

My research interests align closely with your lab's focus. I recently:
- Implemented CLIP, ViT, and GPT from scratch (deployed AI photo search on HF)
- Achieved 99.8% F1 on real-time gesture recognition for HRI (Pepper robot)
- Developed hierarchical VLA research proposal addressing deployment constraints

I am particularly interested in [specific aspect of their research]. My 
background in [relevant skill] would enable me to contribute to [their project].

Would you have capacity to supervise a PhD student in 2025-26? I would welcome 
the opportunity to discuss potential alignment.

Research proposal and CV attached.

Best regards,
Anil Himam
```

---

## Track 4: Kaggle Biomass Competition

**Status:** Ongoing (ends late January 2026)

**Allocated Time:** 80 hours (Dec-Jan)

### Competition Strategy

**Phase 1: Baseline (Dec 18-25)**
- Load dataset, EDA, train simple CNN baseline
- Target: Public LB score >0.65

**Phase 2: Model Development (Dec 26-Jan 10)**
- Test 3-5 architectures: EfficientNet, ConvNeXt, Swin Transformer
- Multi-task learning: Predict all 5 targets jointly
- Incorporate metadata (NDVI, Height) through feature fusion

**Phase 3: Ensembling (Jan 11-20)**
- Train 5+ diverse models
- Weighted ensemble + TTA (rotate/flip)
- Test-time optimization

**Phase 4: Final Push (Jan 21-31)**
- Hyperparameter tuning
- Model stacking
- Submit best ensemble

**Target Placement:** Top 10 (stretch: Top 3)
**Prize Potential:** $5k-$50k

---

## Master Timeline: Jan-March 2026

| Week | MatterCLIP | F1 Analysis | PhD Apps | Kaggle | Hours |
|------|------------|-------------|----------|--------|-------|
| Dec 15-17 | - | - | IPAB application | Setup | 10 |
| 1 (Jan 1-7) | Lit review | - | Amsterdam email | Baseline complete | 25 |
| 2 (Jan 8-14) | Data exploration | Tire degradation post | Cambridge/EPFL email | Model dev | 30 |
| 3 (Jan 15-21) | Baseline model | - | 3 applications | Ensembling | 30 |
| 4 (Jan 22-28) | Baseline complete | - | 2 applications | Final push | 35 |
| 5 (Feb 1-7) | Ablations start | Race prediction post | - | Competition ends | 20 |
| 6 (Feb 8-14) | Ablations complete | - | 3 applications | Results analysis | 20 |
| 7 (Feb 15-21) | Paper writing | - | 2 applications | - | 15 |
| 8 (Feb 22-28) | Paper + demo | - | - | - | 15 |
| 9 (Mar 1-7) | ArXiv submission | - | - | - | 10 |
| 10 (Mar 8-14) | - | AI strategist (opt) | - | - | 5 |

**Total Estimated Hours:** 215 hours over 10 weeks = ~21 hours/week

---

## Success Metrics & Checkpoints

### Monthly Reviews

**End of January 2026:**
- ✅ Kaggle competition submitted (aiming Top-10)
- ✅ MatterCLIP baseline working (>60% accuracy)
- ✅ 1 F1 analysis post published (500+ views)
- ✅ 5+ PhD applications submitted
- ✅ IPAB application decision received

**End of February 2026:**
- ✅ MatterCLIP ablations complete
- ✅ 2 F1 analysis posts published (1,000+ views each)
- ✅ 8+ PhD applications submitted
- ✅ Kaggle results known (prize money?)

**End of March 2026:**
- ✅ MatterCLIP ArXiv preprint submitted
- ✅ HuggingFace demo deployed
- ✅ 3-4 F1 posts published (2,000+ total views)
- ✅ 10+ PhD applications submitted
- ✅ Interview invitations from 2-3 programs (goal)

---

## Risk Management

### Scenario Planning

**Scenario 1: Kaggle doesn't place Top-10**
- Still valuable portfolio piece
- Write blog post: "What I learned from Kaggle Biomass"
- Leverage technical skills demonstrated

**Scenario 2: MatterCLIP results are mediocre**
- Pivot to methodology paper
- Emphasize thorough ablations
- Target workshop instead of main conference

**Scenario 3: No PhD offers by March**
- Continue with MatterCLIP (stronger application for next cycle)
- Start freelancing (Upwork/Toptal) for income
- Apply to industry ML research positions

**Scenario 4: Time management breakdown**
- Drop F1 analysis (lowest priority)
- Focus MatterCLIP + PhD apps only
- Extend timeline to April if needed

---

## Key Resources & Tools

### Development Stack
- **Python:** 3.10+
- **ML Frameworks:** PyTorch, PyTorch Geometric (GNNs)
- **Data:** RDKit (chemistry), FastF1 (F1 telemetry)
- **Viz:** Plotly, Matplotlib, Seaborn
- **Deployment:** HuggingFace Spaces, Streamlit
- **Version Control:** Git + GitHub

### Research Resources
- **Papers:** ArXiv, Google Scholar, Connected Papers
- **Datasets:** MoleculeNet, PubChem, Kaggle
- **Community:** Reddit (r/MachineLearning), Twitter/X, Kaggle forums

### Time Management
- **Pomodoro:** 25-min focused sprints
- **Weekly Review:** Sunday evenings
- **Daily Standup:** Log progress in notebook
- **Accountability:** Share weekly updates on LinkedIn

---

## Closing Notes

**Core Philosophy:**
"Build in public, ship consistently, learn relentlessly."

**Mindset:**
- Each project compounds: F1 analysis → data skills → helps MatterCLIP
- Each rejection is data: Learn from CDT-ML Systems feedback
- Each demo is a resume: Live projects > bullet points

**Support System:**
- Mentor check-ins (bi-weekly)
- Peer accountability (PhD applicant Discord?)
- Family support (communicate timeline expectations)

**Remember:**
You're not just applying to PhDs. You're building the profile that makes rejecting you impossible.

---

**Last Updated:** December 17, 2025  
**Next Review:** January 7, 2026  
**Version:** 1.0
