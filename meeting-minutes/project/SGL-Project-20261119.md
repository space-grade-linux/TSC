![logo](logo_elisa_small.png )

## ELISA Space Grade Linux Special Interests Group

The goal of the group is to advance space technology innovation and competitiveness by developing a common Linux distribution that can be used in space applications, ready for the challenges of deep space, often long lifespan robotic or human-based missions. The nature of space missions brings many challenges, from development to deployment there are multiple considerations that need to be considered. Furthermore this group is the initial step towards creating an ecosystem of supported platforms and a community that benefits from them, and also from the open source nature of the project. (https://lists.elisa.tech/g/space-grade-linux/)

# Minutes

## 19 November, 2026

---

# Agenda

- Roll Call
- Brief Notices
- Announcements
  - Upcoming Events
  - Project news
- Main Topic: The Technical Steering Committee
  - What the kick-off covered
  - Who is on the TSC
  - Space agency seats and new members
  - The TSC Chair
  - What comes next for the TSC
- RFC check-in (five RFCs in Draft)
- Closing a chapter: Space Grade Linux at ELISA
  - By the numbers
  - In person
  - Milestones along the way
  - Thank you, ELISA
- What happens next
- Mailing List Highlights
- Action Items Review
- Open Discussion / AOB
- Closing

---

# Roll Call

## Attended this meeting

-

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

- **Dec 9** Space Grade Linux launches as a standalone Linux Foundation project at Open Source Summit Japan, Tokyo. This replaces the December 7 date shared on October 15.

## Project news

- This is the last meeting of Space Grade Linux as an ELISA Special Interest Group. After the launch, SGL continues as its own project under the Linux Foundation.
- The Technical Steering Committee held its first meeting on Friday, November 13 (see below).
- The relicensing of the documentation to CC-BY-4.0 is complete, which closes a long-running action item. The repositories now match section 7 of the charter: MIT for code and CC-BY-4.0 for documentation.
- meta-sgl has recent pull requests waiting for review: [#69](https://github.com/space-grade-linux/meta-sgl/pull/69) build and run docs for BeagleV-Fire, [#71](https://github.com/space-grade-linux/meta-sgl/pull/71) small fixes, [#73](https://github.com/space-grade-linux/meta-sgl/pull/73) PIC64-HPSC QEMU guide for arm64 hosts, and [#74](https://github.com/space-grade-linux/meta-sgl/pull/74) meta-mchp bump for PIC64-HPSC. Reviews are welcome.

---

# Main Topic: The Technical Steering Committee

The TSC held its kick-off meeting on Friday, November 13, 2026. It is the first TSC meeting under the [Technical Charter](../../CHARTER.md), and it follows the governance review from October 15.

## What the kick-off covered

1. Introductions
2. Charter review: membership, decision making, quorum and future seats
3. Space agency participation in the TSC, and votes to admit two new members
4. Election of the TSC Chair
5. The five RFCs for 2027, moved to the next TSC meeting for lack of time
6. A proposal from a member organization related to RFC-0001
7. Next steps

Minutes: [SGL-TSC-20261113.md](../tsc/SGL-TSC-20261113.md), in review as [#9](https://github.com/space-grade-linux/TSC/pull/9)

## Who is on the TSC

Under charter section 2.b the voting members are the meta-sgl committers. The committers serving on the TSC:

- Ramón Roche (@mrpollo), project lead
- Philip Balister (@balister)
- Ivan Perez (@ivanperez-keera)
- Rob Woolley (@robwoolley)
- Pedro Roque (@Pedro-Roque)

Admitted as TSC members by vote on November 13:

- Michael Monaghan
- Piotr Skrzypek

## Space agency seats and new members

The TSC discussed giving space agencies a path to a voting seat, since agency staff often cannot contribute as committers. It did not adopt a standing rule. Members raised the balance between agency and commercial interests, whether a seat should be automatic or decided case by case, and how to keep politics out of the project.

For now the TSC admitted the two agency participants present, each by its own vote and with no commitment on future seats. The permanent policy will be settled when the TSC revisits who holds a voting seat, starting with the definition of committer. Charter section 2.b lets the TSC choose an alternative approach for determining its voting members, as long as it is documented in the CONTRIBUTING file.

## The TSC Chair

The TSC elected **Michael Monaghan** as its first Chair, for his role in starting Space Grade Linux and his involvement since the beginning. No other candidates came forward.

- **The role (charter 2.f):** the Chair presides over TSC meetings, serves until resignation or replacement by the TSC, and is the primary contact between the project and the Space Grade Linux Fund.
- The role is technical. Funding, membership and other business decisions stay with the Governing Board of the Fund.

## What comes next for the TSC

- Define who holds a TSC voting seat: tighten the definition of committer and settle the policy for space agency participation. Both start as email threads on a new TSC mailing list.
- Agree on a TSC meeting cadence. TSC meetings are intended to be open to the public (charter 2.b).
- Take up the five RFCs at the next TSC meeting (see the RFC check-in below).
- List the TSC members on the project website for the launch.
- TSC minutes are published in [meeting-minutes/tsc](../tsc/).

**Notes:**

-

---

# RFC check-in

The five RFCs are still open as Draft pull requests. The minimum comment period (two project meetings or three weeks) was met on October 15, so they are ready for a TSC decision. The TSC ran out of time at its November 13 kick-off and will take them up at its next meeting. Before approving them, the TSC may set requirements such as an identified lead for each working group.

| RFC | Title | Proposed WG | Discussion |
| --- | --- | --- | --- |
| 0001 | Software-defined vehicle architecture for space systems | SDV for Space Architecture WG | [#1](https://github.com/space-grade-linux/TSC/pull/1) |
| 0002 | Radiation fault injection in CI | CI Testing WG | [#2](https://github.com/space-grade-linux/TSC/pull/2) |
| 0003 | Hardware-in-the-loop testing in CI | CI Testing WG | [#3](https://github.com/space-grade-linux/TSC/pull/3) |
| 0004 | Long-term support releases | LTS and Release Engineering WG | [#4](https://github.com/space-grade-linux/TSC/pull/4) |
| 0005 | Certification baseline for downstream adopters | Assurance and Certification WG | [#5](https://github.com/space-grade-linux/TSC/pull/5) |

**Discussion on the PRs since October 15:**

- RFC-0001: @h-hihara proposed IEEE 1003.1 (POSIX) and IEEE 2050-2018 as the basis for evaluating an OS-agnostic reference architecture and the interface between Linux and RTOSes. They also supported treating the hypervisor as one option and not a requirement, since many SoCs already provide efficient communication between cores. @yassine-cherni expressed interest.
- RFC-0002: @kbp-sigmalabs runs radiation tests on Linux platforms and offered to contribute. They suggested starting from LEO use cases, where most Linux platforms fly today, and pointed to [QEMU simulation of SEEs](https://github.com/space-grade-linux/meta-sgl/issues/40) as a way to cover more use cases.
- RFC-0003: @kbp-sigmalabs offered to contribute from the radiation testing side.
- RFC-0004: no new comments.
- RFC-0005: no new comments.

**From the TSC kick-off:** a member organization wants to contribute to RFC-0001, with a focus on the interfaces between Linux and an RTOS, and a TSC member reported similar work starting with a different RTOS. The suggestion was to define that interface together, across RTOSes.

**Working group leads:** the call for leads from October 15 is still open. Each proposed WG needs one:

- SDV for Space Architecture WG (RFC-0001)
- CI Testing WG (RFC-0002 and RFC-0003)
- LTS and Release Engineering WG (RFC-0004)
- Assurance and Certification WG (RFC-0005)

**For discussion:**

- Volunteers or nominations for WG leads. A lead for each working group makes the TSC decision easier
- What else the TSC should require of an RFC before approving it

**Ask:** keep commenting on the PRs at [github.com/space-grade-linux/TSC](https://github.com/space-grade-linux/TSC). The work continues there while the calls are paused.

**Notes:**

-

---

# Closing a chapter: Space Grade Linux at ELISA

Today is the last meeting of Space Grade Linux as an ELISA Special Interest Group. Before we move on, a look back at what this group did under the ELISA Project.

## By the numbers

| | |
| --- | --- |
| SIG calls | 22, counting today. The first dedicated SGL call was January 16, 2025. In 2024 the SIG met together with the ELISA Aerospace Working Group. |
| Time on calls | About 30 hours |
| Published minutes | 21 sets, January 2025 to October 2026 |
| Attendance | 300 sign-ins across the roll calls, about 15 people per call |
| People | More than 80 |
| Organizations | More than 40: space agencies, primes, silicon vendors, OS vendors, startups, universities and other open source projects |
| Guest talks | Red Hat, Columbia University (Radshield), KP Labs and Tuxera |
| Interest survey | 46 responses, September 2024 to January 2026 |
| meta-sgl | 35 pull requests merged, 11 contributors |

## In person

ELISA workshops:

- **December 10 to 12, 2024:** ELISA Workshop at NASA Goddard Space Flight Center, Greenbelt, Maryland. Co-hosted by NASA and themed on Space Grade Linux. [Presentation archive](https://directory.elisa.tech/workshops/index.html)
- **November 18 to 19, 2025:** ELISA Workshop, Munich
- **June 9 to 11, 2026:** ELISA Workshop, London

On the road, Space Grade Linux was presented at:

- **August 2025:** Open Source Summit Europe, Amsterdam
- **October 2025:** ROSCon, Singapore, with the first hardware demo of SGL and Space ROS ([recap](https://elisa.tech/blog/2025/11/13/robotics-and-space-grade-linux-at-roscon-2025-singapore/))
- **December 2025:** Open Source Summit Japan, Tokyo, with the SGL keynote and a community meetup
- **February 2026:** OpenEmbedded Workshop, Brussels

## Milestones along the way

- **2024:** the SIG forms under ELISA, the mailing list opens and the SGL Interest Survey starts collecting responses
- **January 2025:** first dedicated SIG call. The group settles on MIT for code, Creative Commons for documentation and DCO sign-off
- **October 2025:** first hardware demo of SGL with Space ROS
- **November 2025:** the SIG discusses its intent to form a standalone project
- **December 2025:** SGL keynote at Open Source Summit Japan
- **April 2026:** Technical Charter adopted
- **September 2026:** five RFCs propose the 2027 working groups, and meta-sgl and the governance repository move to the [space-grade-linux](https://github.com/space-grade-linux) GitHub organization
- **November 2026:** first TSC meeting and first TSC Chair
- **December 9, 2026:** launch

## Thank you, ELISA

Space Grade Linux exists because the ELISA Project gave it a home before it had anything to show. A huge thank you to:

- The **ELISA Project**, its Governing Board and its TSC, for taking in a space SIG and backing it for more than two years
- The **ELISA Aerospace Working Group**, for sharing its calls with us in 2024 and for the collaboration since, from the cFS demo build to kernel minimization
- The **Linux Foundation staff behind ELISA**, for the meetings, the mailing list, the workshops, the survey and the website
- The **workshop hosts**, starting with NASA Goddard, for getting us in the same room
- **Everyone who joined a call**, presented, reviewed a pull request or answered a thread on the list. You are the reason there is a project to launch

We are leaving the SIG, not the community. ELISA's work on safety for Linux and ours on Linux for space stay closely related, and we expect to keep working together.

**Notes:**

-

---

# What happens next

- **Launch:** December 9, at Open Source Summit Japan in Tokyo. Founding members are announced with the launch.
- **Recurring calls:** we do not know yet when the recurring project calls resume. We will have a better idea once the project has launched, and the new schedule will be announced on the mailing list. The ELISA SIG call series ends with this meeting. How and when the project moves to its own meetings and infrastructure is for the TSC to define.
- **Where to find us in the meantime:**
  - Code: [space-grade-linux/meta-sgl](https://github.com/space-grade-linux/meta-sgl)
  - Governance, RFCs and minutes: [space-grade-linux/TSC](https://github.com/space-grade-linux/TSC)
  - Mailing list: [lists.elisa.tech/g/space-grade-linux](https://lists.elisa.tech/g/space-grade-linux/)
- **The work does not stop:** RFC review, WG lead nominations and meta-sgl pull requests continue on GitHub and the mailing list.

**Notes:**

-

---

# Mailing List Highlights

- The ELISA Aerospace WG posted an RFC with draft Linux kernel minimization documentation on October 20 and is asking for feedback.

---

# Action Items Review (from Oct 15)

- All: volunteer or nominate leads for the four proposed WGs, on the RFC pull requests or the mailing list
- Ramón: announce the call for WG leads on the mailing list (done, October 15)
- Ramón: contact each TSC voting member under charter 2.b to confirm they accept the position, then schedule the first TSC meeting (done, the TSC met November 13)
- Organizations joining or considering membership: attend the formation meeting
- All: keep commenting on RFC-0001 to RFC-0005 on their pull requests or on the mailing list

---

# Open Discussion / AOB

-

---

# Closing

## Three asks

1. Comment on the open RFC PRs, and volunteer or nominate a WG lead
2. Watch the mailing list for the launch on December 9 and for the new call schedule
3. Want to be a committer? Start with a PR to meta-sgl

[github.com/space-grade-linux](https://github.com/space-grade-linux) · [lists.elisa.tech/g/space-grade-linux](https://lists.elisa.tech/g/space-grade-linux)

## Action Items

-

Tracked in [GitHub Issues](https://github.com/space-grade-linux/TSC/issues)

## Next Meeting

- To be announced after the launch. This was the last meeting as the ELISA Space Grade Linux SIG.
