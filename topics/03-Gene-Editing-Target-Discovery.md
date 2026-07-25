# Topic 03: Gene Editing Target Discovery

## Overview
CRISPR guide RNA design, off-target prediction, and computational approaches to trait engineering target discovery for agricultural gene editing applications.

---

### Q1: What computational considerations are involved in CRISPR guide RNA (gRNA) design for a plant gene editing application, and how do these differ from typical mammalian/therapeutic CRISPR design considerations?

**A:**
**Shared core considerations (applicable across CRISPR applications generally):**
1. **On-target efficiency prediction:** Using established sequence-feature-based or ML models (trained largely on mammalian cell data, an important caveat below) predicting gRNA cutting efficiency based on sequence features (GC content, position-specific nucleotide preferences, secondary structure)
2. **Off-target prediction:** Genome-wide search for sequences similar to the intended gRNA target (allowing for the mismatch tolerance characteristic of the specific Cas enzyme being used) that could be inadvertently edited, typically scored by a combination of sequence similarity and position-specific mismatch tolerance models

**Plant-specific considerations requiring adaptation:**
1. **Polyploidy and homoeolog targeting decisions (connecting to Topic 01):** For polyploid crops, a critical design decision is whether to target all homoeologous gene copies simultaneously (requiring a gRNA sequence conserved across all sub-genome copies) or selectively target a single homoeolog — this is a fundamentally different design consideration than typical diploid mammalian CRISPR design, requiring explicit homoeolog-aware sequence analysis and deliberate design strategy matched to the specific trait engineering goal (e.g., a recessive loss-of-function trait may require editing all homoeologous copies to see a phenotype, given genetic redundancy)
2. **Off-target prediction models trained predominantly on mammalian/human genomic and chromatin context may not transfer well to plant genomes:** Many published off-target prediction models were developed and validated using human/mammalian cell line data, where chromatin accessibility, genome organization, and repeat structure differ substantially from plant genomes (particularly given plant genomes' typically higher repeat content, Topic 01) — the AI specialist should be appropriately cautious about applying such models' predictions directly to plant genome contexts without species-specific validation, and should be aware of and prioritize plant-genome-specific off-target prediction tools/validation data where available
3. **Delivery method constraints shape practically achievable edits differently than in mammalian systems:** Plant transformation methods (e.g., Agrobacterium-mediated transformation, biolistic delivery) and the subsequent tissue culture/regeneration process impose their own constraints on editing strategy (e.g., timing of edits relative to the regeneration process, chimerism considerations in the regenerated plant) that don't have a direct analogue in typical mammalian cell-culture-based CRISPR applications, and computational target design should be considered alongside these practical delivery/regeneration constraints, not in isolation
4. **Regulatory categorization implications of the specific edit type inform target design strategy (connecting to Topic 09):** Given the regulatory distinctions between different classes of genetic modification (e.g., small indels/SDN-1 edits vs. larger insertions, discussed further in Topic 09), the specific type of edit being designed (not just its biological effect) has direct regulatory strategy implications that should inform target/edit design decisions from the start, not be considered only after a specific edit is already technically finalized

### Q2: Describe a computational approach to prioritizing candidate gene editing targets for a specific agronomic trait (e.g., improving drought tolerance), starting from limited functional genomics evidence.

**A:**
**Prioritization framework:**
1. **Aggregate multi-source evidence rather than relying on a single evidence type:** Combine QTL mapping results (Topic 01) identifying genomic regions associated with the trait, comparative genomics evidence (orthologous genes with characterized function in model species or related crops), transcriptomic evidence (genes showing differential expression under the relevant stress condition, e.g., drought), and any available prior functional characterization (e.g., published gene knockout/overexpression phenotype data) — no single evidence type is typically sufficient alone, and a well-designed computational prioritization pipeline should systematically integrate multiple evidence streams with appropriate weighting reflecting each evidence type's typical reliability
2. **Assess candidate genes' likely mechanism of action and predicted edit outcome, not just association strength:** A gene showing strong statistical QTL association isn't automatically a good editing target — the AI specialist should assess (often in close collaboration with plant biology/trait discovery scientists, Topic 10) whether the likely biological mechanism suggests a tractable editing strategy (e.g., is the desired outcome more consistent with a loss-of-function edit disrupting a negative regulator, versus requiring a more complex gain-of-function or precise regulatory-sequence modification that may be substantially harder to achieve reliably with current editing technology)
3. **Explicitly weigh predicted trait improvement against pleiotropy/trade-off risk:** Genes involved in stress response pathways are frequently pleiotropic (affecting multiple traits), and a computational prioritization approach should incorporate available evidence about potential negative trade-offs (e.g., a gene edit improving drought tolerance that's known or predicted, based on pathway/network evidence, to also reduce yield potential under well-watered conditions) — presenting only the primary trait benefit without surfacing plausible trade-off risks provides an incomplete, potentially misleading prioritization to breeding/trait development decision-makers
4. **Rank and stage candidates for experimental validation given realistic testing throughput constraints:** Given that generating and phenotyping actual gene-edited plant lines is a resource- and time-intensive process (often requiring a full plant generation cycle or more), the computational prioritization output should produce a realistically-sized, well-justified ranked candidate list matched to actual experimental validation capacity, with clear documentation of the evidence and reasoning supporting each candidate's priority ranking — this transparency is important both for effective trait discovery team collaboration (Topic 10) and for maintaining an auditable record of why specific candidates were prioritized, valuable if early candidates don't pan out and the reasoning needs to be revisited

### Q3–Q15: (Representative additional topics)
- Base editing and prime editing computational design considerations for precision agricultural trait engineering
- Multiplexed/multi-gene editing design strategy and combinatorial target prioritization
- Machine learning approaches to predicting edit outcome phenotypes prior to experimental validation
- Comparative genomics and synteny analysis for translating gene function knowledge across crop species
- Natural variation mining (identifying naturally-occurring beneficial alleles) as a complementary strategy to de novo gene editing
- Regulatory sequence (promoter/enhancer) editing target design for precise expression-level trait modulation
- CRISPR screening approaches (e.g., pooled guide RNA library screens) adapted for plant systems
- Off-target validation experimental design (whole-genome sequencing-based off-target detection) and its computational analysis
- Gene network/pathway modeling approaches informing target discovery beyond single-gene candidate approaches
- Managing intellectual property/freedom-to-operate considerations in computational target discovery strategy

---

## Summary
Gene editing target discovery for agricultural biotech requires adapting CRISPR design methodology for plant-specific genomic complexity (polyploidy, genome structure) and integrating multi-source functional genomics evidence into a rigorously-justified, trade-off-aware candidate prioritization process suited to the realistic experimental validation throughput of plant transformation/regeneration workflows.
