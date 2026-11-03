# Methods Notes

## Experimental question

How do a financial word-list baseline, TF-IDF with Logistic Regression, and a pretrained financial-language model compare in classifying financial passages as positive, negative, or neutral?

## Task

The experiment will use supervised, three-class financial sentiment classification. Each example will contain a passage and a human reference label: positive, negative, or neutral. Predictions will be evaluated against those reference labels.

The label definitions and financial perspective will follow the selected dataset's annotation guidelines. The dataset audit will establish how its annotators distinguish directional financial implications, neutral information, and ambiguous or mixed passages. Existing labels will be preserved, with exclusions and transformations documented.

## Data preparation

Financial PhraseBank is the initial candidate, subject to an audit before final selection. The audit will record the dataset source and version, fields, annotation procedure, agreement subsets, example counts, class distribution, missing values, and available document metadata. It will check exact and likely near duplicates, conflicting labels, and overlap between subsets.

A reproducible pilot sample of approximately 100 passages will be inspected to understand label meaning and recurring challenges. The sample and selection procedure will be saved. Raw data will remain unchanged, and preparation steps will produce traceable outputs with stable example identifiers.

## Splitting and model selection

The experiment will save fixed training, validation, and test assignments, with the exact allocation chosen after inspecting data size, class balance, and grouping constraints. Duplicate passages will stay together. Passages from the same source document will also stay together where document identifiers permit it; missing metadata will be documented as a limitation.

Learned preprocessing and model fitting will use training data only. Validation data will guide hyperparameter selection and threshold tuning. Configurations will be frozen before final test evaluation, and all approaches will be compared on the same final test examples.

Candidate language-model checkpoints will be checked for sentiment-training overlap with evaluation examples. A new random split does not resolve prior exposure by a downloaded classifier. The final evaluation route will be selected after checking provenance, and any remaining uncertainty will be reported alongside the results.

## Approach 1: Financial word-list baseline

The initial dictionary candidate is the Loughran–McDonald financial vocabulary. Its version and usage terms will be recorded. The implementation will specify token matching, positive and negative scoring, negation handling, and the thresholds that convert scores into three labels. Thresholds will be selected using development data.

This approach provides an interpretable reference: individual dictionary matches can be inspected to explain a passage's score.

## Approach 2: TF-IDF with Logistic Regression

A single pipeline will fit TF-IDF on training passages and train a multiclass Logistic Regression classifier using human labels. A small comparison will examine word-only versus word-and-short-phrase features and regularization strength. Validation macro-F1 will guide the selected configuration.

This approach tests whether learning predictive word and phrase patterns improves on fixed dictionary scoring.

## Approach 3: Pretrained financial-language model

FinBERT is the starting candidate. The exact checkpoint, revision, training history, tokenizer, output-label mapping, and input-length handling will be documented before evaluation. The decision to use an existing sentiment checkpoint or fine-tune a suitable checkpoint will depend on training provenance, data availability, and computational requirements.

If fine-tuning is used, training examples will update the model and validation examples will guide configuration selection. This approach tests whether contextual text representations provide useful improvements over the simpler methods.

## Metrics and error analysis

Macro-F1 will be the primary metric so each sentiment class contributes equally to the reported score. Results will also include accuracy, class counts, per-class precision, recall and F1, and confusion matrices. A majority-class baseline will select its predicted class using training labels.

A hyperparameter-performance table or figure will accompany the selected configuration. Error analysis will compare correct and incorrect predictions across methods, focusing on negation, numerical comparisons, expectations, mixed evidence, and neutral versus positive statements. Runtime and hardware requirements will be recorded where useful.

## Reproducibility

The experiment will record package versions, random seeds, dataset versions, checkpoint revisions, preparation decisions, split assignments, model configurations, predictions, and figure-generation commands. An experiment log will connect each run to its settings and outputs.

## Decisions to resolve during the dataset audit

- Dataset configuration and annotation perspective.
- Duplicate handling and available source-document grouping.
- Training, validation, and test allocation.
- Checkpoint provenance and the final evaluation route.
- Dictionary scoring rules and the hyperparameter search ranges.

These notes describe the planned procedure. Dataset selection and implementation details will be updated as the audit and experiments establish them.
