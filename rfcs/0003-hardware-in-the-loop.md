---
# SPDX-License-Identifier: CC-BY-4.0
rfc: 0003
title: Hardware-in-the-loop testing in CI
status: Draft
authors: ["Ramón Roche (mrpollo, Linux Foundation / Dronecode Foundation)"]
created: 2026-09-23
discussion: pending
supersedes: null
license: CC-BY-4.0
---

# RFC-0003: Hardware-in-the-loop testing in CI

## Summary

SGL CI today builds images for three QEMU machines and two boards (BeagleV-Fire and Microchip PIC64-HPSC, both RISC-V), but it boots nothing on hardware. Failures seen on real boards in radiation testing, and the questions raised about power interruption and watchdog recovery, need real boards to reproduce and regression-test. I propose that SGL images boot and are tested on real boards as part of SGL CI, and that the CI Testing WG own that work. I ask the Technical Steering Committee (TSC) to charter the CI Testing WG for hardware-in-the-loop testing, and to ask it for a recommendation covering at least the boards, where they are hosted, and how access works.

## Motivation

### "CI all the way to hardware" has no owner

- CI in [meta-sgl][meta-sgl] is build-only today. The reusable `build-sgl.yml` workflow and a `test_build_*` workflow per target build images for `qemuarm64`, `qemuriscv64`, `qemux86-64`, `beaglev-fire` and `pic64hpsc`, and meta-sgl PR #45 uploads the build artifacts (merged, per the [May 21, 2026 minutes][m-20260521]). Nothing boots those artifacts on a board.
- "CI all the way to hardware" entered the roadmap proposals at the [April 16, 2026 meeting][m-20260416], with the aim of verifying that builds run on hardware. The April 16, [June 18][m-20260618], [July 23][m-20260723] and [August 20][m-20260820] minutes carry it as the action item "Roadmap: define plan for CI all the way to hardware (verify builds run on target)" with no name attached, and the [May 21][m-20260521] review lists "CI-to-hardware plan" with the note "owner?". sig-sgl [issue #8][issue-8] has listed "Test on Hardware / Hardware Deployments" since June 2025.
- The [October 16, 2025 minutes][m-20251016] ask whether to target specific hardware, such as the HPSC or existing cubesat kits, and record that a testing solution, for example for EDAC, would be valuable.

### Failures seen on real boards

Two research groups that presented at project meetings, BYU SHREC and SnT, reported radiation test results from real boards. Several of the failures involve parts of the system that QEMU does not model faithfully.

- On AMD Versal running Linux, BYU SHREC saw cache ECC and scrubbing correct many errors, but still saw processor hangs that are hard to diagnose, and Linux reported OCM errors without correcting them until the group patched the EDAC driver ([August 21, 2025][m-20250821]).
- On an NXP i.MX 8M module, SnT traced boot failures to firmware, the device tree and the early kernel before ECC was initialized, and tracked some ext4 errors down to the controller, ending with a filesystem that failed to mount ([September 18, 2025][m-20250918]).

Reproducing and regression-testing these paths (firmware and the device tree on a specific board, the memory controller and the EDAC driver, a storage controller) needs boards.

### Boards and demand

- PIC64-HPSC machine support landed in [meta-sgl][meta-sgl] on August 14, 2026 (commit 8bae619). Evaluation boards exist, and none is in CI.
- BeagleV-Fire is the current low-cost dev board, and CI builds a Space ROS image for it (meta-sgl PR #29, [February 19, 2026 minutes][m-20260219]).
- The roadmap feedback summary in the [April 16, 2026 minutes][m-20260416] records "demand for Zynq7000, UltraScale+, and Versal targets". The ELISA Aerospace WG requested the [June 18, 2026][m-20260618] agenda item on "SGL hardware targets and adding an AeroWG cFS demo build".
- A participant from Space Cubics wrote on April 12, 2026, in a reply on the thread started by [list message #173][msg-173], that the company's Versal-based OBC is too expensive to distribute freely, but that Space Cubics might be able to set up a board for CI testing.

### Power interruption, watchdogs and storage

Tuxera's talk at the [July 23, 2026 meeting][m-20260723] asked "What common use cases would a power-interruption and degraded-media test harness need to cover?" and "What should be guaranteed after a watchdog reset, power fault, or SEU-related restart?". The [August 20, 2026 minutes][m-20260820] carry "Storage and persistence workstream, including a power-interruption test profile (follow-up from the July Tuxera talk)" as a roadmap proposal. Answering either question in CI needs tests on real boards.

### What the survey says

The figures below come from the SGL Interest Survey, 46 responses, September 2024 to January 2026. The questions are multi-select, so percentages do not sum to 100 percent.

- Platforms in use or planned, of 46 respondents: QEMU 48 percent, AMD/Xilinx 46 percent, Raspberry Pi 28 percent, GR740/LEON 17 percent, HPSC 15 percent, BeagleBone 15 percent, Jetson Orin NX 13 percent, other Jetson 13 percent. Write-ins include PolarFire SoC, NXP, STM32, Vorago ARM MCUs, Xiphos Q7S/Q8S and x86-64.
- Architectures, of 46 respondents: ARM 83 percent, 64-bit 65 percent, 32-bit 41 percent, RISC-V 35 percent, Intel 33 percent, PowerPC 13 percent, SPARC 13 percent.
- Radiation hardening items marked important, of 46 respondents, that testing on real boards can exercise: hardware watchdog 25 of 46 (54 percent), writeable mass storage 18 of 46 (39 percent), power-cycle mitigation 16 of 46 (35 percent).

QEMU and AMD/Xilinx are the two largest platform groups (22 and 21 of 46 respondents, 48 and 46 percent). HPSC (7 of 46, 15 percent) has machine support in meta-sgl but no board in CI. Both boards SGL builds for today are RISC-V, while 38 of 46 respondents (83 percent) need ARM.

Asked about assurance levels, one respondent answered "Let's test it in orbit, can't really do that in lab". Another answered "nightly and accelerated testing of core logic". This RFC is about bringing part of that testing into a lab.

## Proposal

### Goal

SGL images boot and are tested on real boards as part of SGL CI.

### Requirements

The outcome must meet these requirements:

- Hardware tests run from SGL CI, against the images it builds.
- No use of the boards blocks upstream SGL work.
- Results are published so adopters, including those who certify products, can use them.

### Starting points

These are starting points, not a shortlist.

- The boards SGL builds for today, BeagleV-Fire and PIC64-HPSC, and the build artifacts SGL CI already uploads.
- A Versal-based board that a participant from Space Cubics said the company might be able to set up for CI testing.
- Prior art in hardware test labs: [LAVA][lava], [Labgrid][labgrid] (from Pengutronix, which was represented at the [October 16, 2025 meeting][m-20251016]), [KernelCI][kernelci]-style labs and the [Yocto Project][yocto]'s own hardware test lab.
- Work already raised at project meetings: the sgl-telemetry-collect script for EDAC and system data (meta-sgl PR #44, a draft in the [May 21, 2026 minutes][m-20260521]), the roadmap proposal to stress and analyze partitions with stress-ng ([April 16, 2026][m-20260416]), and Tuxera's power-interruption questions.

### What the recommendation must address

The recommendation must address:

- which boards are tested, which architectures they cover, and how boards are added or removed;
- where the boards are hosted, and whether at one site or more;
- how hardware tests are scheduled and wired into SGL CI;
- which tests run on hardware, and when;
- how access works, including whether and how others use the boards to test their own layers on SGL, and how upstream SGL work stays unblocked;
- how donated hardware and export-controlled hardware are handled;
- how results are published and kept so adopters can rely on them over a release's life.

### Constraints

- SGL CI builds images for two boards today, BeagleV-Fire and PIC64-HPSC, both RISC-V, and boots none of them.
- The TSC creates working groups under charter section 2.g.iv, and its responsibilities include establishing community norms and workflows under charter section 2.g.vi.

## Scope and non-goals

In scope:

- Hardware-in-the-loop testing of SGL images on real boards, as part of SGL CI.
- The CI Testing WG's recommendation to the TSC, and hardware-in-the-loop testing in SGL CI that meets the requirements in the Proposal.

Out of scope:

- Physical radiation testing.
- Radiation mitigations themselves (EDAC drivers, scrubbing, ECC bring-up, TMR).
- Flight hardware qualification.
- How the boards, their hosting and the work in this RFC are resourced is outside this RFC.

## Working group

The CI Testing WG owns automated testing of SGL beyond the build.

**Name:** CI Testing WG, created by the TSC under Technical Charter section 2.g.iv.

**Charter:** The WG brings hardware-in-the-loop testing into SGL CI, so that SGL images boot and are tested on real boards. It brings the TSC a recommendation that addresses the requirements in the Proposal, delivers hardware-in-the-loop testing that meets those requirements, and reports progress to the TSC.

**Cadence:** set by the WG at its first meeting.

**Chair:** to be elected by the working group at its first meeting, confirmed by the TSC.

### Deliverables and timeline (proposed)

- A recommendation to the TSC on hardware-in-the-loop testing of SGL, addressing the requirements in the Proposal.
- SGL images booting and tested on real boards as part of SGL CI, meeting the requirements in the Proposal.
- Published results.

The working group defines its own timeline. It holds its first meeting in the first quarter of 2027, elects its chair and publishes a quarterly plan; each quarter it reports progress to the TSC and publishes the next quarter's plan.

## Decision requested

The TSC decides by consensus, or by a vote under charter section 3.

1. Charter the CI Testing WG under charter section 2.g.iv to bring hardware-in-the-loop testing into SGL CI.
2. Ask the CI Testing WG to bring the TSC a recommendation for hardware-in-the-loop testing of SGL, covering at least the boards, where they are hosted, and how access works, so that upstream SGL work is never blocked. The recommendation comes back to the TSC for approval.

## References

Project and governance:

- Space Grade Linux Technical Charter, sections 2.g.iv, 2.g.vi and 3.

Survey:

- SGL Interest Survey, 46 responses, September 2024 to January 2026.

Project meeting minutes:

- [August 21, 2025][m-20250821]: BYU SHREC, Linux on AMD Versal and the OCM EDAC patch
- [September 18, 2025][m-20250918]: SnT, Linux boot failures in radiation testing
- [October 16, 2025][m-20251016]: which hardware to target; testing solution for EDAC
- [February 19, 2026][m-20260219]: CI builds Space ROS on BeagleV-Fire
- [April 16, 2026][m-20260416]: roadmap feedback summary (Zynq, UltraScale+, Versal); "CI all the way to hardware"; stress-ng partition item
- [May 21, 2026][m-20260521]: "CI-to-hardware plan", "owner?"; meta-sgl PR #45 merged, PR #44 draft
- [June 18, 2026][m-20260618]: ELISA Aerospace WG cross-over, SGL hardware targets and cFS demo build
- [July 23, 2026][m-20260723]: Tuxera talk, power-interruption and degraded-media test harness
- [August 20, 2026][m-20260820]: storage and persistence workstream proposal; "CI all the way to hardware" action item

Mailing list:

- Reply from a Space Cubics participant, April 12, 2026, on the thread started by [list message #173][msg-173]: a Versal-based board Space Cubics might be able to set up for CI testing

Projects and repositories:

- [meta-sgl][meta-sgl]; [sig-sgl issue #8, Roadmap Issue Discussion][issue-8]
- [KernelCI][kernelci]; [LAVA][lava]; [Labgrid][labgrid]; [Yocto Project][yocto]

[m-20250821]: ../meeting-minutes/project/ELISA-SGLSIG-Meeting-20250821.md
[m-20250918]: ../meeting-minutes/project/ELISA-SGLSIG-Meeting-20250918.md
[m-20251016]: ../meeting-minutes/project/ELISA-SGLSIG-Meeting-20251016.md
[m-20260219]: ../meeting-minutes/project/ELISA-SGLSIG-20260219.md
[m-20260416]: ../meeting-minutes/project/ELISA-SGLSIG-20260416.md
[m-20260521]: ../meeting-minutes/project/ELISA-SGLSIG-20260521.md
[m-20260618]: ../meeting-minutes/project/ELISA-SGLSIG-20260618.md
[m-20260723]: ../meeting-minutes/project/ELISA-SGLSIG-20260723.md
[m-20260820]: ../meeting-minutes/project/ELISA-SGLSIG-20260820.md
[msg-173]: https://lists.elisa.tech/g/space-grade-linux/message/173
[meta-sgl]: https://github.com/elisa-tech/meta-sgl
[issue-8]: https://github.com/elisa-tech/sig-sgl/issues/8
[kernelci]: https://kernelci.org/
[lava]: https://www.lavasoftware.org/
[labgrid]: https://labgrid.readthedocs.io/
[yocto]: https://www.yoctoproject.org/
