# Research Hypotheses & Assumptions

## Core Hypothesis
**H1: Compressed Hand Evaluation** - A subset of k \<\< 26 features from the RPBridge evaluator can achieve \>95% accuracy of the full 26-step evaluation through optimal feature selection and simple arithmetic combinations.

**Assumption being challenged**: That all 26 steps in RPBridge are necessary for accurate hand evaluation.

**H2: Data-Driven Superior Performance** - A machine learning model trained on existing bridge datasets can outperform rule-based evaluators (including RPBridge) on real-world hand evaluation accuracy.

**Assumption being challenged**: That hand-crafted rules are optimal for bridge hand evaluation.

# Experiment Ideas

## Core Experiments

### 1. **Feature Selection for RPBridge Compression**
   * **Objective**: Prove that k ≤ 8 features can achieve ≥95% correlation with full RPBridge scores
   * **Method**: 
     - Generate 10,000 random 13-card bridge hands
     - Compute all 26 RPBridge features f₁...f₂₆ for each hand
     - Use exhaustive search for k ≤ 6, greedy forward selection for k ≤ 8
     - Test linear combinations, polynomial features (degree ≤ 2), and simple decision trees
   * **Success Criteria**: Pearson correlation r ≥ 0.95 with original RPBridge scores
   * **Validity Threats**: 
     - Random hands may not represent real game distributions
     - Mitigation: Compare with hands from actual tournaments
   * **Timeline**: 2-3 days for implementation and evaluation

### 2. **ML Model vs Rule-Based Evaluation**
   * **Objective**: Demonstrate ML models achieve >90% accuracy on expert-labeled hand strength
   * **Method**:
     - Collect expert bridge player evaluations of hand strength (1-10 scale)
     - Train models: Random Forest, Gradient Boosting, Neural Network
     - Features: High-level card statistics (HCP, distribution, controls, etc.)
     - Compare against RPBridge, standard point counting, and Milton Work
   * **Success Criteria**: Classification accuracy >90% on expert labels, >5% improvement over rule-based methods
   * **Resources**: Need expert bridge player annotations (n≥1000 hands)
   * **Timeline**: 1-2 weeks including data collection

### 3. **Contextual Hand Evaluation**
   * **Objective**: Show that auction context significantly improves hand evaluation accuracy
   * **Method**:
     - Use tournament data with bidding sequences and final contracts
     - Compare hand evaluation with/without auction information
     - Measure correlation with actual contract success
   * **Success Criteria**: >15% improvement in predicting contract outcomes
   * **Data Requirements**: Tournament databases with complete auction + play records
   * **Timeline**: 1 week analysis

## Ablation Studies

### Feature Category Analysis
* **Remove shape features**: Expected 10-15% performance drop (distribution matters significantly)
* **Remove honor concentration**: Expected 5-8% drop (tenaces and honor combinations important)
* **Remove suit quality**: Expected 8-12% drop (suit playability crucial)

### Model Architecture Ablations
* **Simple linear vs polynomial**: Expect polynomial to improve by 3-5%
* **Individual features vs interaction terms**: Interactions likely improve 5-10%
* **Depth of decision trees**: Expect optimal depth around 8-12 levels

## Baselines & Benchmarks

### Traditional Methods
* **Milton Work Point Count**: ~70% correlation with expert evaluations
* **Modern Losing Trick Count**: ~75% correlation expected
* **Bergen Hand Evaluator**: ~80% correlation expected
* **Full RPBridge (26 steps)**: Target baseline to match/exceed

### State-of-the-Art
* **GIB hand evaluator**: Commercial standard, expect ~85% accuracy
* **Bridge Baron evaluation**: Another commercial baseline

## Experimental Controls & Validation

### Cross-Validation Strategy
- Stratified 5-fold CV by hand strength quartiles
- Separate test set of tournament hands (never used in training)
- Time-based split for tournament data (train on older, test on newer)

### Statistical Significance
- Bootstrap confidence intervals (n=1000 samples)
- Paired t-tests for method comparisons
- Bonferroni correction for multiple comparisons

## Priority & Risk Assessment

### Must Have (Core Validation)
1. **RPBridge feature selection** - Directly tests main hypothesis, low technical risk
2. **Basic ML vs rules comparison** - Essential for establishing ML viability

### High Impact, Higher Risk  
1. **Contextual evaluation with auction data** - High impact if successful, but requires complex tournament data parsing

### Nice to Have (Robustness)
1. **Cross-game generalization** - Test on other trick-taking games
2. **Online learning evaluation** - Adaptive evaluation during play

## Success Metrics & Thresholds

### Primary Success Criteria
- **Compression**: r ≥ 0.95 correlation with k ≤ 8 features
- **ML Performance**: >90% accuracy on expert labels
- **Practical Impact**: System usable by human players (≤5 steps)

### Secondary Metrics
- **Computational efficiency**: <10ms evaluation per hand
- **Interpretability**: Features human-understandable
- **Robustness**: Performance stable across different deal types

## Resource Requirements

### Computational
- 10K-100K hand evaluations: Standard laptop sufficient
- ML training: GPU recommended but not required
- Statistical analysis: R/Python scientific stack

### Data
- Random deal generation: Programmatic (unlimited)  
- Expert annotations: 1000+ hands needed, significant effort
- Tournament data: Existing databases available (BBO, tournaments)

### Timeline
- **Phase 1** (RPBridge compression): 1 week
- **Phase 2** (ML baseline): 2 weeks  
- **Phase 3** (Contextual evaluation): 2 weeks
- **Phase 4** (Analysis & write-up): 1 week

**Total estimated effort: 6-8 weeks**