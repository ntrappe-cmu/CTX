# Containerization Usability and Scientific Reproducibility: A Tale of Two Research Cultures

The past five years reveal a stark divergence in how bioinformatics and systems research communities approach computational reproducibility. While bioinformatics has spawned a **mature ecosystem of abstraction tools** making containerization accessible to non-experts, systems research remains mired in infrastructure challenges where even expert researchers struggle with artifact evaluation. Most critically, **gap-identification papers currently hold greater research value** than solution papers, as they articulate unmet needs with precision while existing solutions largely serve narrow use cases without addressing fundamental usability barriers.

## Domain contrast: Divergent maturity and user expectations
Bioinformatics research has embraced containerization through sophisticated wrapper systems that completely hide Docker complexity. Arcadia ResearchPubMed The 2025 Nextflow/nf-core ecosystem exemplifies this maturity—124 production-ready pipelines, 1,400+ reusable modules, and 10,000+ active Slack users demonstrate community-scale adoption. Galaxy's 500,000+ registered users access 9,000+ scientific tools through zero-code web interfaces. Oxford Academic These platforms succeeded by recognizing that life scientists fundamentally differ from software engineers: they need reproducibility without requiring DevOps expertise.

Systems research tells a starkly different story. The May 2025 workshop report on HPC reproducibility identifies that 60.39% of Docker-related StackOverflow posts have no accepted answers, signaling a profound expert scarcity. arXiv +2 At SOSP 2023, artifact evaluation revealed that 50% of reviewers were first-time evaluators, many unable to distinguish between validating reproducibility and critiquing research methodology. ACM SIGOPSACM SIGOPS The June 2024 study of 13 distributed systems conferences found artifact evaluation practices "lag behind other computing disciplines"—only ~50% followed comprehensive guidelines, and merely 48% of submitted artifacts received "Results Reproducible" badges.

This divergence stems from fundamentally different experimental paradigms. Bioinformatics workflows process data through sequential tool pipelines—well-suited to workflow orchestration abstractions. The Carpentries Systems research demands bare-metal hardware access, specific firmware versions, complex network topologies, and precise timing characteristics that resist abstraction. A neural network training pipeline can run on any GPU with Docker; a networking experiment examining microsecond-scale latency requires exact hardware matching down to microarchitecture and device drivers.

## Gap papers reveal systemic barriers unsolved by current tools
Recent gap-identification papers expose that containerization's promise remains largely unfulfilled for non-experts across both domains, with technical complexity, knowledge gaps, and time costs forming insurmountable barriers.

### The expertise chasm persists despite tooling advances
The August 2020 StackOverflow analysis of Docker challenges found that container development "requires knowledge on various domains like networking, operating system, cloud computing and software engineering"—a combination few researchers possess. arxiv Critically, networking errors (66.29% unresolved), memory management (65.24% unresolved), and web browser issues (69.47% unresolved) indicate that even when researchers attempt containerization, they frequently fail without expert assistance. 

Bioinformatics papers echo this finding. The January 2022 Frontiers in Bioinformatics paper notes "containers are rarely used so far in the image analysis field, as building a container may appear difficult at first glance." PubMed Central Despite microscopy's clear need for reproducibility—where software versions "change fast" and reproducing pipelines becomes "time-consuming at best or impossible at worst"—adoption remains minimal. frontiersinFrontiers The October 2023 "Five Pillars" paper in Briefings in Bioinformatics confirms that while Docker is extensively used in bioinformatics, "improper version control and documentation remain issues." PubMed Central Even within the community that has adopted containers most successfully, fundamental practices remain broken.

The July 2023 Nature Reviews Methods Primers paper quantifies security risks: hundreds of vulnerabilities exist in neuroscience data analysis containers. This reveals a critical gap—researchers focus on functional reproducibility while ignoring security implications, creating privacy and integrity risks especially problematic in clinical settings.

### Systems research faces uniquely intractable reproduction challenges
The May 2025 workshop report on practical reproducibility identifies seven fundamental barriers in systems/HPC research: incomplete artifact descriptions, hardware dependencies, poor packaging quality, complex environment setup, prohibitive costs, reviewer recruitment difficulties, and artifact decay over time. Quantitatively, artifact evaluation demands 13 hours per artifact on average, with total reviewer commitments reaching 40-50 hours. ACM SIGOPS A longitudinal study of ML-security papers required 10,000 CPU-hours and 8 person-years to reproduce 744 papers—costs utterly prohibitive at scale.

The June 2024 study of distributed systems conferences enumerates seven technical challenges unique to this domain: exact hardware matching requirements including vendor, microarchitecture, firmware, and device drivers; diverse software stacks from hypervisor to application; large-scale environments requiring hundreds to thousands of nodes; resource heterogeneity complicating coordination; autonomous self-tuning mechanisms operating beyond experimenter control; unclear experimental boundaries; and inherent nondeterministic behavior from network timing. 

Internet systems face an additional fundamental barrier: unknowable ground truth. The 2021 EuroSys Best Artifact paper observes that in Internet experiments, "fundamental conditions are unknowable"—it's impossible to determine whether application performance reflects system quality or merely favorable "Internet weather." This necessitates emulated testbeds, but reproducing such environments proves extremely difficult. ACM SIGOPS Statistical evidence: of 177 papers at top-tier systems conferences, **only 68% submitted artifacts, and only 48% received "Results Reproducible" badges**.

### Time and incentive structures make reproducibility unsustainable
Gap papers consistently identify that reproducibility's cost-benefit ratio fails to motivate adoption. The 2020 PLOS Computational Biology "Ten Simple Rules" paper notes researchers "lack time and incentives" and face "substantial technical challenges in maintaining software and documentation." PLOSWellcomeopenresearch The 2024 community workshop found that current incentive structures "don't outweigh considerable costs"—flat badge systems provide no credit differentiation for high-quality artifacts versus minimal efforts. 

Procedurally, systems conferences compound this problem with impossibly short timelines. The 2021 EuroSys artifact evaluation gave authors only 3 days between acceptance and artifact submission, leading to "haphazard collections of scripts." ACM SIGOPSACM SIGCOMM The May 2025 workshop report documents 10-14 day windows for authors to package complex experiments—adequate for simple applications but wholly insufficient for HPC or distributed systems requiring coordinated multi-node deployments. 

Perhaps most damaging: artifacts become unsearchable and unfindable after evaluation. The workshop identified a "findability crisis"—artifacts live on GitHub while papers reside in digital libraries, with no integration between repositories. Collections exist but lack indexing comparable to paper databases. ACM SIGOPSarxiv This renders reproducibility a one-time evaluation exercise rather than enabling cumulative scientific progress.

## Solution papers: Sophisticated tools for narrow audiences
The solution landscape divides into two categories:** workflow orchestration** systems (Nextflow, Galaxy, Snakemake, Binder) and testbed infrastructure (Chameleon, POWDER, CloudLab). Both achieve technical sophistication but reveal fundamental limitations in addressing non-expert usability at scale.

### Bioinformatics solutions: Mature but community-bound
The 2025 Nextflow/nf-core paper in Genome Biology represents the pinnacle of bioinformatics workflow systems. DSL2 enables modular components, 1,400+ reusable modules provide building blocks, and 124 community-curated pipelines deliver turnkey solutions. Training materials have 35,000+ YouTube views, and 10,000+ Slack users provide community support. The system supports Docker, Singularity, Conda, and Bioconda, automatically handling environment setup.

Galaxy (2024 update, Nucleic Acids Research) offers even more radical abstraction—zero programming required through point-and-click interfaces. The visual workflow editor with graphical "noodles" connecting tools enables non-programmers to construct sophisticated analyses. Training Infrastructure as a Service (TIaaS) reserves compute resources for workshops, eliminating queue time frustrations. With 500,000+ registered users across public instances, Galaxy demonstrates genuine mass adoption.

Yet these solutions share critical limitations. They serve domain-specific communities with shared tool ecosystems—bioinformatics pipelines fundamentally resemble each other, enabling standardization. The 2024 CREDO tool (BMC Bioinformatics) exemplifies this: it generates Dockerfiles specifically for Bioconductor, Conda, and Bioconda packages with a GUI interface. biomedcentral This solves a real problem for bioinformaticians but provides zero value to neuroscientists using different tool stacks, or social scientists running statistical analyses.

The 2023 Neural Simulation Pipeline (Frontiers in Neuroinformatics) demonstrates the generalization challenge. PubMed Central Despite providing 35 Bash scripts and 16 PowerShell scripts for GENESIS/PGENESIS neural simulators, it serves only the narrow community using these specific simulation engines. nih Each scientific subdomain requires custom tooling, preventing the economies of scale that would enable truly non-expert-friendly solutions.

### Infrastructure solutions: Powerful but expert-oriented
The 2020 Chameleon testbed paper (USENIX ATC) presents a sophisticated platform supporting 4,000+ users across 500+ projects. ChameleoncloudUchicago Bare-metal access enables full software stack control, appliance sharing captures complete environments, and OpenStack provides familiar cloud abstractions. Readthedocs The 2020-2023 Trovi platform adds Jupyter integration for one-click reproducibility with automatic resource provisioning, Zenodo archival, and GitHub version control.

The 2020-2021 POWDER platform (WiNTECH/Computer Networks) delivers city-scale software-defined wireless testbeds with controllable RF environments, remote access, and open-source 5G capabilities added in 2023. ACM Digital LibraryACM Digital Library The 2023 KheOps framework (ACM REP) enables reproducibility across the edge-to-cloud continuum, coordinating experiments across Chameleon, Grid'5000, and CHI@Edge.

These represent remarkable engineering achievements, yet they fundamentally assume expert users. A 2024 technical report evaluating SC24 artifacts **found only 1 of 45 submissions used Trovi for one-click reproducibility** despite its availability. arXiv +3 Researchers defaulted to manual configuration scripts, suggesting either awareness gaps or trust issues with abstraction layers. The testbeds succeed for their core audience—systems researchers comfortable with infrastructure-as-code—but do nothing to help a social scientist trying to share a computational model.

The 2021 Popper workflow engine (IPDPSW) illustrates the expert assumption problem. It applies DevOps principles to scientific experimentation with declarative YAML workflows, separates logic from environment configuration, and supports Docker/Singularity/Podman with SLURM/Kubernetes integration. IEEE Xplore For someone fluent in CI/CD systems, Popper provides elegant abstractions. For a domain scientist unfamiliar with continuous integration concepts, YAML configuration files and resource manager integration represent yet another technical hurdle.

### The abstraction paradox: Simpler interfaces hide greater complexity
Multiple solution papers reveal an uncomfortable truth: making containers easier to use often requires more sophisticated infrastructure, creating brittleness and vendor lock-in. Binder's repo2docker automatically converts Git repositories to Docker containers—magical when it works, but users must structure repositories according to Reproducible Execution Environment Specifications. Project JupyterThe Binder Project Galaxy's web interface hides all containerization details, but Galaxy-specific tool wrappers must be written for each computational tool. Code Ocean's Compute Capsules® provide turnkey reproducibility through proprietary cloud infrastructure unavailable for on-premises deployment.

The 2024 WorkflowHub registry (Scientific Data) attempts to bridge workflow systems—supporting Galaxy, Nextflow, Snakemake, and others through RO-Crate packaging. Yet this meta-solution introduces another layer: researchers must now learn WorkflowHub's metadata schemas to make workflows findable. Each abstraction layer trades immediate usability for long-term technical debt.

BioContainers (2021, Journal of Proteome Research) represents perhaps the most sustainable approach: 9,000+ pre-built tool containers following "one tool, one container" principles, automated building from Bioconda recipes, and availability through multiple registries (quay.io, Docker Hub). By providing containers rather than container-building tools, BioContainers eliminates the expertise requirement entirely. However, this model only works for mature, stable tools with active maintainer communities—precisely what many cutting-edge research projects lack.

## Gap papers are more valuable for advancing the field
For researchers developing new containerization solutions for non-experts, gap-identification papers provide substantially greater research value than solution papers. This conclusion emerges from three critical observations about the current landscape.

- **Solution papers describe tools, not generalizable principles**: The May 2025 workshop report on practical reproducibility synthesizes seven fundamental barriers applicable to any reproducibility system: completeness, hardware dependencies, quality, environment setup, cost, incentives, and longevity.
- **Gap papers reveal why existing solutions fail to generalize**: Multiple solution papers claim to improve usability for non-experts, yet gap papers show adoption remains limited. _This suggests the problem lies not in containerization technology itself but in scientific workflow practices. Tools providing better Docker interfaces don't address the root cause._
- **Gap papers articulate unmet needs that define research opportunities**: The most valuable gap papers don't merely list problems—they define solution requirements with precision.

## Why Container Adoption Low
- Expertise Barrier
  - Requiring knowledge across networking, operating systems, cloud computing, and software engineering simultaneously
  - Improper version control and documentation remain pervasive issues
 
- Cost Benefit Analysis
  - No citation credit, no authorship recognition, no hiring committee asking about reproducibility contribution

- Abstraction Has Problems
  - The "easier" tools like Galaxy, Nextflow, and Binder succeed by hiding complexity, but this creates brittleness (specific versins or no extensibility)
 
- Even when researchers successfully create reproducible artifacts, they become unsearchable and unfindable after evaluation. Artifacts live on GitHub, papers in digital libraries, with no systematic connection between them. There's no "Google Scholar for reproducible artifacts."

- The fundamental issue is that we've treated reproducibility as a technical problem requiring better tools, when it's actually a social/institutional problem requiring different incentive structures, workflows, and support systems. Better container technology won't fix broken incentives or intractable domain barriers.




