---
type: source
status: draft
created: 2026-07-10
title: "Exploring the Use of Text Classification in the Legal Domain"
authors:
- Octavia-Maria Sulea
- Marcos Zampieri
- Shervin Malmasi
- Mihaela Vela
- Liviu P. Dinu
- Josef van Genabith
organisation: 
source_type: paper
venue: 
url: https://arxiv.org/abs/1710.09306
year: 2017
date_published: 2017-10-25
anthropic: false
topic:
- topic/domain-applications
- topic/research-papers
tags: [legal-nlp, text-classification, french-supreme-court, svm, ensemble-methods]
nlm_id: 
nlm_skip: false
watchlist_channel: 
---

# Exploring the Use of Text Classification in the Legal Domain

> Full citation: Octavia-Maria Sulea, Marcos Zampieri, Shervin Malmasi, Mihaela Vela, Liviu P. Dinu, Josef van Genabith. "Exploring the Use of Text Classification in the Legal Domain." arXiv, 2017. https://arxiv.org/abs/1710.09306

## Summary

This paper applies text classification to 126,865 rulings from the French Supreme Court (Court de Cassation), spanning the 1800s to 2016. The authors train a mean probability ensemble of Support Vector Machine classifiers, built on word unigram and bigram features, to predict three targets from a case description: the law area (eight chambers, such as chambre sociale and chambre criminelle), the ruling outcome (six or eight classes, such as cassation and rejet), and the decade in which the ruling issued. Before training, the authors mask each target label and its inflected forms from the case text, so the model works from a synthetic draft description that approximates what a lawyer would hold before a hearing, rather than from a text that already names the outcome. The ensemble reaches 96.8% accuracy on law area prediction, 98.6% F1 on the six-class ruling task and 95.8% F1 on the eight-class task, and 87.0% F1 on decade estimation. Each result exceeds the linear SVM baseline reported in the authors' earlier RANLP 2017 paper, which used the same dataset. Confusion matrix analysis shows that classes with few training instances, such as chambre mixte and non-lieu, remain the hardest to predict, which points to class imbalance as the main source of residual error.

## Key Concepts

- Mean probability ensemble: sums the class probability estimates from multiple SVM classifiers and predicts the class with the highest average, rather than taking a single classifier's top prediction.
- Label masking: removing a target label and its nominal and verbal forms from the case description text, to simulate a draft case description that has not yet been decided.
- Synthetic draft description: a case text stripped of outcome-revealing language, built to resemble the information a lawyer has before a ruling exists.
- Temporal text classification: predicting the period in which a text was written from its language alone, applied here to legal rulings by decade.

## Terminology

- **Chambre**: a division of the French Supreme Court, such as chambre sociale (labour) or chambre criminelle (criminal), used as the law area label.
- **Cassation / rejet / non-lieu**: ruling outcome labels, respectively quashing a lower decision, dismissing an appeal, and finding no grounds to proceed.
- **QPC (question prioritaire de constitutionnalite)**: a priority question of constitutionality, one of the ruling classes in the six-class setup.

## Architecture and Implementation

The system uses bag of words and bag of bigrams as features, feeding a set of SVM classifiers whose class probabilities are combined by simple averaging. The authors evaluate with stratified 10-fold cross-validation, chosen to match the evaluation protocol of the RANLP 2017 baseline paper and to account for class imbalance in the corpus. For ruling prediction, the paper runs two setups: a six-class version that keeps only the first word of each ruling label, and an eight-class version that keeps the full multi-word ruling label, such as cassation partielle sans renvoi. For decade estimation, all digits are stripped from case text, since digits could otherwise leak date information through cited law numbers.

## Code Examples

Not applicable. The paper reports experimental results using scikit-learn's SVM implementation and does not publish source code.

## Best Practices

- Mask the target label, including its verbal and nominal inflections, before training a classifier meant to predict that label from surrounding text.
- Use stratified cross-validation when class sizes are unbalanced, as ruling and law area labels are in this corpus.
- Report per-class confusion matrices alongside aggregate F1 scores, since low-frequency classes can hide behind a strong average score.
- Prefer a probability-averaging ensemble over a single classifier when robustness against estimation error matters more than training speed.

## Warnings and Anti-Patterns

- A classifier trained on unmasked case text risks learning to detect the outcome word itself rather than the reasoning that precedes it, which inflates accuracy without producing a usable draft-stage predictor.
- Classes with fewer than a few hundred examples, such as chambre mixte with 222 cases, produce unreliable predictions regardless of overall model strength.
- Decade boundaries are an arbitrary discretisation of a continuous timeline, so temporal classification results should be read as estimates rather than exact placements.

## Related Concepts

- [[tool-use]]
- [[evaluation]]
- [[legal-qa-ranking-svm-cnn-do-2017]]

## Future Work

The authors propose investigating how to induce a more accurate draft-form case description directly from the court's final case description, rather than relying on label masking as a proxy for what a lawyer would see before a ruling.

## References

- Sulea, O.M., Zampieri, M., Vela, M., van Genabith, J. 2017. Predicting the Law Area and Decisions of French Supreme Court Cases. RANLP.
- Aletras, N., Tsarapatsanis, D., Preotiuc-Pietro, D., Lampos, V. 2016. Predicting Judicial Decisions of the European Court of Human Rights: A Natural Language Processing Perspective. PeerJ Computer Science.
- Katz, D.M., Bommarito, M.J., Blackman, J. 2014. Predicting the Behavior of the Supreme Court of the United States: A General Approach. arXiv:1407.6333.
- Fan, R.E., Chang, K.W., Hsieh, C.J., Wang, X.R., Lin, C.J. 2008. LIBLINEAR: A Library for Large Linear Classification. Journal of Machine Learning Research.
