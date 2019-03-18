---
key: ANNN+19
slug: mudetect
type: conference
title: "Investigating Next Steps in Static API-Misuse Detection"
authors:
  - amann
  - hoan
  - nadi
  - tien
  - mezini
published_in: "Proceedings of the 16th International Conference on Mining Software Repositories"
series: MSR
year: 2019
preprint: mudetect-msr19.pdf
artifact_page: http://www.st.informatik.tu-darmstadt.de/artifacts/mudetect/
abstract: >
  Application Programming Interfaces (APIs) often impose constraints such as call order or preconditions. API misuses, i.e., usages violating these constraints, may cause software crashes, data-loss, and vulnerabilities. Researchers developed several approaches to detect API misuses, typically still resulting in low recall and precision. In this work, we investigate ways to improve API-misuse detection. We design MUDetect, an API-misuse detector that builds on the strengths of existing detectors and tries to mitigate their weaknesses. MUDetect uses a new graph representation of API usages that captures different types of API misuses and a systematically designed ranking strategy that effectively improves precision. Evaluation shows that MUDetect identifies real-world API misuses with twice the recall of previous detectors and 2.5x higher precision. It even achieves almost 4x higher precision and recall, when mining patterns across projects, rather than from only the target project.

---
