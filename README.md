# Astrona Training Path: {{ .title }}

This repository contains the blueprint for an **Astrona Training Path (ATP)**.

## What is a Training Path?

An ATP represents a **complete, end-to-end learning course** designed to cover multiple different domains, competencies, and milestones. While individual educational units (like labs, readings, and exercises) are self-contained inside **Astrona Training Specifications (ATS)**, the ATP strings these modules together into a complete, structured curriculum or learning path.

### Exam Preparation Courses (e.g., CNCF or Linux Foundation Certifications)
When a training path is designed for professional exam preparation—such as **Linux Foundation LFCS** or **CNCF CKA/CKAD**—the path structure directly reflects the certification's official syllabus domains. 

To achieve this, the ATP schema supports two crucial features:
1. **`examPreparation` Mapping:** Declares whether the course is aligned with an official professional exam, and specifies metadata to connect with the provider:
   * `enabled` (boolean): Flag to turn on exam mapping.
   * `title` (string): The full name of the certification.
   * `officialSyllabusUrl` (string): A direct link to the official exam outline, such as `https://training.linuxfoundation.org/certification/linux-foundation-certified-sysadmin-lfcs/`.
   * `examId` (string): The standard code/identifier for the exam (e.g., `LFCS` or `CKA`).
   * `provider` (string): The body issuing the certification (e.g., `The Linux Foundation` or `CNCF`).
2. **Domain `weight` Percentages:** Every stage in the path can carry a numeric weight. This maps directly to the official certification syllabus weight (e.g., setting a stage weight to `25` representing 25% of the exam coverage).

---

## Designing Your Path

### 1. Plan Your Course Domains
Before writing code, map out the comprehensive path. If you are building a CNCF or other industry exam prep course, gather the official domain percentages. Break the path down into **Stages** corresponding directly to those domains.

### 2. Configure Stage Weights
For exam-aligned courses, assign a relative `weight` percentage to each stage in `path.yaml` to specify its importance and guide the learner's focus:
* **Cluster Architecture & Setup:** 25%
* **Services & Networking:** 20%
* **Troubleshooting & Debugging:** 30%

### 3. Specify Prerequisites and Outcomes
Use active, measurable verbs for stage and global outcomes:
* **Good:** "Initialize a multi-node cluster using kubeadm", "Isolate broken control plane nodes".
* **Avoid:** "Learn cluster setup", "Understand how to troubleshoot".

### 4. Reference ATS Resources
Inside each stage, link to the relevant spec ID (`ATSxxx`) and its remote Git repository SSH/HTTPS address. All referenced specifications must be reachable and valid for the CLI package builder to compile successfully.

The `version` field represents the git reference (tag, commit, or branch) that the builder will checkout:
* **Development Phase:** Reference an active development branch (e.g., `"main"` or `"dev"`) to quickly test updates and build continuous integration packages.
* **Release Phase:** Once development is finalized and you are ready to ship a static, stable release of the path, tag your ATS repositories with version numbers and update the path's references to point to these fixed version tags (e.g., `"1.0.0"` or `"2.3.1"`) to guarantee 100% reproducible and deterministic builds.

---

## Editor Workflow

Edit `path.yaml` to define your path. Run these Astrona CLI commands to test and preview changes:

```bash
# Verify YAML schema validity and resolve all ATS references
astrona content validate

# Compile the training path into a release artifact
astrona content build

# Open a local web browser to preview the path as a learner
astrona content preview
```

## Where Content Lives

Keep a clean boundary between structure and content:
* **Modify here:** Path organization, stage definitions, exam preparation options, prerequisites, outcomes, and metadata in `path.yaml`.
* **Modify in ATS:** Reading prose, exercises, lab configs, and grading scripts. If you need new content, run `astrona content init spec ATSxxx` to create a separate spec.

---

## Teacher Checklist

Verify these requirements before publishing the path:

- [ ] Target audience and difficulty level are set.
- [ ] If aligned to an exam, `examPreparation` block is configured with correct metadata.
- [ ] Stage `weight` percentages are set and align with the certification blueprint.
- [ ] Prerequisites and outcomes are explicit.
- [ ] Overall and Stage outcomes use action-oriented verbs.
- [ ] All ATS references and version ranges point to exact, fixed tags.
- [ ] `astrona content validate` runs without errors.
