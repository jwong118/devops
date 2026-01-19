<!-- Copied/updated by AI to help coding agents work productively in this repo -->
# AI Coding Instructions for this repository

Purpose: help an AI coding agent be immediately productive by describing the repository's architecture, developer workflows, and concrete examples.

Short summary
- This repository is a collection of DevOps and Kubernetes lab artifacts (mostly declarative YAML, CI configs and how‑to notes).
- Major focus: Kyverno policies (labs under `lab/kyverno`), GitLab CI examples (`lab/gitlab`), Docker notes (`lab/docker/docker_command.md`).

Big picture & file organization
- `lab/kyverno/` — standalone Kyverno policies and small lab files (e.g. `lab04-require_annotations.yaml`, `lab05-02-check_dev_deployment_replica.yaml`). These are single-policy YAMLs you can `kubectl apply -f`.
- `lab/kyverno/LFS255-code-public/` — chapter-based lab content used for the LFS255 course. Example chapters contain policy examples, test fixtures and demonstrations.
  - Example test fixtures: `lab/kyverno/LFS255-code-public/chapter-07-policy-validate-and-testing/lab7.2/tests/require_annotations/` (contains `kyverno-test.yaml`, `pod_with_annotation.yaml`, `pod_without_annotation.yaml`).
- `lab/gitlab/` — GitLab CI example pipelines (multiple `gitlab-ci*.yml` files). These are GitLab CI examples (not GitHub Actions).
- `lab/docker/docker_command.md` — common docker commands and examples for building/running images.

What a change usually looks like
- Most changes are edits to YAML (Kubernetes manifests or Kyverno policies). Preserve top-level keys: `apiVersion`, `kind`, `metadata.name`, `spec` and policy-specific fields such as `validationFailureAction`, `background`, `rules`, `match`, `validate`, `pattern`, `preconditions`.
- When updating a Kyverno policy, update the corresponding test fixtures (if present) in `LFS255-code-public/.../tests/` to keep examples consistent.

Concrete commands & workflows (discoverable in repo)
- Apply a YAML/policy to a cluster:
```
kubectl apply -f lab/kyverno/lab04-require_annotations.yaml
kubectl delete -f lab/kyverno/lab04-require_annotations.yaml
```
- Use Kyverno checklist commands referenced in `lab/kyverno/Kyverno_CheatSheet.MD` (examples):
```
# view cluster policies
kubectl get clusterpolicy
# delete by file
kubectl delete -f <policy_file.yaml>
```
- Docker build/run examples are in `lab/docker/docker_command.md` (use those commands as-is for local container experimentation).
- CI: the repo contains GitLab CI example YAMLs under `lab/gitlab/`. Do not attempt to run them in GitHub Actions without conversion.

Project-specific conventions
- Lab-oriented layout: files are grouped by lab/chapter (do not rename chapters unless restructuring the course material).
- Examples are treated as canonical lab artifacts — keep them readable and minimal. When adding new examples, follow the existing naming style: `labXX-<short-desc>.yaml` or place them in the corresponding `chapter-XX` folder under `LFS255-code-public`.
- Tests / fixtures follow this pattern: a policy file + one or more example resources demonstrating pass/fail behavior are co-located in `.../tests/<test-name>/`.

How to write prompts for changes (recommended)
- Be explicit with file paths and the intent. Good example:
  - "Update `lab/kyverno/lab05-02-check_dev_deployment_replica.yaml` so the policy requires `replicas: 2` for deployments labeled `env: dev`. Also update the test fixture `LFS255-code-public/chapter-07-policy-validate-and-testing/lab7.2/tests/require_annotations/` to include a matching positive and negative example."
- When editing CI files, mention the target runner/environment (GitLab CI) and the example file path in `lab/gitlab/`.

Safety & editing rules for AI agents
- Do not invent new build/test systems: there is no package manager, build script, or tests harness in the repo root — focus on YAML and docs present in `lab/`.
- Preserve YAML structure and indentation. Use existing examples as templates.
- When adding or changing policies, update or add test fixtures under the corresponding `tests/` directory if one exists for that chapter.

Key files to inspect for context (start here)
- `lab/kyverno/Kyverno_CheatSheet.MD` — commands and short guide.
- `lab/kyverno/lab04-require_annotations.yaml` — small example policy (validation pattern).
- `lab/kyverno/lab05-02-check_dev_deployment_replica.yaml` — example using `preconditions`.
- `lab/kyverno/LFS255-code-public/chapter-07-policy-validate-and-testing/lab7.2/tests/require_annotations/` — concrete test fixtures.
- `lab/gitlab/` — GitLab pipeline examples.
- `lab/docker/docker_command.md` — docker examples.

If anything here is unclear or you want more detail for a specific workflow (for example: adding a GitHub Actions conversion, adding a Kyverno test harness, or a suggested naming convention), tell me which workflow to expand and I'll iterate.
