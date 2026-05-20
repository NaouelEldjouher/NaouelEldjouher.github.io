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

## 🧬 OmniDomain Build Logs
I'm building something new for me to follow my learning journey. 
## Recent Build Notes
{% for post in site.posts %}
  <div class="post-preview">
    <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
    <p>{{ post.date | date: "%B %d, %Y" }}</p>
  </div>
{% endfor %}



### 🚀 Blog Post

I recently published a deep-dive architectural breakdown of my end-to-end cloud platform.
* 📖 **Read on Medium:** [From Terminal Scripts to the Cloud: Designing an Automated AMR Detection Platform with Nextflow and AWS](https://medium.com/@NaouelEldjouher/from-terminal-scripts-to-the-cloud-designing-an-automated-amr-detection-platform-with-nextflow-and-55bfb16090e7?postPublishedType=repub)


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
