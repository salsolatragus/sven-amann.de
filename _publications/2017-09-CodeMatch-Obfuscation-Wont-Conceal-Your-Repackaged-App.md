---
key: GAER+17
slug: codematch
type: conference
title: "CodeMatch: Obfuscation Won’t Conceal Your Repackaged App"
authors:
  - glanz
  - amann
  - eichberg
  - reif
  - hermann
  - lerch
  - mezini
published_in: "Proceedings of the 11th Joint Meeting of the European Software Engineering Conference and the ACM SIGSOFT Symposium on the Foundations of Software Engineering"
series: ESEC/FSE 17
year: 2017
doi: 10.1145/3106237.3106305
abstract: >
  An established way to steal the income of app developers, or to trick users into installing malware, is the creation of repackaged
  apps. These are clones of – typically – successful apps. To conceal their nature, they are often obfuscated by their creators. But, given that it is a common best practice to obfuscate apps, a trivial identification of repackaged apps is not possible. The problem is further intensified by the prevalent usage of libraries. In many apps, the size of the overall code base is basically determined by the used libraries. Therefore, two apps, where the obfuscated code bases are very similar, do not have to be repackages of each other.
  
  To reliably detect repackaged apps, we propose a two step approach which first focuses on the identification and removal of
  the library code in obfuscated apps. This approach – LibDetect – relies on code representations which abstract over several parts
  of the underlying bytecode to be resilient against certain obfuscation techniques. Using this approach, we are able to identify on
  average 70% more used libraries per app than previous approaches. After the removal of an app’s library code, we then fuzzy hash the
  most abstract representation of the remaining app code to ensure that we can identify repackaged apps even if very advanced obfuscation techniques are used. This makes it possible to identify repackaged apps. Using our approach, we found that ≈ 15% of all
  apps in Android app stores are repackages.
artifact_page: http://www.st.informatik.tu-darmstadt.de/artifacts/codematch/

---
