---
key: PNAM16
slug: enriched-event-streams
type: conference
title: "Enriching In-IDE Process Information with Fine-grained Source Code History"
authors:
  - proksch
  - nadi
  - amann
  - mezini
published_in: "Proceedings of the 24th International Conference on Software Analysis, Evolution, and Reengineering"
series: SANER 17
year: 2017
abstract: >
  Current studies on software development either focus on the change history of source code from version-control systems or on an analysis of simplistic in-IDE events without context information. Each of these approaches contains valuable information that is unavailable in the other case. Our work proposes enriched event streams, a solution that combines the best of both worlds and provides a holistic view on the software development process. Enriched event streams not only capture developer activities in the IDE, but also specialized context information, such as source-code snapshots for change events. To enable the storage of such code snapshots in an analyzable format, we introduce a new intermediate representation called Simplified Syntax Trees (SSTs) and build CARET, a platform that offers reusable components to conveniently work with enriched event streams. We implement FeedBaG++, an instrumentation for Visual Studio that collects enriched event streams with code snapshots in the form of SSTs. We share a dataset of enriched event streams captured from 58 users and representing 915 days of work. Additionally, to demonstrate usefulness, we present three research applications that have already made use of CARET and FeedBaG++.
artifact_page: http://www.st.informatik.tu-darmstadt.de/artifacts/caret/

---
