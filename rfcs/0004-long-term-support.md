---
# SPDX-License-Identifier: CC-BY-4.0
rfc: 0004
title: Long-term support releases
status: Draft
authors: ["Ramón Roche (mrpollo, Linux Foundation / Dronecode Foundation)"]
created: 2026-09-23
discussion: pending
supersedes: null
license: CC-BY-4.0
---

# RFC-0004: Long-term support releases

## Summary

SGL tracks Yocto Project long-term support (LTS) releases, but nobody in the project has yet defined what an SGL LTS release is. Yocto supports each LTS for four years upstream, while 59 percent of 46 respondents to the SGL Interest Survey operate their systems for five years or more. The goal is that adopters can rely on a defined SGL long-term support release. I propose an LTS and Release Engineering WG that brings the Technical Steering Committee (TSC) a recommended SGL long-term support policy meeting the requirements set out here. I ask the TSC to charter the working group and to ask it for that recommendation, which comes back to the TSC for approval under charter section 2.g.vi.

## Motivation

### Mission lifetimes outrun upstream support

The lifecycle figures below come from the SGL Interest Survey, 46 responses, September 2024 to January 2026. Each lifecycle question sums to 100 percent.

| Lifecycle (of 46 respondents) | Under 1 year | 1 to 3 years | 5+ years | 5 to 10 years | 10+ years |
| --- | ---: | ---: | ---: | ---: | ---: |
| Development | 15% | 52% | 33% | | |
| Operation | 15% | 26% | | 26% | 33% |

Of 46 respondents, 59 percent operate their systems for five years or more, and the median respondent sits in the 5 to 10 year operational band. Add one to three years of development before launch and a program that picks a Yocto release at the start of development needs support well past launch. Yocto Project LTS releases are supported for four years upstream ([Yocto Project][yocto]). That window does not cover the median mission.

The Civil Infrastructure Platform ([CIP][cip]) maintains super long-term support (SLTS) kernels for ten years or more.

### No written policy governs today's releases

SGL already tracks Yocto LTS releases. The first meta-sgl pull request set the base as "Whatever is the LTS, right now Scarthgap" and chose kas for layer management ([May 15, 2025 minutes][m-20250515]). Scarthgap (5.0) is still the base for every CI target today. Wrynose, the new Yocto LTS, is arriving in [meta-sgl][meta-sgl]: a kas configuration (commit dated May 15, 2026), `layer.conf` compatibility (dated August 1), and a bump to 6.0.3 on September 17. The [July 23, 2026 minutes][m-20260723] record "New Kernel, package updates, and the latest meta-virtualization" and a to-do to add Wrynose to CI, and the [August 20, 2026 minutes][m-20260820] carry that as an action item. Kirkstone support was removed by meta-sgl PR #56 (commit b155957, written in May and merged in June 2026; the PR is listed in the [May 21, 2026 minutes][m-20260521]). Neither change was governed by a written policy that tells an adopter how long a series stays supported or how much notice they get before it goes. Nobody in the project has yet written down what "LTS" means for SGL, what support covers, or who decides when a release ends.

### Adopters live on fragmented bases

In the same survey, Yocto is the most common distribution on target (61 percent of 46 respondents; multi-select questions in the survey do not sum to 100 percent), ahead of Ubuntu (35 percent), FreeRTOS (28 percent), RTEMS, Debian, Arch Linux with PREEMPT_RT and Buildroot (15 percent each). The Yocto releases respondents named run from Fido and Sumo through Thud, Dunfell, Hardknott, Honister, Kirkstone, Langdale, Nanbield, Scarthgap and Walnascar, plus PetaLinux 2023.2 and 2024.2. One respondent put the constraint plainly: "Keeping vendor compatibility/support is more important than the version." Of 46 respondents, 35 (76 percent) assemble their OS with an open source builder and package feeds, which means a reproducible build depends on sources and recipes still being fetchable years later. Only 19 of 46 (41 percent) use an SBOM and 22 of 46 (48 percent) run vulnerability management today.

### Build observability has been on the roadmap since 2025

The project has wanted build observability for over a year: "We need observability into what makes to each build, licenses, and all" ([May 15, 2025 minutes][m-20250515]), and "Document why we are making the decision for this footprint" ([June 19, 2025 minutes][m-20250619]). The April 16, 2026 minutes summarize the replies on the thread started by the project roadmap sent to the list ([list message #173][msg-173]) and list "Reproducibility: KAS-based build guarantees" among the key themes ([April 16, 2026 minutes][m-20260416]). meta-sgl CI already uploads build artifacts (PR #45, merged, listed in the [May 21, 2026 minutes][m-20260521]). No written policy yet says which of those artifacts make up a release or how long they are kept.

### CNES asked for reproducibility and separation

CNES's May 21, 2026 KOSMOS talk listed, among open challenges where SGL can help, a "Minimal Yocto distribution definition", "KAS for reproducibility", "Isolation between distribution generation and application code development", and "Maintainability: ... delegating Yocto vs app work to different teams" ([May 21, 2026 minutes][m-20260521]).

## Proposal

### Goal

Adopters can rely on a defined SGL long-term support release.

### Requirements

The SGL long-term support policy that the LTS and Release Engineering WG recommends must meet these requirements:

1. It is written down and published, so an adopter can read, before choosing a release, how long that release is supported, what support covers, and how its support ends.
2. It addresses the needs cited in Motivation: mission lifetimes beyond Yocto's four-year window, fragmented Yocto bases, build observability, and CNES's reproducibility and separation asks.

The recommendation must address:

- What an SGL LTS release contains, and what it leaves to adopters' own application layers. Examples to consider, not a list to adopt: kas lockfiles, SBOMs, mirrored sources, signed artifacts.
- What reproducibility means for an SGL LTS release, and how it is kept for the release's whole support window.
- The cadence of SGL LTS releases, how they relate to Yocto Project releases, and which base the first one uses, given that meta-sgl builds Scarthgap today and Wrynose is arriving.
- The support window, including whether an extended tier aligned to CIP SLTS kernels is needed for the 33 percent of 46 respondents with operational lives of ten years or more, and what maintenance a window beyond Yocto's four years involves before the project commits to it.
- What support covers, and for which boards.
- How end of support is announced, and how much notice adopters get.
- What evidence of testing each SGL LTS release carries, and how it is kept for the release's support window, so adopters, including those who certify products, can use it.

My view is that SGL LTS releases should track Yocto LTS releases, as meta-sgl has done since its first pull request. It is a view to start the discussion; the recommendation is the WG's.

### Starting points

These exist today. They are starting points for the WG, not a shortlist:

- meta-sgl builds Scarthgap images for three QEMU machines (qemuarm64, qemuriscv64, qemux86-64) and two boards (BeagleV-Fire, PIC64-HPSC), has a Wrynose kas configuration and `layer.conf` compatibility, and uploads build artifacts from CI.
- Yocto Project LTS releases, which SGL already tracks.
- CIP SLTS kernels, maintained for ten years or more.
- [kas][kas], which meta-sgl uses for layer management, and whose lockfiles pin every layer to a commit.

### Constraints

- Charter section 2.g.vi lists among the TSC's responsibilities "establishing community norms, workflows, issuing releases, and security issue reporting policies". The policy comes to the TSC for approval under that section.
- The TSC creates working groups under charter section 2.g.iv.
- Yocto's upstream support for an LTS series ends after four years.

## Scope and non-goals

In scope:

- An SGL long-term support policy: what an SGL LTS release is, its cadence, its support window, what support covers, and how end of support is announced.
- Release engineering for SGL LTS releases, each made under a long-term support policy approved by the TSC under charter section 2.g.vi.
- Keeping the evidence of testing that the policy requires for each SGL LTS release, for the release's support window.

Non-goals:

- Setting the policy's answers in this RFC. The WG recommends them, and they come back to the TSC for approval under charter section 2.g.vi.
- Certification of SGL or of products built on it.
- How the work described here is resourced is outside this RFC.

## Working group

**Name:** LTS and Release Engineering WG, created by the TSC under charter section 2.g.iv.

**Charter:** The LTS and Release Engineering WG exists so that adopters can rely on a defined SGL long-term support release. It brings the TSC a recommendation for an SGL long-term support policy that meets the requirements in this RFC, and it runs SGL LTS releases under a long-term support policy approved by the TSC. It reports to the TSC.

**Cadence:** set by the WG at its first meeting.

**Chair:** to be elected by the working group at its first meeting, confirmed by the TSC.

### Deliverables and timeline (proposed)

Deliverables:

- A recommendation to the TSC on an SGL long-term support policy that addresses every item under Requirements.
- SGL LTS releases, each made under a long-term support policy approved by the TSC.

The working group defines its own timeline. It holds its first meeting in the first quarter of 2027, elects its chair and publishes a quarterly plan; each quarter it reports progress to the TSC and publishes the next quarter's plan.

## Decision requested

The TSC decides by consensus, or by a vote under charter section 3.

1. Charter the LTS and Release Engineering WG under charter section 2.g.iv.
2. Ask the LTS and Release Engineering WG to recommend an SGL long-term support policy to the TSC: what an SGL LTS release is, its cadence, and its support window. The TSC approves the policy under charter section 2.g.vi.

## References

Project and governance:

- [Space Grade Linux Technical Charter][charter], sections 2.g.iv, 2.g.vi and 3.
- [meta-sgl][meta-sgl]

Project meeting minutes:

- [May 15, 2025][m-20250515]: first meta-sgl pull request; build observability roadmap item
- [June 19, 2025][m-20250619]: footprint rationale
- [April 16, 2026][m-20260416]: roadmap feedback summary
- [May 21, 2026][m-20260521]: CNES KOSMOS talk; meta-sgl PR #45 and PR #56
- [July 23, 2026][m-20260723]: Wrynose
- [August 20, 2026][m-20260820]: Wrynose CI action item

Mailing list:

- [List message #173][msg-173], project roadmap, April 2, 2026

Survey:

- SGL Interest Survey, 46 responses, September 2024 to January 2026.

External:

- [Civil Infrastructure Platform][cip]
- [Yocto Project][yocto]
- [kas][kas]

[charter]: ../CHARTER.md
[meta-sgl]: https://github.com/elisa-tech/meta-sgl
[m-20250515]: ../meeting-minutes/project/ELISA-SGLSIG-Meeting-20250515.md
[m-20250619]: ../meeting-minutes/project/ELISA-SGLSIG-Meeting-20250619.md
[m-20260416]: ../meeting-minutes/project/ELISA-SGLSIG-20260416.md
[m-20260521]: ../meeting-minutes/project/ELISA-SGLSIG-20260521.md
[m-20260723]: ../meeting-minutes/project/ELISA-SGLSIG-20260723.md
[m-20260820]: ../meeting-minutes/project/ELISA-SGLSIG-20260820.md
[msg-173]: https://lists.elisa.tech/g/space-grade-linux/message/173
[cip]: https://www.cip-project.org/
[yocto]: https://www.yoctoproject.org/
[kas]: https://kas.readthedocs.io/
