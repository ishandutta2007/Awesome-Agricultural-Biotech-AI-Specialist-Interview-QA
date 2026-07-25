# Topic 11: Troubleshooting & Case Studies

## Overview
Diagnosing model failures, field data quality issues, and structured problem-solving for common real-world agricultural AI/genomics scenarios.

---

### Q1: A genomic prediction model that performed well in cross-validation shows systematically inflated (overly optimistic) predictions for a specific subset of breeding lines once real field results come in. Walk through your troubleshooting approach.

**A:**
**Systematic troubleshooting framework:**
1. **Characterize the affected subset precisely — is there a common thread?** Determine whether the systematically over-predicted lines share a common characteristic — e.g., all from a specific recent cross/pedigree, all from a specific breeding sub-population, all sharing a specific parent, or all evaluated primarily in a specific subset of environments — this pattern-identification step often quickly narrows the plausible root cause hypotheses
2. **Check for training population relatedness/representation gaps:** A common root cause is that the affected lines are more genetically distant from the genomic prediction model's training population than typical (e.g., a novel cross introducing a previously underrepresented parental source) — genomic prediction accuracy is well-documented to degrade for genotypes poorly represented in or distantly related to the training population, and this is often the single most likely explanation warranting first investigation, connecting directly to Topic 02's discussion of training population design
3. **Check for a specific pedigree/relationship data error:** Verify that the genomic relationship matrix and underlying genotype data for the affected lines are actually correct — a data error (e.g., an incorrect pedigree record, a sample identity mix-up in genotyping) affecting a specific subset of lines can produce exactly this kind of systematic, subset-specific prediction failure, and this more mundane data-quality explanation should be ruled out before concluding there's a genuine model generalization limitation
4. **Assess whether a specific non-additive genetic effect (e.g., strong heterosis/dominance or epistasis, Topic 01) is more pronounced for this specific subset than the model's assumed genetic architecture captures:** If the affected lines share a specific novel parental combination pattern, and the genomic prediction model primarily captures additive genetic effects (as GBLUP does by default, Topic 02), a case where non-additive effects are unusually important for this specific parental combination could produce systematic over-prediction if the model isn't capturing a negative non-additive interaction specific to that combination
5. **Consider environmental/GxE explanations if the affected lines were disproportionately tested in specific environments:** As discussed in Topic 05, if the affected subset of lines happens to have been field-tested disproportionately in environments different from the genomic prediction model's training environments, a GxE-driven explanation should be investigated alongside the purely genetic explanations above

**Resolution approach:** Depending on the diagnosed root cause, resolution might involve expanding/diversifying the training population to better represent the affected genetic background, correcting identified data errors, incorporating explicit non-additive effect terms into the model, or incorporating envirotyping-based GxE modeling (Topic 05) — the specific fix should be clearly matched to the actual diagnosed root cause rather than applying a generic "add more data and retrain" response without understanding why the systematic bias occurred in the first place.

### Q2: Case study — A computer vision-based automated disease detection system, validated with strong accuracy on a research station's trial plots, performs substantially worse when deployed across a network of commercial grower fields for a pilot program. How do you approach root-causing this?

**A:**
**Systematic root-cause approach:**
1. **Characterize the actual nature of the performance drop precisely, not just its magnitude:** Determine whether the degraded performance manifests as increased false positives, increased false negatives, or both, and whether it's uniform across all pilot fields or concentrated in specific fields/conditions — this pattern provides important diagnostic direction (e.g., uniformly elevated false positives across all commercial fields suggests a different systematic explanation than performance that's fine in most fields but poor in a specific subset)
2. **Systematically compare research station and commercial field conditions across plausible confounding factors:** Research station trial plots often differ systematically from commercial production fields in ways that could affect a computer vision model's performance — different camera/imaging equipment (if growers are using different drones/cameras than the research station's standardized equipment), different crop management practices affecting canopy appearance (e.g., different planting density, different varieties than the training data's specific varieties), different disease pressure/prevalence patterns, or different image capture conditions (lighting, time-of-day consistency) — a thorough investigation systematically works through this full list of plausible domain-shift sources rather than anchoring prematurely on a single explanation
3. **Assess training data representativeness relative to actual commercial deployment diversity:** If the original model training data was collected primarily or exclusively at the research station (a common and understandable practice given data collection convenience/control), it may simply not represent the genuine diversity of conditions (varieties, management practices, camera equipment, geographic/soil conditions) present across a realistic commercial grower network — this is a classic and common domain-shift failure mode, directly connecting to similar generalization challenges discussed in Topic 04's plant-counting case study
4. **Investigate ground-truth/validation labeling consistency between the original research validation and the pilot program's outcome assessment:** If the pilot program's "ground truth" disease assessment (used to evaluate the deployed model's real-world accuracy) was conducted differently or less rigorously than the original research station validation's ground-truth process (e.g., different raters, less standardized disease rating protocols), some of the apparent performance drop could reflect ground-truth measurement inconsistency rather than a genuine model performance problem — this possibility should be investigated rather than automatically assuming the model itself is entirely at fault

**Resolution and broader lesson:** This scenario typically points toward the need for deliberately diverse, representative training data collection (spanning realistic deployment conditions, not just convenient research station conditions) before or alongside broader commercial deployment, and reinforces the general principle (echoed throughout this repository) that strong performance on a convenient/controlled validation dataset doesn't guarantee — and should not be assumed to guarantee — comparable performance in genuinely different real-world deployment conditions without explicit validation under those target conditions.

### Q3–Q14: (Representative additional topics)
- Diagnosing unexpected genotyping data quality issues (sample mix-ups, low call rates) affecting genomic prediction pipelines
- Troubleshooting envirotyping data pipeline failures or unexpected gaps in historical weather data coverage
- Root-causing discrepancies between drone-based and ground-truth manual phenotyping measurements
- Investigating unexpected genetic gain stagnation despite continued genomic-prediction-informed selection
- Debugging field trial data integration pipeline failures (mismatched plot IDs, design metadata loss)
- Troubleshooting a precision agriculture recommendation system producing agronomically implausible outputs for specific field conditions
- Investigating batch effects across different genotyping platforms/service providers in a combined historical dataset
- Root-causing unexpectedly poor gene-editing on-target efficiency relative to computational efficiency predictions
- Diagnosing why a multi-environment GxE model's predictions don't match experienced breeder expectations for specific known germplasm
- Handling situations where field research data itself appears internally inconsistent or of questionable reliability

---

## Summary
Rigorous troubleshooting of agricultural AI/genomics model failures requires systematically distinguishing data quality issues, training population/domain representativeness gaps, and genuine biological/model structural limitations — with particular attention to the domain-shift risks inherent in models validated under research-station or historical conditions but deployed across the genuine diversity of commercial field conditions and future growing seasons.
