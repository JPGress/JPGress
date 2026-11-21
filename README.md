# Pedro Gress

**Cyber Threat Intelligence** — public-source assessments and evidence-led MITRE ATT&CK mapping.  
Brasília / Formosa, Brazil

Background in military environments, IT operations, technical leadership, and university teaching. Open to senior Cyber Threat Intelligence roles.

The public record is the three projects below: one tactical assessment, and two laboratory toolkits whose ATT&CK catalogs state what is implemented and what is still a gap.

## Projects

### [CTI Portfolio](https://github.com/JPGress/cti-portfolio)

Public-source tactical intelligence: the question, the sources, the judgment, and the remaining gap are written as separate things.

**Problem.** Which publicly reported Volt Typhoon behaviors should critical-infrastructure defenders prioritize, and how strong is that judgment?

**How it is built.** One Markdown product. It separates reported fact, source assessment, and analyst judgment, and it defines high and moderate confidence before either grade is used. The source set is the joint advisory AA24-038A (CISA, FBI, NSA, and partners), the Microsoft Threat Intelligence blog of 24 May 2023, and MITRE ATT&CK [G1017](https://attack.mitre.org/groups/G1017/), each with a stated limitation.

**ATT&CK.** The mapping is selective and tied to a cited behavior: [T1190](https://attack.mitre.org/techniques/T1190/), [T1078](https://attack.mitre.org/techniques/T1078/), [T1059.003](https://attack.mitre.org/techniques/T1059/003/), [T1059.001](https://attack.mitre.org/techniques/T1059/001/), [T1003](https://attack.mitre.org/techniques/T1003/), [T1018](https://attack.mitre.org/techniques/T1018/), [T1090](https://attack.mitre.org/techniques/T1090/), and [T1560.001](https://attack.mitre.org/techniques/T1560/001/). Each row names a defensive use. The product then lists priority detection opportunities and collection gaps. Classification is TLP:CLEAR. Published 2026-09-04, with the same information cutoff. The analyst note records no original victim telemetry and no new attribution.

**Status.** Published sample. One product, one commit (2026-09-04).

**Artifacts**

- [Volt Typhoon: Tactical Intelligence Assessment for Critical Infrastructure Defenders](https://github.com/JPGress/cti-portfolio/blob/main/reports/volt-typhoon-tactical-intelligence-assessment.md)
- [Scope, confidence rules, and source principles](https://github.com/JPGress/cti-portfolio/blob/main/README.md)

### [OwL PyOpS](https://github.com/JPGress/0wL-PyOpS)

Python laboratory toolkit: plugins, a CLI, JSON run records, and an ATT&CK catalog that includes the gaps.

**Problem.** The Bash toolkit below is two scripts of about 4,500 lines each. PyOpS is the modular successor: a stable id per tool, aliases back to the old menu numbers, and an explicit difference between a working plugin, a reference, and a missing capability.

**Stack.** Python 3.11+ (`owl-pyops` 0.2.0, setuptools). The core uses the standard library. Optional extras are `dnspython`, `requests`, `beautifulsoup4`, `instaloader`, and `pytest`. Plugins call operator-installed programs, including Nmap, ExifTool, WHOIS, smbclient/rpcclient, and arp-scan. `pyops.py` loads plugins through a registry. The menu and `run` share one argument parser. Each run writes JSON under `outputs/` (gitignored), including the ATT&CK association for that run. Enterprise 19.2 technique ids are pinned in the tree.

**ATT&CK and collection.** This is a catalog of lab behaviors. Implemented plugins cluster on reconnaissance and discovery: DNS and PTR, WHOIS and certificate transparency, zone transfer, document metadata, HTTP headers and site inventory, TCP and Nmap, SMB inventory, and local Linux inventory. The generated matrix marks other tactics as gaps. Scan context selects T1046 or T1595. Reference entries are listed apart from tools.

OwL's Eyes, in the same repository, is a personal attack-surface pilot. The social-collection module is implemented with Instaloader, requests, and BeautifulSoup. The footprint module is a short menu over the DNS and WHOIS plugins. The OPSEC, breach, monitoring, social-engineering, and defensive modules print a pilot-status warning and return.

**Status.** Laboratory prototype, version 0.2.0. Last push 2026-09-27. The portability note of that date records 19 operational plugins, six references, and one intentional gap for the legacy menu, and records 58 unit tests plus 6 loopback integrations passing in the author's environment (Python 3.14). That note keeps every plugin `experimental` until the environmental checks it lists are done. The repository limits use to authorized labs.

**Artifacts**

- [Portability status, ATT&CK corrections, and open acceptance checks](https://github.com/JPGress/0wL-PyOpS/blob/main/docs/plano-portabilidade-attack.md)
- [Generated ATT&CK catalog](https://github.com/JPGress/0wL-PyOpS/blob/main/docs/matriz-attack.md)
- [Architecture and execution contract](https://github.com/JPGress/0wL-PyOpS/blob/main/docs/architecture.md)
- [Operator manual (Portuguese)](https://github.com/JPGress/0wL-PyOpS/blob/main/docs/manual-do-operador.md)
- [Tests](https://github.com/JPGress/0wL-PyOpS/tree/main/tests)
- [Social-collection module](https://github.com/JPGress/0wL-PyOpS/blob/main/plugins/purple/owls_eyes_modules/mod2_socmint.py)
- [Footprint menu](https://github.com/JPGress/0wL-PyOpS/blob/main/plugins/purple/owls_eyes_modules/mod3_footprint.py)
- [Pilot placeholder (OPSEC module)](https://github.com/JPGress/0wL-PyOpS/blob/main/plugins/purple/owls_eyes_modules/mod1_opsec.py)

### [0wL OPS](https://github.com/JPGress/owl-ops)

Bash menu that groups authorized lab tasks by ATT&CK tactic number. Predecessor of PyOpS.

**Problem.** One interactive entry point for reconnaissance and related lab tasks, with a numeric fast path (`./0wlops.sh`, or `./0wlops.sh <option>`).

**Stack.** Bash. Version 1.27.030-VADER, dated 2026-03-24 in the script header. Entry point [`0wlops.sh`](https://github.com/JPGress/owl-ops/blob/main/0wlops.sh) (4,459 lines in the PyOpS migration baseline) and a near-duplicate [`0wlops_unstable.sh`](https://github.com/JPGress/owl-ops/blob/main/0wlops_unstable.sh) (4,489 lines). MIT license, copyright 2025 JPGress. Modules call common utilities such as DNS tools, WHOIS, Nmap, and Netcat. Menu hundreds follow tactic ids. The module table marks HTML parsing (option 106) disabled and SMB enumeration (option 904) unstable.

**ATT&CK.** The menu is organized under TA0043, TA0042, TA0001, TA0004, TA0006, TA0007, and TA0008. The module table is the catalog: reconnaissance, discovery, local references, and a smaller set of lab operations. The PyOpS portability note records legacy option 1001 (`legacy_arp_agent`) as unavailable: the alias resolves, and execution returns unavailable.

**Status.** Predecessor. Still public, not archived. Code changes run through 2026-03-24. The commit on 2026-09-27 adds a review and does not add modules. There is no automated test suite. That review records `bash -n` passing on both scripts, and it flags the duplicated files and the absence of `set -euo pipefail`. Later design work is in PyOpS.

**Artifacts**

- [Module table](https://github.com/JPGress/owl-ops/blob/main/README.md)
- [Review of the Bash scripts](https://github.com/JPGress/owl-ops/blob/main/pareceres-owl-ops-e-migracao-pyops.md) — its paragraph on the Python migration predates the PyOpS portability delivery later the same day; current PyOpS status is the portability note linked above
- [Stable script](https://github.com/JPGress/owl-ops/blob/main/0wlops.sh)

## Focus

- Intelligence requirements, source evaluation, confidence language, and a judgment a defender can use
- ATT&CK mappings kept next to the evidence and the detection implication
- Python and Bash on Linux for lab collection, with missing coverage written into the catalog

## Background

- More than twelve years across military environments, IT operations, technical leadership, and higher education
- University lecturer in information security, networks, operating systems, and project management
- Technical specialization in cyber warfare
- Postgraduate degree in Data Protection Officer (DPO)
- arcX Foundation-level Threat Intelligence Analyst
- CompTIA Security+ (SY0-701), in progress, target December 2026

## Português

Profissional de cibersegurança em Brasília / Formosa, com mais de 12 anos em ambientes militares, operações de TI, liderança técnica e docência universitária (segurança da informação, redes, sistemas operacionais e gestão de projetos). O material público acima está em inglês: uma avaliação tática de fontes abertas sobre o Volt Typhoon e duas ferramentas de laboratório (PyOpS em Python e 0wL OPS em Bash), com mapeamento MITRE ATT&CK e limitações declaradas no próprio código. Especialização técnica em guerra cibernética, pós-graduação em encarregado de dados (DPO) e arcX Foundation-level Threat Intelligence Analyst. CompTIA Security+ SY0-701 em andamento, meta em dezembro de 2026. Aberto a posições seniores de Cyber Threat Intelligence.

## Contact

- [LinkedIn](https://www.linkedin.com/in/pedrogress)
- [Email](mailto:jpgress@gmail.com)

> All public portfolio material uses public sources and excludes client, operational, and restricted information. The laboratory toolkits above are scoped to authorized environments.
