---
key: ANNN+18
slug: mustudy
type: article
title: "A Systematic Evaluation of Static API-Misuse Detectors"
authors:
  - amann
  - hoan
  - nadi
  - tien
  - mezini
published_in: "IEEE Transactions on Software Engineering"
series: TSE
year: 2018
doi: 10.1109/TSE.2018.2827384
preprint: https://arxiv.org/abs/1712.00242
artifact_page: http://www.st.informatik.tu-darmstadt.de/artifacts/mustudy/
abstract: >
  Application Programming Interfaces (APIs) often have usage constraints, such as restrictions on call order or call conditions. API misuses, i.e., violations of these constraints, may lead to software crashes, bugs, and vulnerabilities. Though researchers developed many API-misuse detectors over the last two decades, recent studies show that API misuses are still prevalent. Therefore, we need to understand the capabilities and limitations of existing detectors in order to advance the state of the art. In this paper, we present the first-ever qualitative and quantitative evaluation that compares static API-misuse detectors along the same dimensions, and with original author validation. To accomplish this, we develop MUC, a classification of API misuses, and MUBenchPipe, an automated benchmark for detector comparison, on top of our misuse dataset, MUBench. Our results show that the capabilities of existing detectors vary greatly and that existing detectors, though capable of detecting misuses, suffer from extremely low precision and recall. A systematic root-cause analysis reveals that, most importantly, detectors need to go beyond the naive assumption that a deviation from the most-frequent usage corresponds to a misuse and need to obtain additional usage examples to train their models. We present possible directions towards more-powerful API-misuse detectors.

---
