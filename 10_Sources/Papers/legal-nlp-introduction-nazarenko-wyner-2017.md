---
type: source
status: draft
created: 2026-07-10
title: "Legal NLP Introduction"
authors:
- Adeline Nazarenko
- Adam Wyner
organisation: "LIPN, Université Paris 13 / Sorbonne Paris Cité and CNRS; Swansea University, School of Law and Department of Computer Science"
source_type: paper
venue: "TAL (Traitement Automatique des Langues), Volume 58, n°2"
url: TBD
year: 2017
date_published: 2017
anthropic: false
topic:
- topic/domain-applications
- topic/research-papers
tags: [legal-nlp, survey, legaltech, argumentation-mining, document-engineering]
nlm_id: 
nlm_skip: false
watchlist_channel: 
---

# Legal NLP Introduction

> Full citation: Nazarenko, A. and Wyner, A. "Legal NLP Introduction." TAL, Volume 58, n°2, 2017, pages 7-19.

## Summary

This introduction frames legal natural language processing as a field that spans a full stack of linguistic analysis, from character-string identification through to argumentation. Nazarenko and Wyner open the special issue of TAL by arguing that language and law share a close bond, since law is fundamentally a discourse. They survey LegalTech applications built on NLP, including document drafting, information retrieval, resource linking, and compliance checking, then set out why legal language resists standard NLP tools built for newspaper or narrative text. The paper closes on integration: combining citation extraction, syntactic parsing, terminology handling, semantic analysis, discourse analysis, and argumentation mining into a single operational pipeline. The authors treat this integration challenge as under-documented and largely unsolved, and they use it to introduce the two research papers that follow in the issue.

## Key Concepts

- Legal NLP spans levels of analysis from citation identification to argumentation.
- LegalTech applications include drafting, retrieval, linking, reasoning, and compliance checking.
- Legal language resists NLP tools trained on newspaper or narrative corpora.
- Legal applications demand high performance and explanation, not just accuracy.
- Integration across analysis levels remains a technical problem without documented trade-offs.

## Terminology

- **LegalTech** — technologies from computer science applied to legal practice and materials, including document support, litigation discovery, and legal research.
- **Forensic linguistics** — linguistic analysis applied to legal materials in proceedings, such as authorship identification and courtroom discourse analysis.
- **Shepardisation** — the practice of linking cases through relations such as upholds and overrules in case law.
- **LegalDocML / Akoma Ntoso** — standards for encoding the structure of legal documents.
- **LegalRuleML** — a standard for encoding the semantic content of legal rules.

## Architecture and Implementation

The paper does not describe a single system. Instead, it identifies the levels of linguistic analysis a legal NLP pipeline must integrate.

- **Document engineering** — normalising legal documents and encoding their structure, using standards such as Akoma Ntoso and LegalDocML.
- **Syntactic analysis** — parsing long, embedded, and ambiguous legal sentences, where general-purpose parsers such as the Stanford Parser often fail.
- **Terminology** — resolving legal terms of art alongside domain terminology drawn from the field the law regulates.
- **Stylistics** — accounting for drafting conventions intended to reduce ambiguity.
- **Semantic analysis** — supporting information retrieval, consistency checking, and reasoning, through tasks such as semantic annotation and rule extraction.
- **Discourse analysis** — organising and contextualising content through the analysis of document networks.
- **Argumentation analysis** — mining, checking, and modelling legal arguments as the basis of legal reasoning.
- **Knowledge engineering** — building ontologies and formal rule representations that ground semantic analysis and support temporal reasoning over legal timelines.

The authors note that errors propagate between these levels, and that ambiguity resolved at one level can introduce error at another. They cite general text-engineering architectures, such as GATE, NLTK, and UIMA, as candidate frameworks for managing this integration, though none was designed for legal sources specifically.

## Code Examples

This is a journal introduction; it does not ship code.

## Best Practices

- Treat citation and list-structure extraction as a distinct NLP module, since legal presentational formats break sentences across nested lists.
- Validate translation and retrieval output against the standard set by human legal experts, since legal applications tolerate little error.
- Provide explanation alongside classification output, since legal decision-making requires a transparent basis in precedent and legislation.
- Track document versioning explicitly, since legal texts are amended and multiple versions of the same article can coexist.

## Warnings and Anti-Patterns

- Do not apply NLP tools trained on newspaper or narrative text to legal corpora without adaptation. Long, embedded clauses and legal-specific lexis degrade parser performance.
- Do not treat high classifier accuracy as sufficient for legal decision-making. A verdict prediction without explanation fails the legal system's requirement for a reasoned, precedent-based justification.
- Do not treat integration across analysis levels as a solved technical detail. The authors state that the trade-offs between analysis depth, reliability, and coverage are rarely documented, so proposed integration solutions cannot be judged as optimal.

## Related Concepts

- [[what-is-an-ai-agent]]
- [[civil-law-article-retrieval-tran-2017]]
- [[legal-qa-ranking-svm-cnn-do-2017]]

## Future Work

The authors call for tools that support comparative law across jurisdictions, richer metadata standards for legislative publication, and a legal semantic web that interconnects sources for query and enrichment. They flag generic legal semantic parsing as an open research issue, and they call for explicit documentation of the trade-offs involved in integrating NLP, semantic technologies, and knowledge engineering into a single legal application.

## References

- Athan, T., Governatori, G., Palmirani, M., Paschke, A. and Wyner, A. Z. "LegalRuleML: Design Principles and Foundations." Reasoning Web, Springer, 2015, pages 151-188.
- Bonin, F., Dell'Orletta, F., Venturi, G. and Montemagni, S. "Singling out Legal Knowledge from World Knowledge. An NLP-based approach." Proceedings of LOAIT, 2010.
- Boulet, R., Mazzega, P. and Bourcier, D. "A Network Approach to the French System of Legal Codes - Part I: Analysis of a Dense Network." Journal of Artificial Intelligence and Law, Volume 19, 2011, pages 333-355.
- Casanovas, P., Palmirani, M., Peroni, S., van Engers, T. M. and Vitali, F. "Semantic Web for the Legal Domain: The next step." Semantic Web, Volume 7, n°3, 2016, pages 213-227.
- Christensen, M. L., Olsen, H. P. and Tarissan, F. "Identification of Case Content with Quantitative Network Analysis: An Example from the ECtHR." Legal Knowledge and Information Systems - JURIX 2016, IOS Press, 2016, pages 53-62.
- Coulthard, M. and Johnson, A. (eds). The Routledge Handbook of Forensic Linguistics. Routledge, 2010.
- Dragoni, M., Villata, S., Rizzi, W. and Governatori, G. "Combining NLP Approaches for Rule Extraction from Legal Documents." Proceedings of the Workshop on Mining and Reasoning with Legal Texts, JURIX, 2016.
- Francesconi, E. "Semantic Model for Legal Resources: Annotation and Reasoning over Normative Provisions." Semantic Web Journal, Volume 7, n°3, 2016, pages 255-265.
- Gordon, T. F. "A Theory Construction Approach To Legal Document Assembly." Pre-Proceedings of the 3rd International Conference on Logic, Informatics, and Law, 1989, pages 485-498.
- Höfler, S. "Legislative Drafting Guidelines: How Different Are They from Controlled Language Rules for Technical Writing?" Proceedings of Controlled Natural Language CNL2012, Springer, 2012, pages 138-151.
- Mimouni, N., Nazarenko, A. and Salotti, S. "An Approach for Searching and Browsing a Network of Legal Documents." Network Analysis in Law, Edizioni Scientifiche Italiane, 2014, pages 183-207.
- Moens, M.-F., Boiy, E., Palau, R. M. and Reed, C. "Automatic Detection of Arguments in Legal Texts." Proceedings of the 11th International Conference on Artificial Intelligence and Law, ICAIL, 2007, pages 225-230.
- Osslon, J. "Forensic linguistics." LINGUISTICS - Volume I, Encyclopedia of Life Support Systems, EOLSS Publishers/UNESCO, 2009, pages 378-393.
- Sartor, G., Casanovas, P., Biasiotti, M. and Fernández-Barrera, M. Approaches to Legal Ontologies: Theories, Domains, Methodologies. Springer, 2013.
- Sprowl, J. "Automated Assembly of Legal Documents." Computer Science and Law - an advanced course, Cambridge University Press, 1980, pages 195-203.
- Winkels, R. and de Ruyter, J. "Survival of the Fittest: Network Analysis of Dutch Supreme Court Cases." AI Approaches to the Complexity of Legal Systems (AICOL-III), Springer, 2011, pages 106-115.
- Wyner, A., Mochales-Palau, R., Moens, M.-F. and Milward, D. "Approaches to Text Mining Arguments from Legal Cases." Semantic Processing of Legal Texts, Springer-Verlag, 2010, pages 60-79.
- Wyner, A. and Peters, W. "On Rule Extraction from Regulations." Legal Knowledge and Information Systems - JURIX 2011, IOS Press, 2011, pages 113-122.
