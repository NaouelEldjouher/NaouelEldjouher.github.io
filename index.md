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

<style>
  .note-card {
    background-color: #1e1e1e;
    border: 1px solid #333;
    border-radius: 8px;
    padding: 15px 20px;
    margin-bottom: 20px;
    box-shadow: 0 4px 6px rgba(0,0,0,0.3);
  }
  .note-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 1px solid #333;
    padding-bottom: 8px;
    margin-bottom: 12px;
  }
  .note-title { font-weight: bold; color: #e0e0e0; margin: 0; font-size: 1.1em; }
  .note-date { color: #81a1c1; font-size: 0.85em; }
</style>

## 🧬 OmniDomain Build Logs
*I am building in public. These are my daily architectural notes and challenges.*

{% for post in site.posts limit:10 %}
  <div class="note-card">
    <div class="note-header">
      <span class="note-title">{{ post.title }}</span>
      <span class="note-date">{{ post.date | date: "%b %d, %Y" }}</span>
    </div>
    <div style="font-size: 0.95em; line-height: 1.5;">
      {{ post.content }}
    </div>
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
* 📧 **Email:** [hellonaouel[at]gmail.com]
