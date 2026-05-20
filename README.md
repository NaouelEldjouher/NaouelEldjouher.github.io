<style>
  body {
    background-color: #121212 !important;
    color: #e0e0e0 !important;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif;
  }
  a { color: #81a1c1 !important; text-decoration: none; }
  a:hover { text-decoration: underline; }
  hr { border-color: #333 !important; }
  code { background-color: #2e3440 !important; color: #eceff4 !important; padding: 2px 6px; border-radius: 4px; }
</style>
Full-Stack Bioinformatician

I specialize in plant and bacterial genomics, bridging high-throughput wet-lab insights with containerized, cloud-native infrastructure and Nextflow. 

---
### 🚀 Current Focus: OmniDomain
**The Architecture of a Multi-Kingdom Genomic Platform**
I am building a unified platform to consolidate my bacterial, fungal, and plant genomic pipelines into a single, scalable codebase. Instead of isolated one-off scripts, I am developing a shared "control plane" using Nextflow, AWS Batch, and Streamlit to treat infrastructure as a reusable utility.

*   **Status:** Active Development (Day 1 Documentation)
*   # Blog Notes: Building OmniDomain (Day 1)

After finishing my work on **NextAMR**, I wanted to expand my research to include fungal and plant analysis, all in one place. To do this, I’m building **OmniDomain**: a central management platform that consolidates genomic analysis into a single, unified codebase. By leveraging a shared "control plane" powered by AWS Batch and a Streamlit dashboard, I’ve replaced the model of one-off pipelines with a standardized framework. This treats infrastructure as a reusable utility—meaning any improvement in storage, processing, or pipeline logic is instantly inherited across all research areas, allowing me to focus on the science rather than the setup.

---

### The Scope & Challenge
To scale successfully, my architecture must accommodate vastly different biological requirements:

| Engine | Target | Genome Size | Key Challenge |
| :--- | :--- | :--- | :--- |
| **NextAMR** | Bacteria | 2–6 Mb | AMR gene detection, plasmid resolution |
| **FungalFlow** | Fungi | 20–80 Mb | Gene prediction, BGC discovery |
| **PlantFlow** | Plants | 100 Mb – 16 Gb | Polyploidy, 40–85% repeat content |

---

### The Blueprint
I am using my **NextAMR** pipeline as the foundation, porting its engine—global `nextflow.config` files, retry logic, and subworkflow abstractions—to create a "Base Architecture" that works across kingdoms.

**Core Focus Areas:**
*   **Infrastructure Inheritance:** Improving a container strategy or fixing a memory bug in one pipeline instantly updates the entire ecosystem.
*   **Modular Subworkflows:** Abstracting repetitive tasks (QC, repeat masking) into shared, reusable logic.
*   **AWS Cost Management:** Utilizing Spot instance strategies, S3 intelligent storage, and resource profiling to balance performance with exponentially scaling data costs.

---

### Current Status
*   **🧬 Metacflow:** Stable foundation for metagenomics.
*   **🌱 OmniFlora:** Testing plant HiFi assembly architecture.
*   **🍄 FungalFlow:** Scaling assembly and BGC detection.

---

### The Learning Curve
Designing an `nf-core` module system flexible enough to handle bacterial binning while remaining robust enough for complex plant assemblies is a significant architectural challenge. Coming from a bacterial-focused background, scaling my logic to the eukaryotic domain—where genome sizes and repeat content require drastically different computational approaches—is my biggest hurdle.

---

### What's Next?
I’ve started the **Technical Design Document (TDD)** to map out the infrastructure. Future notes will cover:
1.  **Nextflow Architecture:** Folder structures and module scopes.
2.  **Streamlit Control Plane:** Building the unified UI.
3.  **AWS Infrastructure:** Terraform configurations for cost-efficient compute.

I’m "learning in public." The goal isn't perfection, but building a system I can actually maintain.

**Follow the progress:** [github.com/NaouelEldjouher](https://github.com/NaouelEldjouher)


### 🚀 Blog Post

I recently published a deep-dive architectural breakdown of my end-to-end cloud platform.
* 📖 **Read on Medium:** [From Terminal Scripts to the Cloud: Designing an Automated AMR Detection Platform with Nextflow and AWS](https://medium.com/@NaouelEldjouher/from-terminal-scripts-to-the-cloud-designing-an-automated-amr-detection-platform-with-nextflow-and-55bfb16090e7?postPublishedType=repub)
* **Current Project:** [My OmniDomain Architecture Notes (Day 1)](blog/day-1-omnidomain.md)

---

### 💻 Projects

#### 🧬 NextAMR (AMR-Flow) — Cloud-Native Bacterial Genome Assembly & AMR Profiling
*Nextflow DSL2 | AWS Batch | Amazon S3 | Docker | Terraform | Streamlit*
* **Automated Cloud Infrastructure:** Provisioned an event-driven AWS architecture using Terraform (IaC) to handle automated job submission via AWS Batch.
* **Cost Efficiency & Portability:** Optimized cloud spend by leveraging EC2 Spot instances and containerized the entire pipeline using Docker for cross-platform reproducibility.
* 🐙 **Code & Architecture:** [Explore the NextAMR Repository on GitHub](https://github.com/NaouelEldjouher/NextAMR)

#### 🎓 Baktflow — Automated Bacterial Genome Analysis Pipeline
*M.Sc. Thesis Project | Nextflow | Genome Assembly & Functional Annotation*
* **Reproducible Workflows:** Built an end-to-end bacterial genomics workflow to automate quality control, short/long-read hybrid assembly, and downstream annotation.
* **Academic Foundations:** Developed as the core software deliverable for my M.Sc. thesis at Justus Liebig University Giessen.(Record: [Zenodo 10.5281/zenodo.14995561](https://zenodo.org/records/14995561)

---

### 🛠️ Tools & Technologies I Work With

* **Bioinformatics:** NGS Data Analysis, Plant & Bacterial Genomics, AMR Profiling, GATK Best Practices, Variant Calling, FastP, Unicycler, Bakta
* **Workflow & Cloud:** Nextflow DSL2, AWS (Batch, S3, EC2), Terraform (Infrastructure as Code), Docker, Bash scripting, Slurm HPC
* **Data Science:** Python, R (Tidyverse), SQL, Pandas

---

### 📫 Connect With Me

* 💼 **LinkedIn:** [linkedin.com/in/naoueleldjouher](https://linkedin.com/in/naoueleldjouher)
* 🐙 **GitHub Profile:** [github.com/NaouelEldjouher](https://github.com/NaouelEldjouher)
* 📧 **Email:** [hellonaouel@gmail.com](mailto:hellonaouel@gmail.com)
