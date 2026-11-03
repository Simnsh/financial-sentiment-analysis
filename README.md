# CS150 Financial Sentiment Analysis

This project compares three approaches for classifying English financial passages as **positive**, **negative**, or **neutral**. The experiment will examine predictive performance, common errors, and whether more complex methods provide useful improvements.

## Experimental question

How do a financial word-list baseline, TF-IDF with Logistic Regression, and a pretrained financial-language model compare in classifying financial passages as positive, negative, or neutral?

## Approaches

1. **Financial word-list baseline:** Score passages using a financial dictionary, with documented word matching, negation handling, and classification thresholds.
2. **TF-IDF with Logistic Regression:** Represent passages using word and short-phrase features and train a multiclass classifier against human reference labels.
3. **Pretrained financial-language model:** Evaluate a suitable financial-language checkpoint, with FinBERT as the initial candidate. Check its training provenance before choosing a checkpoint and deciding whether to fine-tune it.

These methods allow a comparison between transparent dictionary scoring, a learned classifier using sparse text features, and a contextual language model.

## Data and evaluation plan

Financial PhraseBank is the initial dataset candidate. The first data milestone is to inspect its labels, annotation perspective, class distribution, duplicates, and available metadata before selecting the final dataset configuration.

Training, validation, and test assignments will be saved for reproducibility. Duplicate passages and related source documents will stay in the same split where identifiers are available. Checkpoint training overlap will be assessed before claiming performance on unseen examples. Model selection will use development data, with the final test set reserved for the final comparison.

The primary metric will be macro-F1, supplemented by accuracy, per-class precision, recall and F1, and confusion matrices. A majority-class baseline will provide a reference. Error analysis will examine concrete successes and failures, including negation, numerical comparisons, mixed evidence, and neutral statements.

## Current status

The experimental question and initial Methods notes are documented. Dataset auditing, environment setup, and model implementation are pending.

See [Methods notes](METHODS.md) for the planned experimental procedure and decisions to resolve.
