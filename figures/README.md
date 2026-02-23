# WirelessAgent MCTS Optimization - Visualization Results

## Overview

This document describes the professional academic visualizations generated for the WirelessAgent Monte Carlo Tree Search (MCTS) optimization analysis (Rounds 1-19).

## Generated Figures

### Figure 1: Performance Overview (`performance_overview.png`)

A comprehensive 6-panel analysis of the optimization performance:

**Panel A - Performance Evolution**
- Main line chart showing validation score across optimization rounds
- Rolling average (n=3) to smooth trends
- Highlighted best performing round (Round 14: 0.8178)
- Threshold lines indicating optimization mode boundaries:
  - Conservative mode (≥0.65): Minor prompt tweaks only
  - Moderate mode (0.50-0.65): Single structural changes allowed

**Panel B - Score Distribution**
- Histogram of score frequencies across all rounds
- Color-coded by performance tier:
  - Green (≥0.80): High performance
  - Blue (0.65-0.80): Medium performance
  - Orange (<0.65): Lower performance
- Mean and median score indicators

**Panel C - Cumulative Performance Improvement**
- Tracks the cumulative best score achieved over rounds
- Shows how the best solution evolves
- Diamond markers indicate significant improvement rounds (Δ > 0.01)
- Filled area visualizes total accumulated improvement

**Panel D - Computational Cost per Round**
- Bar chart of total cost ($) per optimization round
- Red bars highlight high-cost rounds (top 25th percentile)
- Shows resource investment for each iteration

**Panel E - Cost-Performance Trade-off**
- Scatter plot of cost vs. score
- Color gradient represents round number (temporal progression)
- Star marker identifies best cost-efficiency round
- Reveals optimization efficiency trends

**Key Statistics:**
- Total rounds: 19
- Best score: 0.8178 (Round 14)
- Mean score: 0.7648 ± 0.0568
- Total improvement: +0.1934 (30.97%)
- Total cost: $4.95
- Best efficiency: 7.96 score/$ (Round 1)

---

### Figure 2: MCTS Tree Structure (`mcts_tree_structure.png`)

**Panel A - Exploration Tree (Hierarchical Layout)**
- Directed graph showing parent-child relationships in MCTS exploration
- Node properties:
  - **Color**: Performance level
    - Green: High score (≥0.80)
    - Blue: Medium score (0.65-0.80)
    - Orange: Low score (<0.65)
  - **Size**: Proportional to validation score
  - **Label**: Round number (e.g., "R14")
- Edge properties:
  - **Solid green (thick)**: Improvement (Δ > +0.01)
  - **Dashed red (medium)**: Degradation (Δ < -0.01)
  - **Dotted gray (thin)**: Neutral change (|Δ| ≤ 0.01)
- Visualizes exploration strategy and search paths

**Panel B - Exploration Outcome Distribution (Pie Chart)**
- Success: 11.8% (2 nodes) - Modifications that improved performance
- Neutral: 52.9% (9 nodes) - Modifications with minimal impact
- Failure: 35.3% (6 nodes) - Modifications that decreased performance

**Panel C - Score Change Distribution (Histogram)**
- Distribution of score deltas across all parent-child transitions
- Vertical line at Δ=0 separates improvements from degradations
- Shows exploration bias and search effectiveness

**Panel D - Tree Depth Distribution (Bar Chart)**
- Distribution of nodes across different tree depths
- Indicates search breadth vs. depth strategy
- Maximum depth: 5 levels

**Summary Statistics Table:**
- Total nodes explored: 18
- Total transitions: 17
- Average branching factor: 1.89 children per parent
- Success rate: 11.8%
- Average improvement (when successful): +0.0760
- Average degradation (when failing): -0.0352

---

### Figure 3: Comparative Analysis (`comparative_analysis.png`)

**Panel A - Score Trends with Moving Averages**
- Scatter plot of actual scores per round
- Overlaid moving averages (3-round and 5-round windows)
- Smooths noise to reveal underlying trends
- Helps identify momentum and convergence patterns

**Panel B - Round-to-Round Score Changes**
- Bar chart of score deltas between consecutive rounds
- Green bars: Improvements
- Red bars: Degradations
- Horizontal line at Δ=0 as reference
- Reveals optimization volatility and stability

**Panel C - Cost Accumulation vs. Performance**
- Dual y-axis plot showing:
  - Left axis (red): Cumulative cost over rounds
  - Right axis (green): Cumulative best score over rounds
- Shows diminishing returns and cost-effectiveness
- Identifies optimal stopping points

**Panel D - Performance Stability Analysis**
- Rolling 5-round mean score (solid blue line)
- Shaded region: ±1 standard deviation band
- Orange dashed line: Coefficient of variation (CV%)
- Lower CV% indicates more stable performance
- Assesses convergence and exploration-exploitation balance

---

## Key Findings

### Performance Metrics
1. **Significant Improvement**: 30.97% score increase from Round 1 (0.6244) to best Round 14 (0.8178)
2. **High Average Performance**: Mean score of 0.7648 demonstrates strong overall optimization
3. **Low Variability**: Std dev of 0.0568 shows consistent performance with controlled exploration

### MCTS Exploration
1. **Conservative Search**: Average branching factor of 1.89 indicates focused exploration
2. **Deep Search**: Maximum depth of 5 levels shows persistent refinement
3. **Balanced Outcomes**: 
   - 11.8% success rate is reasonable for optimization in high-score regime
   - 52.9% neutral outcomes reflect conservative mode constraints (score ≥0.65)
   - 35.3% failures provide learning signal for avoiding poor modifications

### Cost Efficiency
1. **Front-loaded Returns**: Round 1 achieved best cost-efficiency (7.96 score/$)
2. **Diminishing Returns**: Later rounds show higher costs for smaller improvements
3. **Total Investment**: $4.95 total cost for 19 rounds is computationally efficient

### Optimization Behavior
1. **Rapid Initial Improvement**: Rounds 1-2 show largest gains (+0.1842 in Round 2)
2. **Plateau at High Performance**: Rounds 7-19 fluctuate around 0.75-0.82
3. **Conservative Mode Effect**: Once score exceeded 0.65 (Round 4), structural changes were prohibited, limiting further exploration

---

## Recommendations

Based on these visualizations:

1. **Explore ToolAgent Integration**: Current workflow uses only Custom operators. Adding ToolAgent for calculation-heavy problems may break the 0.82 ceiling.

2. **Modify Conservative Threshold**: Consider allowing moderate structural changes even at score ≥0.65 to enable continued exploration of promising operators.

3. **Cost-Aware Stopping**: Given diminishing returns after Round 14, consider implementing early stopping criteria based on cost-performance ratio.

4. **Increase Exploration Budget**: Low success rate (11.8%) in high-score regime suggests more aggressive exploration strategies may be beneficial.

---

## Technical Details

**Software Stack:**
- Python 3.9+
- matplotlib (publication-quality plotting)
- seaborn (statistical visualization)
- networkx (graph/tree visualization)
- numpy (numerical analysis)

**Data Sources:**
- `workspace/WCHW/workflows/results.json` - Round-by-round performance metrics
- `workspace/WCHW/workflows/processed_experience.json` - MCTS tree structure

**Figure Specifications:**
- Resolution: 300 DPI (publication-ready)
- Format: PNG with white background
- Font: Times New Roman (academic standard)
- Color scheme: Professional accessible palette

**Reproducibility:**
```bash
python results_analysis.py
```

All figures are automatically saved to `./figures/` directory.

---

## Citation

If using these visualizations in academic work, please cite:

```
WirelessAgent: Monte Carlo Tree Search Optimization for Wireless Communication Problem Solving
Optimization Rounds: 1-19
Date: January 2026
```

---

**Generated by:** `results_analysis.py`  
**Date:** January 13, 2026  
**Version:** 1.0
