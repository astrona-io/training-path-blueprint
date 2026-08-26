# Astrona Training Path: {{ .title }}

This repository contains the blueprint for an **Astrona Training Path (ATP)**.

An ATP arranges existing educational units (ATS resources) into a structured learning path. It defines target audiences, milestones, progression logic, and final assessments.

This repository does **not** host raw educational content. Reading materials, quizzes, lab environments, and code solutions belong entirely within **Astrona Training Specifications (ATS)**.

---

## Designing Your Path

### 1. Specify Prerequisites and Outcomes
Define who the path is for and what they must know beforehand. Write outcomes using active, measurable verbs:
* **Good:** "Configure a secure firewall ruleset", "Diagnose networking latency".
* **Avoid:** "Understand firewalls", "Learn about networks".

### 2. Group into Stages
Organize the path chronologically using stages. Stages break down a long path into clear milestones, each with its own intermediate outcomes.

### 3. Reference ATS Resources
Inside each stage, link to the relevant ATS identifiers (like `ATS010`) and provide the corresponding Git repository SSH/HTTPS address. All declared resources are required to be reachable and valid for the CLI package builder to compile successfully.

Because specifications evolve, define compatible semantic versions:
* `^1.0.0` — compatible with 1.x.x, but not 2.0.0.
* `>=1.2.0 <2.0.0` — any version from 1.2.0 up to 2.0.0 (exclusive).

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
* **Modify here:** Path organization, stage definitions, prerequisite list, overall outcomes, and metadata in `path.yaml`.
* **Modify in ATS:** Reading prose, exercises, lab configs, and grading scripts. If you need new content, run `astrona content init spec ATSxxx` to create a separate spec.

---

## Teacher Checklist

Verify these requirements before publishing the path:

- [ ] Target audience and difficulty level are set.
- [ ] Prerequisites are explicit.
- [ ] Overall and Stage outcomes use action-oriented verbs.
- [ ] All ATS references and version ranges are valid.
- [ ] Stages follow a logical pedagogical progression.
- [ ] The final assessment points to a valid ATS activity.
- [ ] `astrona content validate` runs without errors.
