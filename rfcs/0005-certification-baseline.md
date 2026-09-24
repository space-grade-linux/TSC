---
# SPDX-License-Identifier: CC-BY-4.0
rfc: 0005
title: Certification baseline for downstream adopters
status: Draft
authors: ["Ramón Roche (mrpollo, Linux Foundation / Dronecode Foundation)"]
created: 2026-09-23
discussion: pending
supersedes: null
license: CC-BY-4.0
---

# RFC-0005: Certification baseline for downstream adopters

## Summary

Organizations that build Linux systems for space keep asking how a Linux-based system should be approached under the ECSS software standards their programs must meet ([list #181][l181], [April 16, 2026 minutes][m0416]), and an ESA engineer notes that ECSS compliance for Linux has not been discussed in detail ([list #184][l184]). Space Grade Linux (SGL) has not defined what it provides to adopters who certify products built on it, which standards it addresses, or its position on certification of the distribution itself. The goal of this RFC is that adopters who certify products built on SGL get what they need from the project. I ask the Technical Steering Committee (TSC) to charter an Assurance and Certification WG under charter section 2.g.iv and to ask it for a recommendation on those three points, which comes back to the TSC for decision.

## Motivation

### Adopters keep asking for certification guidance

- **KP Labs**, April 10, 2026: they build Zynq UltraScale+ and Versal on-board computers running Yocto Linux, one product at TRL 9, and in ESA projects "compliance with ECSS-E-ST-40 and ECSS-Q-ST-80 standards is still often required. At present, there is a lack of clear guidance on how Linux-based systems should be approached within the context of these standards." The message also notes that ESA's draft Technology Harmonisation Dossier on On-Board Software references ELISA ([list #181][l181]).
- **An ESA engineer** (ESTEC), April 12, 2026: ECSS compliance for Linux has not been discussed in detail; the ECSS software standards are "quite similar to DO-178, particularly regarding quality aspects"; ESA representatives take part in the ELISA working group ([list #184][l184]).
- **A list participant**: it has been hard to get organizations that flew Linux to report what they changed, and those lessons learned would "inform the design choices for the SGL Linux" ([list #186][l186]).
- **Roadmap feedback** on the roadmap posted for comment on April 2, 2026 ([list #173][l173]): "ECSS compliance guidance: multiple organizations flagged the lack of clear guidance on how Linux-based systems should be approached within ECSS standards" ([April 16, 2026 minutes][m0416]).
- **KP Labs talk**, "Linux-Based Systems for Space & ECSS Compliance", a guest presentation at the June 18, 2026 project meeting. The minutes tie the talk to the ECSS compliance guidance theme from the roadmap feedback ([June 18, 2026 minutes][m0618]).
- **CNES**: KOSMOS, the CNES generic flight software framework, is "ECSS-B qualified", and step 1 of the CNES plan is a Yocto-based Linux partition inside it, "relying on poky, and potentially SGL". CNES also asked: "Are there NASA/ESA initiatives on Linux-for-space standards?" ([May 21, 2026 minutes][m0521]).
- **Tuxera**, July 23, 2026: "What assurance artifacts would help integrate SGL with mission criticality or safety certification requirements?" ([July 23, 2026 minutes][m0723]).
- **The project formation discussion**, October 16, 2025: "What class (A-E) of mission is this targetting?", with a note that some participants work on class A mission issues; "Current meta-sgl seems easier to adopt in cubesats where they don't have the safety and certification constraints"; and "CGL had a spec that vendors certified against. AGL started with an architecture document, then transitioned to a reference distribution" ([October 16, 2025 minutes][m1016]).

### Who needs it, and against which standards

The SGL Interest Survey (46 responses, September 2024 to January 2026) shows who needs this and how wide the standards landscape is. Multi-select questions in the survey do not sum to 100 percent. Of 46 respondents, 63 percent already use Linux for space projects, 22 percent deploy crewed systems and another 22 percent deploy both crewed and uncrewed systems. Of 46 respondents, 35 percent already use a hypervisor. Asked which standards they must conform with, of 46 respondents:

| Standard | Share of 46 respondents |
| --- | ---: |
| POSIX | 65% |
| DO-178 | 28% |
| NASA-STD-8739.8 | 20% |
| NASA-STD-8719.13 (one respondent notes it is cancelled but still used by legacy programs) | 20% |
| ISO 26262 | 20% |
| ARINC 653 | 15% |
| MIL-STD-882E | 13% |
| NIST 800 series | 13% |
| NPR 8705.4A | 11% |

Write-ins add ECSS-E-ST-40C and ECSS-Q-ST-80C, NPR 7150.2, DO-330 and SSC 91-710. ECSS was not a listed option and appears only as write-ins, while the stated demand for ECSS guidance on the list and in project meetings came from KP Labs ([list #181][l181]), ESA ([list #184][l184]) and CNES ([May 21, 2026 minutes][m0521]). Stated rigor levels run from ECSS criticality categories B and C, NASA classes A through D and DO-178C DAL A through E, to ASIL B through D from automotive respondents. "Safety Certification" and "Qualification and Certification" appear as write-in interest areas.

Closing comments say what respondents need. One asks: "How to certify LINUX based OS for a human flight?" Another lists "a set of verifiable requirements for Linux", "Tests and evidence of meeting requirements and functionality", "Protection from Common-Cause failures", and "Awareness of contributors and IP rights, and ITAR/EAR Laws". A third warns that "Work done to satisfy lesser degrees of rigor is not as broadly useful as work done to satisfy the greatest degree of required rigor".

### Why now

The asks on the list and in project meetings above are specific and recent, from October 2025 to July 2026. They come from a space company, space agencies, organizations that commented on the roadmap, a storage vendor, a list participant and the project's own discussion, and the survey's closing comments ask the same. The project has not answered them yet: it has not defined what it provides to adopters who certify, which standards it addresses, or its position on certification of the distribution itself.

## Proposal

### Goal

Adopters who certify products built on SGL get what they need from the project. This RFC does not decide what that is. It sets the requirements the Assurance and Certification WG's recommendation must meet, and the TSC decides on the recommendation.

### My view

My view is that no open source community can certify a distribution for a mission; what it can do is produce the inputs adopters need. No single legal entity holds the design authority for a mission, and the standards named above (DO-178C, the ECSS and NASA software standards, ISO 26262) certify systems and the process that developed them, not distributions. Adopters who certify need much the same inputs from the Linux side, and today each one builds them alone, so what one program learns stays inside it, the reporting gap a list participant describes ([list #186][l186]). A shared distribution can build those inputs once, in the open. The October 2025 discussion recalled a similar model in CGL: a spec that vendors certified against ([October 16, 2025 minutes][m1016]). This view leads the discussion; it does not bind the WG.

### Starting points

These exist today. They are starting points, not a shortlist.

- **Configuration rationale.** The "Minimal System Layer, stripped down and usable out of the box" roadmap item, "Documenting whats in the build, and why" ([April 16, 2026 minutes][m0416]). The June 19, 2025 project meeting asked to "Document why we are making the decision for this footprint" ([June 19, 2025 minutes][m0619]). CNES asked for a "Minimal Yocto distribution definition" ([May 21, 2026 minutes][m0521]). Kernel configuration is an interest area for 85 percent of 46 respondents.
- **Build observability.** The May 15, 2025 project meeting recorded "We need observability into what makes to each build, licenses, and all" ([May 15, 2025 minutes][m0515]). Only 41 percent of 46 respondents used an SBOM when they answered the survey.
- **Process.** New code contributions must carry a Developer Certificate of Origin sign-off (charter section 7.b.ii), and [meta-sgl][meta-sgl] pull requests and their review are public on GitHub.
- **ELISA.** The ELISA white paper [Discovering Linux kernel subsystems used by a workload][elisa-wp] and [kernel workload tracing][wltrace], both named with the Minimal System Layer item; the ELISA Aerospace WG's minimal practice activity ([April 16, 2026 minutes][m0416]); and the Boeing and AMD talk on Xen functional safety, covering aerospace, mixed criticality and mixed function, at the ELISA workshop in London, June 9 to 11, 2026 ([June 18, 2026 minutes][m0618]). ESA representatives take part in the [ELISA][elisa] working group ([list #184][l184]).

### Constraints

- Documentation the project publishes is licensed CC-BY-4.0 (charter section 7.b.iv).
- ECSS standards are free to obtain ([ECSS][ecss]). DO-178C and DO-330 are paid documents, so participants who work from them need copies licensed for that use under the publisher's terms.

### Requirements on the recommendation

The recommendation must address:

- **What the project provides** to adopters who certify products built on SGL. Examples to consider, not a list to adopt: configuration rationale, traceability from source to binary, test evidence, process evidence, and mappings to standards.
- **Which standards to address first**, and at which rigor levels. The stated demand for ECSS came from KP Labs ([list #181][l181]), ESA ([list #184][l184]) and CNES ([May 21, 2026 minutes][m0521]); among the survey's listed options, 28 percent of 46 respondents must conform with DO-178, and 20 percent each with NASA-STD-8739.8, NASA-STD-8719.13 and ISO 26262. This RFC sets no order. The recommendation must also address how work for one standard carries over to others, given ESA's remark that the ECSS software standards are "quite similar to DO-178, particularly regarding quality aspects".
- **The project's position on certification of the distribution itself**, including what the project says, and does not say, about SGL and any standard.
- **How the work uses ELISA's methods and material**, such as the ELISA items in Starting points, including whether the project needs a safety manual as ELISA defines it.
- **Safety profiles**: whether SGL defines safety profiles, and what a safety profile covers.
- **Whether to run a worked example** with a downstream adopter, and with whom.
- **Partitioned systems**: what an adopter who runs SGL as one partition of a partitioned system gets from the project, as in the CNES plan ([May 21, 2026 minutes][m0521]).
- **Contributor provenance**: what the project documents about who contributed what, for programs with IP and export control constraints.
- **Lessons learned**: how the project gathers and shares what organizations that flew Linux changed ([list #186][l186]).
- **Producing and keeping it current**: how the project produces and maintains in the open what it provides, which SGL releases each part covers, and how each part stays current as SGL changes.

## Scope and non-goals

In scope:

- The Assurance and Certification WG's recommendation on what the project provides to adopters who certify products built on SGL, which standards to address first, and the project's position on certification of the distribution itself.

Non-goals:

- Deciding those three points in this RFC. The WG recommends; the TSC decides.
- Acting as design authority for any mission.
- Legal advice on export control.
- How this work is resourced is outside this RFC.

## Working group

**Name:** Assurance and Certification WG, created by the TSC under Technical Charter section 2.g.iv.

**Charter:** The Assurance and Certification WG works so that adopters who certify products built on SGL get what they need from the project. It starts from the evidence in this RFC and brings the TSC a recommendation that meets the requirements in the Proposal.

**Cadence:** set by the WG at its first meeting.

**Chair:** to be elected by the working group at its first meeting, confirmed by the TSC.

### Deliverables and timeline (proposed)

- A recommendation to the TSC on what the project provides to adopters who certify products built on SGL, which standards to address first, and the project's position on certification of the distribution itself.

The working group defines its own timeline. It holds its first meeting in the first quarter of 2027, elects its chair and publishes a quarterly plan; each quarter it reports progress to the TSC and publishes the next quarter's plan.

## Decision requested

The TSC decides by consensus, or by a vote under charter section 3.

1. Charter the Assurance and Certification WG under charter section 2.g.iv.
2. Ask the Assurance and Certification WG to recommend to the TSC what the project provides to adopters who certify products built on SGL, which standards to address first, and the project's position on certification of the distribution itself.

## References

Project and governance:

- Space Grade Linux Technical Charter, sections 2.g.iv, 3 and 7.
- meta-sgl: [github.com/elisa-tech/meta-sgl][meta-sgl]

Survey:

- SGL Interest Survey, 46 responses, September 2024 to January 2026.

Project meeting minutes:

- [May 15, 2025][m0515]: build observability
- [June 19, 2025][m0619]: footprint rationale
- [October 16, 2025][m1016]: project formation discussion
- [April 16, 2026][m0416]: roadmap feedback, Minimal System Layer, ELISA Aerospace WG minimal practice activity
- [May 21, 2026][m0521]: CNES KOSMOS talk
- [June 18, 2026][m0618]: KP Labs ECSS talk and ELISA workshop recap
- [July 23, 2026][m0723]: Tuxera talk

Mailing list:

- [#173][l173]: roadmap posted for comment, April 2, 2026
- [#181][l181]: KP Labs on ECSS and Linux, April 10, 2026
- [#184][l184]: ESA on ECSS and DO-178, April 12, 2026
- [#186][l186]: flight lessons learned

External:

- [ELISA][elisa]
- [ELISA white paper, Discovering Linux kernel subsystems used by a workload][elisa-wp]
- [Linux kernel workload tracing][wltrace]
- [ECSS][ecss]

[m0515]: ../meeting-minutes/project/ELISA-SGLSIG-Meeting-20250515.md
[m0619]: ../meeting-minutes/project/ELISA-SGLSIG-Meeting-20250619.md
[m1016]: ../meeting-minutes/project/ELISA-SGLSIG-Meeting-20251016.md
[m0416]: ../meeting-minutes/project/ELISA-SGLSIG-20260416.md
[m0521]: ../meeting-minutes/project/ELISA-SGLSIG-20260521.md
[m0618]: ../meeting-minutes/project/ELISA-SGLSIG-20260618.md
[m0723]: ../meeting-minutes/project/ELISA-SGLSIG-20260723.md
[l173]: https://lists.elisa.tech/g/space-grade-linux/message/173
[l181]: https://lists.elisa.tech/g/space-grade-linux/message/181
[l184]: https://lists.elisa.tech/g/space-grade-linux/message/184
[l186]: https://lists.elisa.tech/g/space-grade-linux/message/186
[meta-sgl]: https://github.com/elisa-tech/meta-sgl
[elisa]: https://elisa.tech/
[elisa-wp]: https://github.com/elisa-tech/ELISA-White-Papers/blob/master/Processes/Discovering_Linux_kernel_subsystems_used_by_a_workload.md
[wltrace]: https://www.kernel.org/doc/html/v6.9/admin-guide/workload-tracing.html
[ecss]: https://ecss.nl/
