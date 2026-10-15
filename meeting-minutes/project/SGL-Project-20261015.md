![logo](logo_elisa_small.png )

## ELISA Space Grade Linux Special Interests Group

The goal of the group is to advance space technology innovation and competitiveness by developing a common Linux distribution that can be used in space applications, ready for the challenges of deep space, often long lifespan robotic or human-based missions. The nature of space missions brings many challenges, from development to deployment there are multiple considerations that need to be considered. Furthermore this group is the initial step towards creating an ecosystem of supported platforms and a community that benefits from them, and also from the open source nature of the project. (https://lists.elisa.tech/g/space-grade-linux/)

# Minutes

## 15 October, 2026

---

# Agenda

- Roll Call
- Brief Notices
- Announcements
  - Upcoming Events
  - Project news
- RFC check-in (five RFCs in Draft)
- Main Topic: Governance review
  - The charter at a glance
  - How the TSC decides
  - Who is on the TSC
  - The TSC Chair and open questions
  - Governing Board and TSC: two bodies, two jobs
- Formation meetings and founding members
- Mailing List Highlights
- Action Items Review
- Open Discussion / AOB
- Closing

---

# Roll Call

## Attended this meeting

- Ramón Roche (Dronecode Foundation)
- Philip Balister (OpenEmbedded)
- Ivan Perez (KBR @ NASA Ames Research Center)
- Rob Woolley (Wind River)
- Geoffrey Biggs (Open Source Robotics Foundation)
- Jameson Beebe
- Piotr Skrzypek (European Space Agency)
- Nicolae Butnari (SES)
- Johan Bertrand (SES)
- Yassine Cherni (GoMyRobot)
- Duc Pham (Tweaklogic)
- Subhajit Ghosh (Tweaklogic)
- Brennan Hay (NASA GSFC)
- Yasushi SHOJI (Space Cubics)
- Alexey Simonov (TII)
- Pedro Roque (Caltech)
- Hans Weggeman (Wind River)
- Nick Zajerko-McKee (Vorago Technologies)
- Leonidas Kosmidis (Barcelona Supercomputing Center)
- Matthias Schmitz

## Attended recently in the past

- Alexey Simonov (TII)
- Brennan Hay (NASA GSFC)
- Brian Kempa
- Christopher Heistand
- Cuauhtemoc Castellanos (SES)
- Cyril Jean (Microchip)
- Dhruv Sharma
- Dongshik Won (TelePIX, KAIST)
- Douglas Landgraf (Red Hat)
- Duc Pham (Tweaklogic)
- Eoin Dickson (Microchip)
- Gabriele Paoloni (Red Hat)
- Gary Crum (Voyager Technologies)
- Geoffrey Biggs (Open Source Robotics Foundation)
- Giacomo Forresu (SES)
- Hans Weggeman (Wind River)
- Haoda Wang "Harry" (Columbia University)
- Hugo Cornelis (Mind OSS)
- Ivan Perez (KBR @ NASA Ames Research Center)
- Ivan Pravdin (NVIDIA)
- Jameson Beebe
- Jan Vermaete
- Jan-Simon Moeller (AGL)
- Joe Speed (Ampere)
- Johan Bertrand (SES)
- Juan Solano
- Kate Stewart (LF)
- Leonidas Kosmidis (Barcelona Supercomputing Center)
- Lukas Mazl (Technical University of Liberec)
- Maciej Nowak (KP Labs)
- Manuel Beltran (Boeing)
- Martin Halle (TUHH)
- Matt Weber (The Boeing Company)
- Matthias Schmitz
- Michael Krasnyk (The Exploration Company)
- Michael Mahoney (Wind River)
- Michael Monaghan (NASA GSFC)
- Michael Starch (JPL)
- Naga (Timesys/Lynx)
- Naoto Yamaguchi (AISIN)
- Nick Zajerko-McKee (Vorago Technologies)
- Nicolae Butnari (SES)
- Panos Kalorog (NRB)
- Paul Greenwood (Vorago Technologies)
- Pawel Wodnicki (32bitmicro)
- Pedro Roque (Caltech)
- Philip Balister (OpenEmbedded)
- Piotr Skrzypek (European Space Agency)
- Rahn Twitchell (Tuxera)
- Ramón Roche (Dronecode Foundation)
- Rob Woolley (Wind River)
- Ryo Takakura
- Sandipan Ghosh (Tweaklogic)
- Shefali Sharma
- Subhajit Ghosh (Tweaklogic)
- Tim Bird (Sony)
- Tony James (Red Hat)
- Tyler Kwolek
- Xavier Scholtes (SES)
- Yassine Cherni (GoMyRobot)
- Yasushi SHOJI (Space Cubics)

---

# Brief Notices

## Code of Conduct and Legal Notices

- ELISA Project meetings involve participation by industry competitors, and it is the intention of the Linux Foundation to conduct all of its activities in accordance with applicable antitrust and competition laws. It is therefore extremely important that attendees adhere to meeting agendas, and be aware of, and not participate in, any activities that are prohibited under applicable US state, federal, or foreign antitrust and competition laws.
  - [Linux Foundation Antitrust Policy](http://www.linuxfoundation.org/antitrust-policy)
- Email communication will be treated as documentation and be received and made available by the Project under the [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0). Please refer to the ELISA Technical Charter section 7 subsection iv. for details.
- The discussions in these meetings are exploratory. The opinions expressed by participants are not necessarily the policy of the companies.
- No recordings of working group meetings are permitted. Special provisions may be arranged for recording in advance with explicit consent of the participants.
- The kernel and LF Code of Conduct applies to all communication with this project
  - [Linux Foundation Code of Conduct](https://www.linuxfoundation.org/code-of-conduct/)
  - Linux [Contributor Covenant Code of Conduct](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/Documentation/process/code-of-conduct.rst)
  - Linux Kernel Contributor Covenant [Code of Conduct Interpretation](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/Documentation/process/code-of-conduct-interpretation.rst)

---

# Announcements

## Upcoming Events

- **Oct 22** Space Grade Linux Fund formation meeting (see below)
- **Dec 7** Full launch and member announcement at Open Source Summit Japan, Tokyo

## Project news

- Founding members signing on to the Space Grade Linux Fund: NEC, Frontgrade Gaisler, SpaceCubics. More conversations are open across the US, Europe and Japan.

---

# RFC check-in

The five RFCs stay open as Draft pull requests until committers weigh in. This is their second project meeting, so the minimum comment period (two project meetings or three weeks) is met after today. The earliest TSC decision is after this meeting.

| RFC | Title | Proposed WG | Discussion |
| --- | --- | --- | --- |
| 0001 | Software-defined vehicle architecture for space systems | SDV for Space Architecture WG | [#1](https://github.com/space-grade-linux/TSC/pull/1) |
| 0002 | Radiation fault injection in CI | CI Testing WG | [#2](https://github.com/space-grade-linux/TSC/pull/2) |
| 0003 | Hardware-in-the-loop testing in CI | CI Testing WG | [#3](https://github.com/space-grade-linux/TSC/pull/3) |
| 0004 | Long-term support releases | LTS and Release Engineering WG | [#4](https://github.com/space-grade-linux/TSC/pull/4) |
| 0005 | Certification baseline for downstream adopters | Assurance and Certification WG | [#5](https://github.com/space-grade-linux/TSC/pull/5) |

**Discussion on the PRs since October 1:**

- RFC-0001: Piotr Skrzypek asked not to exclude Linux running next to an RTOS on a multi-core SoC in AMP configuration. Many targets provide enough isolation that a hypervisor is not always needed.
- RFC-0002: @h313 volunteered for the CI Testing WG with @kevinthegreat1, offered to merge their cache-aware fault injection tool with the others, and suggested targeting non-cached values first since HPSC has ECC in the cache. Nick Zajerko-McKee asked about bit flips in memory-mapped device registers (SPI, I2C); @h313 replied their branch avoids MMIO today but could be changed, and that it needs accurate device simulation, so scope is for the WG to decide.
- RFC-0003: Philip Balister offered his GitLab CI and Labgrid hardware-in-the-loop setup.
- RFC-0004: Ivan Perez expressed interest.
- RFC-0005: Ivan Perez expressed interest. Piotr Skrzypek laid out paths forward (evolve the standards toward alternative verification approaches, use AI-assisted engineering for scale, and avoid aggressive tailoring), offered a presentation on the ECSS requirements that make Linux qualification hard, and noted ESA is running a lessons-learned study on missions flying Linux, including OPS-SAT.

**Ask:** comment on the PRs before the next call at [github.com/space-grade-linux/TSC](https://github.com/space-grade-linux/TSC).

**Notes:**

- Agreed to start locating working group leads now, without waiting for the TSC decision on the RFCs. Each proposed WG needs a lead:
  - SDV for Space Architecture WG (RFC-0001)
  - CI Testing WG (RFC-0002 and RFC-0003)
  - LTS and Release Engineering WG (RFC-0004)
  - Assurance and Certification WG (RFC-0005)
- **Call for WG leads:** if you want to lead one of these working groups, or want to nominate someone, comment on the RFC pull request or reply on the mailing list.

---

# Main Topic: Governance review

## The charter at a glance

The [Technical Charter](../../CHARTER.md) was adopted April 16, 2026. Space Grade Linux is a Series of LF Projects, LLC.

- **Mission (1.a):** an open source Yocto-based reference distribution for space systems.
- **TSC = the committers (2.b):** voting members are the project's committers, and TSC meetings are open to the public.
- **Licensing (7):** MIT for code, CC-BY-4.0 for docs, DCO sign-off on every commit.
- **Open participation (4.d):** nobody is excluded on competitive interests, only on rules applied equally to all.

## How the TSC decides

Consensus first. When a vote is needed, it is one vote per voting member (section 3).

- **6 voting members:** today's committers on meta-sgl.
- **Quorum of 3:** 50% of voting members must be present to decide anything.
- **>50% for normal decisions:** majority of attendees; email votes need a majority of all members.
- **2/3 for charter changes:** two-thirds of the entire TSC, for amendments and license exceptions.

## Who is on the TSC

- Ramón Roche (@mrpollo), project lead
- Philip Balister (@balister)
- Tim Bird (@tbird20d)
- Ivan Perez (@ivanperez-keera)
- Rob Woolley (@robwoolley)
- Pedro Roque (@Pedro-Roque)

**How to become one:**

1. Sustained, high-quality contributions to meta-sgl
2. A committer nominates you
3. Majority vote of existing committers
4. Recorded in MAINTAINERS.md

Seats are earned, not bought.

## The TSC Chair and open questions

**TSC Chair (2.f):** elected by the TSC, serves until resignation or replacement, presides over TSC meetings, and is the main contact between the project and the Space Grade Linux Fund.

**For discussion:**

- Is committers-only still right as SGL grows beyond meta-sgl?
- Should the TSC document a broader path to a vote? Charter 2.b allows it.
- Who is close to committer status today?
- How and when do we elect the chair?

**Notes:**

- Agreed that Ramón reaches out to each committer who is a TSC voting member under charter 2.b and asks whether they accept the position.
- Once they confirm, Ramón schedules the first TSC meeting.

## Two bodies, two jobs

| | Governing Board | Technical Steering Committee |
| --- | --- | --- |
| Scope | The Fund: business decisions | The project: technical decisions |
| Covers | Budget and staffing, membership and marketing, events and legal | Roadmap, RFCs and releases, contribution and security policy, working groups |
| Seats | Come with membership | Earned by committers |

Membership funds the work. Merit governs the code.

---

# Formation meetings and founding members

Formation meetings for the Space Grade Linux Fund start **Thursday, October 22**.

- **What:** set up the Fund: governing board, budget, 2027 priorities.
- **Who:** organizations joining or considering membership.
- **How to join:** not on the invite? Email Ramón after this call.
- **Enroll:** [enrollment.lfx.linuxfoundation.org/?project=space-grade-linux-fund](https://enrollment.lfx.linuxfoundation.org/?project=space-grade-linux-fund)

Founding members signing on: NEC, Frontgrade Gaisler, SpaceCubics. 30+ organizations have engaged in the SIG since 2024. Full launch and member announcement on December 7 at OSS Japan, Tokyo.

**Notes:**

- Reminder: the first formation meeting is Thursday, October 22. Organizations joining or considering membership who are not on the invite should email Ramón.

---

# Mailing List Highlights

-

---

# Action Items Review (from Oct 1)

- All: review and comment on RFC-0001 to RFC-0005 on their pull requests or on the mailing list
- Ramón: summarize mailing list replies on each RFC pull request
- Ramón: update meta-sgl links in the RFC branches to space-grade-linux/meta-sgl
- Philip Balister: share GitLab CI and Labgrid hardware-in-the-loop setup (RFC-0003)
- Volunteers for each proposed WG: add your name on the RFC pull request
- Rob Woolley: integrate the new Yocto LTS release (Wrynose) into SGL CI
- Ramón: follow up with Matt Weber on adding a Space workload example to the roadmap
- Group: evaluate FTRFS and ZFS for SGL inclusion, including licensing implications and hardware fault-tolerance baseline assumptions
- Ramón: chase remaining doc relicensing approvals (CC-BY-SA-4.0 -> CC-BY-4.0) from Matthias Schmitz and Celeste

---

# Open Discussion / AOB

-

---

# Closing

## Three asks

1. Comment on the open RFC PRs before the next call
2. Join the formation meeting on Thursday, October 22
3. Want to be a committer? Start with a PR to meta-sgl

[github.com/space-grade-linux](https://github.com/space-grade-linux) · [lists.elisa.tech/g/space-grade-linux](https://lists.elisa.tech/g/space-grade-linux)

## Action Items

- All: volunteer or nominate leads for the four proposed WGs, on the RFC pull requests or the mailing list
- Ramón: announce the call for WG leads on the mailing list
- Ramón: contact each TSC voting member under charter 2.b to confirm they accept the position, then schedule the first TSC meeting
- Organizations joining or considering membership: attend the formation meeting on Thursday, October 22 (email Ramón if not on the invite)
- All: keep commenting on RFC-0001 to RFC-0005 on their pull requests or on the mailing list

Tracked in [GitHub Issues](https://github.com/space-grade-linux/TSC/issues)

## Next Meeting

- TBD
