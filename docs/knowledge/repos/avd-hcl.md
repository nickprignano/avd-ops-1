---
title: "avd-hcl"
summary: "HCL lane: native Azure Virtual Desktop deployed and operated with Terraform and Packer, beside avd-landing-zone"
topic: repos
status: verified
last_reviewed: 2026-11-09
---

# avd-hcl

Native Azure Virtual Desktop deployed and operated with Terraform and Packer in its own HCL lane, beside avd-landing-zone.

<!-- more -->

The repo is the source of truth: [avd-ops/avd-hcl](https://github.com/avd-ops/avd-hcl). This page says where it fits.

## What it does

It builds and operates a cloud-native AVD estate with Terraform modules and a Packer golden-image template.

- Deploys pooled or personal Entra-joined host pools, workspaces, application groups, scaling plans, FSLogix on Premium Azure Files, Key Vault and AVD Insights in `modules/` and `environments/example/01-platform/`.
- Builds an Azure Compute Gallery in `environments/example/02-images/` and a Windows 11 multi-session golden image with WDOT in `packer/avd-win11/`.
- Runs a read-only readiness preflight check (`scripts/preflight.py`) and a keyless gated GitHub Actions pipeline (`modules/deploy-pipeline/`) driven by one parameter schema (`schema/parameters.json`).

## How it fits

It sits beside avd-landing-zone as a separate HCL-lane sibling so the Bicep and PowerShell repos stay free of HCL.

- [avd-landing-zone](avd-landing-zone.md) and [avd-current-state](avd-current-state.md) never depend on `avd-hcl`.
- Reuses the estate design and real-run lessons of [avd-landing-zone](avd-landing-zone.md) as offline `terraform test` suites, and can be checked read-only by [avd-current-state](avd-current-state.md).

## Read more in the repo

The repo has the full detail. Start here:

- [README and offline test suite](https://github.com/avd-ops/avd-hcl/blob/main/README.md)
- [Platform modules and lessons](https://github.com/avd-ops/avd-hcl/blob/main/docs/knowledge/platform.md)
- [Gated deploy pipeline](https://github.com/avd-ops/avd-hcl/blob/main/docs/knowledge/pipeline.md)
