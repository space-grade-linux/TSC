---
# SPDX-License-Identifier: CC-BY-4.0
rfc: 0002
title: Radiation fault injection in CI
status: Draft
authors: ["Ramón Roche (mrpollo, Linux Foundation / Dronecode Foundation)"]
created: 2026-09-23
discussion: https://github.com/space-grade-linux/TSC/pull/2
supersedes: null
license: CC-BY-4.0
---

# RFC-0002: Radiation fault injection in CI

## Summary

SGL CI builds images for three QEMU machines and two boards (BeagleV-Fire and Microchip PIC64-HPSC), and it injects no faults into any of them. Several research groups, and EPAM on the QEMU development list, have built fault injectors independently, and several project participants offered to help bring fault injection into SGL. I propose that the CI Testing WG take on fault injection for SGL: evaluate what exists, decide how to judge it, and recommend to the Technical Steering Committee (TSC) how SGL CI runs fault injection, including whether to adopt one tool, with its authors' agreement, as an open source project hosted by Space Grade Linux. I ask the TSC to charter the CI Testing WG for this work and to ask it for that recommendation.

## Motivation

### Three groups built radiation fault models, and none of them runs in SGL CI

Three research groups independently built radiation fault models and tools, and all three presented them at project meetings.

**Columbia University, with NASA JPL and Aptos Orbital: Radshield.** The Columbia University Radshield team presented its work at the [January 15, 2026 meeting][m-20260115]. The work is published at ASPLOS 2026 as [Radshield: Software Radiation Protection for Commodity Hardware in Space][radshield-paper] ([project site][radshield-site]). The Idle Latchup Detector finds single-event latchups from OS performance counters, with 0 percent false negatives and 0.02 percent false positives over 960 hours, and Efficient Modular Redundancy protects against single-event upsets at 1.4 to 35.5x the power efficiency of triple modular redundancy. The group's QEMU fault injector is [qemu-hce][qemu-hce], a QEMU fork with cache-aware fault injection. The minutes record that the team's presenter agreed to help integrate Radshield's QEMU-based fault injection tooling with SGL CI infrastructure. On the roadmap thread started by [message #173][msg-173], the team wrote on April 3, 2026 that they are making the QEMU system run headlessly, that it can target faults in DRAM and multi-level caches, that fault frequencies are hard-coded for now, and that they want input on which metrics to collect.

**University of Luxembourg, SnT (Interdisciplinary Centre for Security, Reliability and Trust).** A University of Luxembourg SnT researcher presented Linux boot failures measured under radiation on an NXP i.MX 8M module at the [September 18, 2025 meeting][m-20250918]. Failures traced back to firmware, the device tree, the early kernel (ECC was not yet initialized, so memory errors in that phase bled into later ones) and cascading ext4 errors that ended with the filesystem failing to mount. Existing QEMU plugins did not give the control needed, so the group is writing a plugin that controls where bit flips land, using a "hit map" of places to target. Updated slides were posted to the list on May 4, 2026. The same group's cross-architecture characterization of radiation-induced kernel failures is [arXiv:2503.03722][arxiv-snt].

**BYU SHREC (NSF Center for Space, High-performance, and Resilient Computing at Brigham Young University).** The group's project sheet, [SHREC B1-25 "Fault-Tolerant Techniques for Heterogeneous Computing Architectures"][shrec-b1-25], was discussed at the [July 17, 2025 meeting][m-20250717]. BYU SHREC presented radiation test results on AMD Versal running Linux at the [August 21, 2025 meeting][m-20250821]: cache ECC and scrubbing corrected many errors, the dominant failures were processor hangs that are hard to diagnose, and Linux reported OCM errors without correcting them until the group patched the EDAC driver. The project sheet also covers hardware fault injection on Versal (a "Versal FI kernel"), and the group shared [soft-core fault injection work][byu-etd] at the September 18 meeting. It is the one group of the three injecting faults on real silicon rather than in a simulator.

The September 18 discussion also pointed at MIT's "Hailburst" QEMU fault injection work ([thesis][hailburst-thesis], [code][hailburst-code]). That makes four independently built QEMU fault injectors known to the project: qemu-hce, the SnT plugin in development, Hailburst, and the EPAM TCG plugin described below.

Left alone, these stay separate tools with separate result formats, and SGL CI runs none of them. At the [September 18, 2025 meeting][m-20250918] the project said it was working on setting up CI with QEMU and fault injection; a year later, meta-sgl CI still only builds. People have offered to do the work: the [April 16, 2026 minutes][m-20260416] summarize the roadmap feedback as "QEMU fault injection: strong interest, contributors willing to commit time". A list participant wrote that they are "very interested" and "might be willing to commit some time", and that they are also interested in EDAC/ECC profiles ([message #175][msg-175]). A participant from Space Cubics replied on the [roadmap thread][msg-173] on April 12, 2026 that they are "very interested", can commit time, and plan to release an FPGA-based EDAC/ECC memory scrubbing implementation. The [April 2, 2026 minutes][m-20260402] asked for people to join "a dedicated working session or alternate group call to move this forward". No later minutes record that session. This RFC asks the TSC to charter a working group to be that call.

### An upstream-shaped injector exists

On March 18, 2026 EPAM posted a QEMU fault injection framework RFC to qemu-devel ([patch series][epam-patchew]). It extends the TCG plugin API and adds `contrib/plugins/fault_injection.c` for AArch64, with MMIO interception, IRQ and exception injection, timers, and control through an XML config or a runtime UNIX socket. A list participant forwarded it to the SGL and Aerospace lists from the Xen FuSa call ([aerospace message #344][aero-344]). Unlike the QEMU forks, it is shaped to land in QEMU itself.

### Research tools need a maintained home

My view is that research tools often have no long-term home. Hailburst, whose code was last pushed in August 2022, is one example. Fault injection that SGL relies on across long-lived releases needs a maintained home.

### What the survey says

The figures below come from the SGL Interest Survey, 46 responses, September 2024 to January 2026. The questions are multi-select, so percentages do not sum to 100 percent.

- Of 46 respondents, 24 (52 percent), a majority, are interested in "Emulation/Simulation of effects based on the real OS (probably in a VM)". Write-ins to the same question add "SEU handling, mitigations" and "radiation effects mitigation".
- Radiation hardening items marked important, of 46 respondents: ECC and patrol scrubbing 57 percent, hardware watchdog 54 percent, writeable mass storage 39 percent, redundant hardware 37 percent, static read-only system 35 percent, power-cycle mitigation 35 percent, TMR boot 33 percent, RAM-based filesystem 30 percent. Memory faults are what qemu-hce and BYU SHREC's ECC and scrubbing results cover, and booting in a radiation environment (TMR boot, 15 of 46) is what the SnT boot failure work covers.
- QEMU is in use or planned by 22 of 46 respondents (48 percent). ARM is needed by 38 of 46 (83 percent), and RISC-V by 16 of 46 (35 percent).

One respondent summed up the status quo in their answer on assurance levels: "Let's test it in orbit, can't really do that in lab". Fault injection in CI moves part of that into the lab.

## Proposal

### The goal

Fault injection runs as part of SGL CI, against the images SGL CI builds, and its results are published for each release so adopters, including those who certify products, can use them.

As a starting point, I propose that the working group pick one existing tool, run a small, repeatable fault injection experiment against an SGL image in CI, publish what it finds, and grow from there. The working group may take a different path.

### Starting points, not a shortlist

These are what the project already knows about. They are starting points for the working group's evaluation, not a shortlist. The evaluation is not limited to them.

- [qemu-hce][qemu-hce], the Columbia University Radshield team's QEMU fork with cache-aware fault injection of DRAM and multi-level caches.
- The University of Luxembourg SnT plugin, in development and not yet published, which aims to control where bit flips land, with a planned hit map of places to target, and to reproduce boot failures.
- The EPAM QEMU plugin series ([patch series][epam-patchew]), which targets QEMU's `contrib/plugins` for AArch64.
- Hailburst ([code][hailburst-code]), the QEMU fork from an MIT thesis.
- [Renode][renode], a separate simulator.
- BYU SHREC's hardware fault injection on AMD Versal.

In [meta-sgl][meta-sgl], CI uploads its build artifacts (PR #45, merged per the [May 21, 2026 minutes][m-20260521]), and a draft pull request adds an sgl-telemetry-collect script for EDAC and system data (PR #44, listed in the same minutes).

### Constraints

These are facts from the charter and from the licenses of the starting points, and the requirements any adoption must meet:

- The Project License is MIT (charter section 7.b.i).
- QEMU as a whole is GPL-2.0 ([QEMU license][qemu-license]), and plugins in QEMU's own tree are "GNU GPL, version 2 or later". qemu-hce and Hailburst are QEMU forks, and the EPAM series targets QEMU's `contrib/plugins`.
- Contributions to upstream projects follow the upstream project's license (charter section 7.b.v).
- Copyright stays with its holders, and no contributor is required to assign it (charter section 7.a).
- The project develops and owns its GitHub accounts (charter section 5.b).
- Adopting a tool requires the agreement of its authors, a separate TSC decision under charter section 2.g.ii, and, for a license other than MIT, a license exception under charter section 7.c, which needs a two-thirds vote of the entire TSC.

### What the recommendation must address

The recommendation to the TSC must address:

- which fault models matter most to SGL users, and where faults are injected: in emulation, on hardware, or both (the survey points at memory faults with ECC and scrubbing, watchdog recovery, and boot);
- how the tools are judged;
- whether the project adopts one tool as an open source project hosted by Space Grade Linux, in a GitHub organization the project owns (charter section 5.b), with its authors' agreement and with copyright staying with its holders (charter section 7.a);
- the license path for any tool the project hosts, within the constraints above;
- how the work relates to upstream QEMU, including whether and for how long SGL CI runs QEMU forks;
- how and when fault injection runs in SGL CI, and who maintains the jobs and the tools they depend on;
- what a result contains, including which metrics are collected (the Radshield team asked for input on exactly this on the [roadmap thread][msg-173]);
- how results are published and kept so adopters can rely on them over a release's life.

## Scope and non-goals

In scope:

- Fault injection in SGL CI, against SGL images.
- The evaluation of existing fault injection tools, and the recommendation to the TSC, including whether to adopt a tool.
- Published fault injection results for each SGL release.

Out of scope:

- Adopting a tool without its authors' agreement.
- Copyright assignment.
- Physical radiation testing. The project does not irradiate hardware.
- Radiation mitigations themselves (EDAC drivers, scrubbing, ECC bring-up, TMR). This work makes them testable.
- Certifying SGL, and deciding what evidence a standard requires.
- How this work is resourced is outside this RFC.

## Working group

The CI Testing WG owns automated testing of SGL beyond the build.

**Name:** CI Testing WG.

**Charter:** The WG brings fault injection into SGL CI. It evaluates the existing fault injection tools, recommends to the TSC how SGL CI runs fault injection, runs it in SGL CI and publishes the results for each release. The WG is created under charter section 2.g.iv and reports to the TSC.

**Cadence:** set by the WG at its first meeting.

**Chair:** to be elected by the working group at its first meeting, confirmed by the TSC.

### Deliverables and timeline (proposed)

- A recommendation to the TSC on fault injection in SGL CI, including whether to adopt a tool as an open source project hosted by Space Grade Linux.
- Fault injection running in SGL CI.
- Published fault injection results for each SGL release.

The working group defines its own timeline. It holds its first meeting in the first quarter of 2027, elects its chair and publishes a quarterly plan; each quarter it reports progress to the TSC and publishes the next quarter's plan.

## Decision requested

The TSC decides by consensus, or by a vote under charter section 3.

1. Charter the CI Testing WG under charter section 2.g.iv to bring fault injection into SGL CI.
2. Ask the CI Testing WG to evaluate existing fault injection tools and recommend to the TSC how SGL CI runs fault injection, including whether to adopt a tool as an open source project hosted by Space Grade Linux. Adopting a tool, and any license exception under charter section 7.c, requires a separate TSC decision.

## References

Project and governance:

- Space Grade Linux Technical Charter, sections 2.g.ii, 2.g.iv, 3, 5.b, 7.a, 7.b.i, 7.b.v and 7.c.

Survey:

- SGL Interest Survey, 46 responses, September 2024 to January 2026.

Project meeting minutes:

- [July 17, 2025][m-20250717]: BYU SHREC project sheet
- [August 21, 2025][m-20250821]: BYU SHREC, Versal radiation test results
- [September 18, 2025][m-20250918]: SnT, Linux boot failures under radiation; Hailburst; CI with QEMU and fault injection; BYU soft-core fault injection
- [January 15, 2026][m-20260115]: Radshield (Columbia University)
- [April 2, 2026][m-20260402]: request for a fault injection working session
- [April 16, 2026][m-20260416]: roadmap feedback summary
- [May 21, 2026][m-20260521]: meta-sgl PR #44 (sgl-telemetry-collect) and PR #45 (artifact upload)

Mailing list:

- Replies on the thread started by list [message #173][msg-173]: Radshield QEMU fault injection status (April 3, 2026) and Space Cubics FPGA-based EDAC/ECC scrubbing (April 12, 2026)
- SnT, updated boot failure slides posted to the list on May 4, 2026
- [Message #175][msg-175], QEMU fault injection and EDAC/ECC profiles
- [EPAM QEMU fault injection RFC, forwarded to the Aerospace list, message #344][aero-344]

Research and tools:

- [Radshield: Software Radiation Protection for Commodity Hardware in Space, ASPLOS 2026][radshield-paper]; [project site][radshield-site]; [qemu-hce][qemu-hce]
- [Where Linux Breaks Under Radiation, arXiv:2503.03722][arxiv-snt]
- [SHREC B1-25, Fault-Tolerant Techniques for Heterogeneous Computing Architectures][shrec-b1-25]; [BYU soft-core fault injection][byu-etd]
- [QEMU fault injection framework patch series (EPAM)][epam-patchew]
- [Hailburst thesis (MIT, 2022)][hailburst-thesis]; [code][hailburst-code]
- [Renode][renode]
- [QEMU license][qemu-license]

[m-20250717]: ../meeting-minutes/project/ELISA-SGLSIG-Meeting-20250717.md
[m-20250821]: ../meeting-minutes/project/ELISA-SGLSIG-Meeting-20250821.md
[m-20250918]: ../meeting-minutes/project/ELISA-SGLSIG-Meeting-20250918.md
[m-20260115]: ../meeting-minutes/project/ELISA-SGLSIG-20260115.md
[m-20260402]: ../meeting-minutes/project/ELISA-SGLSIG-20260402.md
[m-20260416]: ../meeting-minutes/project/ELISA-SGLSIG-20260416.md
[m-20260521]: ../meeting-minutes/project/ELISA-SGLSIG-20260521.md
[msg-173]: https://lists.elisa.tech/g/space-grade-linux/message/173
[msg-175]: https://lists.elisa.tech/g/space-grade-linux/message/175
[aero-344]: https://lists.elisa.tech/g/aerospace/message/344
[radshield-paper]: https://dl.acm.org/doi/10.1145/3760250.3762218
[radshield-site]: https://radshield.github.io/
[qemu-hce]: https://github.com/radshield/qemu-hce
[arxiv-snt]: https://arxiv.org/abs/2503.03722
[shrec-b1-25]: https://www.nsf-shrec.org/sites/default/files/2025/B1-25.pdf
[byu-etd]: https://scholarsarchive.byu.edu/etd/10892/
[epam-patchew]: https://patchew.org/QEMU/20260318104640.239752-1-ruslichenko.r@gmail.com/
[hailburst-thesis]: https://dspace.mit.edu/bitstream/handle/1721.1/144731/Skeggs-cela-meng-eecs-2022-thesis.pdf
[hailburst-code]: https://github.com/celskeggs/qemu
[renode]: https://renode.io
[qemu-license]: https://gitlab.com/qemu-project/qemu/-/blob/master/LICENSE
[meta-sgl]: https://github.com/elisa-tech/meta-sgl
