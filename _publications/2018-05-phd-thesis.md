---
key: A18
slug: phd-thesis
type: phdthesis
title: "A Systematic Approach to Benchmark and Improve Automated Static Detection of Java-API Misuses"
authors:
  - amann
published_in: "Technische Universität Darmstadt"
year: 2018
publisher_link: http://tuprints.ulb.tu-darmstadt.de/7422/
abstract: |+
  Today's software industry relies heavily on the reuse of existing software libraries. Such libraries provide the building blocks for modern software products. Reusing them allow developers to focus on innovation, while standing on the shoulders of giants. To use libraries effectively, developers need to know the Application Programming Interfaces (APIs) through which they communicate with the libraries. This includes both the APIs' semantics and the (implicit) usage constraints that come with them. In the face of the rapidly growing and evolving supply of software libraries, this has become a challenging task. As a result, incorrect usages of APIs, or API misuses, are a prevalent cause of software bugs, crashes, and vulnerabilities.

  In reaction to this problem, researchers have proposed a multitude of developer-assistance tools. One particular class of such tools automates the detection of API misuses in software code. We call these tools API-misuse detectors. Existing misuse detectors address different aspects of API misuse. However, no attempt has been made to systematically define the problem space of API misuse and to assess the prevalence of API misuses compared to other types of bugs. This makes it impossible to judge the relevance of research on API-misuse detection. Moreover, previous empirical evaluations of misuse detectors commonly measure the detectors' precision. However, since the studies use different datasets, it is unclear to which extend the results are comparable. It is also unclear where the detectors make trade-offs between their precision and their recall.

  In this thesis, we first present a systematic analysis of the problem of API misuse. We find that API misuse causes 9.1% of all software bugs in real-world projects, including many critical issues, such as program crashes, data loss, and security vulnerabilities. Then, we survey the literature to consolidate over a decade of research on API-misuse detection and build MUBench, a public automated benchmark for API-misuse detectors. This enables us to conduct the first-ever qualitative and quantitative comparison of existing misuse detectors. We find that these detectors have the potential to discover many API misuses, but suffer from extremely low precision and recall in practice. Finally, we systematically design MUDetect, a new API-misuse detector that addresses many of the problems of existing detectors. Using MUBench, we demonstrate that MUDetect clearly outperforms existing detectors with respect to both precision and recall. Our results provide strong evidence that, following our systematic approach, we can develop API-misuse detectors that are fit for practical application.
---
