# CI Governance

## Overview

This repository serves as the **enforcement kernel** for CI/CD governance policies. It defines the policy structure and standards for CI/CD operations without implementing enforcement mechanisms or bindings to downstream repositories.

**Role**: Policy definition and audit framework  
**Status**: Reference implementation  
**Base120 Version**: v1.0 (FROZEN)  
**Base120 Binding**: ✓ ACTIVE (Hash-pinned, CI-enforced)

## Base120 v1.0 Binding

This repository is **built on Base120 v1.0** as immutable infrastructure:

- **SHA256**: `6df3bd9f64693183ed2509e2ca6855a5690c721646e2357b088c3bd4d2cd88b1`
- **Status**: Immutable, frozen, hash-pinned
- **Enforcement**: Automated CI verification on every commit
- **Compliance**: Non-canonical, audit-grade

**Key Files**:
- `base120-dependency.yaml` - Dependency declaration with hash pinning
- `base120-mrcc.yaml` - Machine-readable compliance claim
- `base120-narrative-claim.md` - Narrative compliance documentation
- `.github/workflows/base120-*.yml` - CI enforcement workflows

**Documentation**:
- `ARCHITECTURE.md` - Technical architecture and binding design
- `_CURRENT_STATE.md` - Current binding status and verification results
- `GOVERNANCE.md` - Governance model including Base120 enforcement

## Repository Structure

```
ci-governance/
├── base120-invariant-registry.yaml    # Read-only invariant definitions (FROZEN)
├── base120-dependency.yaml            # Base120 v1.0 binding declaration
├── base120-mrcc.yaml                  # Machine-readable compliance claim
├── base120-narrative-claim.md         # Narrative compliance claim
├── policies/
│   ├── workflow-baselines/            # Workflow policy baselines
│   │   ├── pr-validation-baseline.yaml
│   │   ├── build-baseline.yaml
│   │   └── release-baseline.yaml
│   └── pr-classification/             # PR classification rules
│       └── classification-rules.yaml
├── schemas/
│   └── policy-schema.yaml             # Policy structure schemas
├── .github/workflows/                 # CI enforcement
│   ├── base120-hash-verification.yml
│   ├── base120-schema-validation.yml
│   └── base120-drift-detection.yml
├── ARCHITECTURE.md                    # Architecture documentation
├── _CURRENT_STATE.md                  # Current state tracking
├── GOVERNANCE.md                      # Governance model
└── README.md                          # This file
```

## Components

### 1. Base120 Invariant Registry

**File**: `base120-invariant-registry.yaml`  
**Status**: FROZEN (v1.0)  
**Purpose**: Read-only reference of governance invariants

The invariant registry defines immutable CI/CD governance rules across categories:
- Build Integrity (INV-001, INV-002)
- Artifact Integrity (INV-003, INV-004)
- Code Quality (INV-005, INV-006)
- Security (INV-007, INV-008, INV-009)
- Access Control (INV-010, INV-011)
- Audit Trail (INV-012, INV-013)
- Deployment (INV-014, INV-015)

**Important**: This registry is frozen and must not be mutated. It serves as the canonical source of truth for policy definitions.

### 2. Workflow Baselines

**Directory**: `policies/workflow-baselines/`  
**Purpose**: Define CI workflow policy structures

Workflow baselines establish the reference implementation for CI/CD workflows:

- **PR Validation Baseline** (`pr-validation-baseline.yaml`)
  - Pre-validation checks
  - Code quality validation
  - Security scanning
  - Test execution requirements

- **Build Baseline** (`build-baseline.yaml`)
  - Pre-build validation
  - Reproducible build requirements
  - Artifact generation policies
  - Provenance and SBOM requirements

- **Release Baseline** (`release-baseline.yaml`)
  - Pre-release validation
  - Security validation
  - Approval gate requirements
  - Publication policies

Each baseline references applicable invariants from the Base120 registry.

### 3. PR Classification Rules

**File**: `policies/pr-classification/classification-rules.yaml`  
**Purpose**: Define how pull requests are classified

Classification dimensions include:
- **Impact Scope**: critical, standard, documentation, configuration
- **Change Size**: small, medium, large, massive
- **Risk Level**: high-risk, medium-risk, low-risk

Classifications determine which workflow baselines and additional checks apply to each PR.

### 4. Policy Schema

**File**: `schemas/policy-schema.yaml`  
**Purpose**: Document policy structure formats

Defines the schema for:
- Invariant registry structure
- Workflow baseline format
- PR classification format
- Validation rules

## Design Principles

### 1. Enforcement Kernel, Not Executor
This repository defines **what** should be governed, not **how** to enforce it. Implementation and enforcement are the responsibility of downstream systems.

### 2. Audit-Grade Language
All policies use neutral, precise language suitable for compliance audits and security reviews.

### 3. No Downstream Enforcement
This repository does **not**:
- Enforce policies on downstream repositories
- Contain executable workflows
- Store secrets or production credentials
- Perform org-wide actions
- Mutate the frozen Base120 invariant registry

### 4. Read-Only Reference
The Base120 invariant registry is frozen and serves as a read-only reference. Modifications require a new major version.

## Usage

### For Policy Consumers

1. **Reference Invariants**: Use invariant IDs (e.g., INV-007) to reference specific governance requirements
2. **Apply Baselines**: Map workflow baselines to your CI/CD pipelines
3. **Classify PRs**: Use classification rules to determine applicable policies
4. **Validate Compliance**: Compare implementations against defined policies

### For Auditors

1. Review `base120-invariant-registry.yaml` for governance requirements
2. Verify downstream implementations reference correct invariant IDs
3. Check workflow implementations against baseline policies
4. Validate PR classification logic against defined rules

## Compliance and Audit

### Audit Trail Requirements
- All policies include audit trail specifications
- Retention periods are defined per policy type
- Classification decisions must be logged

### Validation
Policy structures can be validated against schemas defined in `schemas/policy-schema.yaml`.

## Extending Policies

While the Base120 invariant registry is frozen, organizations can:
- Define additional workflow baselines
- Create custom classification dimensions
- Add organization-specific checks (referencing existing invariants)

Extensions must not contradict or weaken frozen invariants.

## Versioning

- **Base120 Registry**: v1.0 (FROZEN)
- **Policy Schema**: v1.0.0
- **Workflow Baselines**: v1.0
- **Classification Rules**: v1.0

## Security Considerations

This repository contains **policy definitions only**:
- No secrets or credentials
- No production configurations
- No executable enforcement code
- No access to org-wide resources

## License

Internal Use Only - Governance Reference

## Contact

For questions about governance policies, consult your organization's compliance team.

---

**Note**: This is a scaffolding repository. Policies are advisory by default and require implementation in downstream systems for enforcement.