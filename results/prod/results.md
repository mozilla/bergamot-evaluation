# What is BLEU

[BLEU (BiLingual Evaluation Understudy)](https://en.wikipedia.org/wiki/BLEU) is a metric for automatically evaluating machine-translated text. The BLEU score is a number between zero and one that measures the similarity of the machine-translated text to a set of high quality reference translations. A value of 0 means that the machine-translated output has no overlap with the reference translation (low quality) while a value of 1 means there is perfect overlap with the reference translations (high quality).

It has been shown that BLEU scores correlate well with human judgment of translation quality. Note that even human translators do not achieve a perfect score of 1.0.

BLEU scores are expressed as a percentage rather than a decimal between 0 and 1.
Trying to compare BLEU scores across different corpora and languages is strongly discouraged. Even comparing BLEU scores for the same corpus but with different numbers of reference translations can be highly misleading.

However, as a rough guideline, the following interpretation of BLEU scores (expressed as percentages rather than decimals) might be helpful.

BLEU Score |	Interpretation
--- | ---
< 10 |	Almost useless
10 - 19 |	Hard to get the gist
20 - 29 |	The gist is clear, but has significant grammatical errors
30 - 40 |	Understandable to good translations
40 - 50 |	High quality translations
50 - 60 |	Very high quality, adequate, and fluent translations
\> 60 |	Quality often better than human

[More mathematical details](https://cloud.google.com/translate/automl/docs/evaluate#the_mathematical_details)

Source: https://cloud.google.com/translate/automl/docs/evaluate#bleu


BLEU is the most popular becnhmark in academia, so using BLEU allows us also to compare with reserach papers results and competitions (see [Conference on Machine Translation Conference (WMT)](http://statmt.org/wmt21/)).

Read [this article](https://www.rws.com/blog/understanding-mt-quality-bleu-scores/) to better understand what BLEU is and why it is not perfect.

# What are these benchmarks

## Translators

1. **bergamot** - uses compiled  [bergamot-translator](https://github.com/mozilla/bergamot-translator)  (wrapper for marian that is used by Firefox Translations web extension)
2. **marian** - uses compiled [marian](https://github.com/marian-nmt/marian-dev) (translation engine bergamot-translator is based on)
3. **google** - uses Google Translation [API](https://cloud.google.com/translate)
4. **microsoft** - uses Azure Cognitive Services Translator [API](https://azure.microsoft.com/en-us/services/cognitive-services/translator/)

Translation quality of Marian and Bergamot is supposed to be very similar.

## Method

We use official WMT ([Conference on Machine Translation](http://statmt.org/wmt21/)) parallel datasets. Available datsets are discovered automatically based on a language pair.

We perform translation from source to target langauge using one of 4 translation systems and then compare the result with the dataset reference and calculate BLEU score.

Evaluation is done using [SacreBLEU](https://github.com/mjpost/sacrebleu) tool which is reliable and widely used in academic world.

Both absolute and relative differences in BLEU scores between Bergamot and other systems are reported.

# Evaluation results

`avg` = average on all datasets



## avg

| Translator/Dataset | cs-en | en-cs | en-de | en-es | en-et | es-en | et-en |
| --- | --- | --- | --- | --- | --- | --- | --- |
| bergamot | 29.44 | 23.77 | 30.56 | 34.37 | 25.20 | 33.40 | 31.00 |
| marian | 29.35 (-0.09, -0.31%) | 23.56 (-0.21, -0.87%) | 30.56 (0.00, 0.00%) | 34.42 (+0.05, +0.15%) | 25.30 (+0.10, +0.40%) | 33.43 (+0.03, +0.10%) | 31.10 (+0.10, +0.32%) |
| google | 31.33 (+1.89, +6.43%) | 25.58 (+1.81, +7.61%) | 31.84 (+1.28, +4.18%) | 36.17 (+1.80, +5.24%) | 26.60 (+1.40, +5.56%) | 34.43 (+1.03, +3.09%) | 32.10 (+1.10, +3.55%) |
| microsoft | N/A | N/A | 32.43 (+1.87, +6.12%) | 35.53 (+1.17, +3.39%) | 27.60 (+2.40, +9.52%) | 33.10 (-0.30, -0.90%) | 34.10 (+3.10, +10.00%) |

![Results](img/avg.png)

## cs-en

| Translator/Dataset | wmt08 | wmt09 | wmt10 | wmt11 | wmt12 | wmt13 | wmt14 | wmt15 | wmt16 | wmt17 | wmt18 | wmt20 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| bergamot | 24.30 | 27.40 | 27.90 | 28.10 | 26.70 | 30.50 | 34.80 | 31.80 | 33.40 | 30.20 | 31.40 | 26.80 |
| marian | 24.40 (+0.10, +0.41%) | 27.50 (+0.10, +0.36%) | 27.90 (0.00, 0.00%) | 28.10 (0.00, 0.00%) | 26.60 (-0.10, -0.37%) | 30.20 (-0.30, -0.98%) | 34.90 (+0.10, +0.29%) | 31.60 (-0.20, -0.63%) | 33.30 (-0.10, -0.30%) | 30.10 (-0.10, -0.33%) | 31.30 (-0.10, -0.32%) | 26.30 (-0.50, -1.87%) |
| google | 26.30 (+2.00, +8.23%) | 29.90 (+2.50, +9.12%) | 30.50 (+2.60, +9.32%) | 30.20 (+2.10, +7.47%) | 28.60 (+1.90, +7.12%) | 32.40 (+1.90, +6.23%) | 38.00 (+3.20, +9.20%) | 33.60 (+1.80, +5.66%) | 34.80 (+1.40, +4.19%) | 31.20 (+1.00, +3.31%) | 32.10 (+0.70, +2.23%) | 28.40 (+1.60, +5.97%) |
| microsoft | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A |

![Results](img/cs-en.png)

## en-cs

| Translator/Dataset | wmt08 | wmt09 | wmt10 | wmt11 | wmt12 | wmt13 | wmt14 | wmt15 | wmt16 | wmt17 | wmt18 | wmt19 | wmt20 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| bergamot | 19.20 | 20.80 | 20.90 | 20.50 | 18.90 | 23.50 | 28.60 | 25.10 | 25.60 | 23.50 | 22.60 | 27.20 | 32.60 |
| marian | 19.00 (-0.20, -1.04%) | 20.80 (0.00, 0.00%) | 20.90 (0.00, 0.00%) | 20.40 (-0.10, -0.49%) | 18.90 (0.00, 0.00%) | 23.10 (-0.40, -1.70%) | 28.60 (0.00, 0.00%) | 24.90 (-0.20, -0.80%) | 25.40 (-0.20, -0.78%) | 23.10 (-0.40, -1.70%) | 22.60 (0.00, 0.00%) | 26.70 (-0.50, -1.84%) | 31.90 (-0.70, -2.15%) |
| google | 20.50 (+1.30, +6.77%) | 22.60 (+1.80, +8.65%) | 22.40 (+1.50, +7.18%) | 23.00 (+2.50, +12.20%) | 20.70 (+1.80, +9.52%) | 25.20 (+1.70, +7.23%) | 31.20 (+2.60, +9.09%) | 26.80 (+1.70, +6.77%) | 28.30 (+2.70, +10.55%) | 24.70 (+1.20, +5.11%) | 24.40 (+1.80, +7.96%) | 27.20 (0.00, 0.00%) | 35.50 (+2.90, +8.90%) |
| microsoft | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A |

![Results](img/en-cs.png)

## en-de

| Translator/Dataset | wmt08 | wmt09 | wmt10 | wmt11 | wmt12 | wmt13 | wmt14 | wmt15 | wmt16 | wmt17 | wmt18 | wmt19 | wmt20 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| bergamot | 23.30 | 22.70 | 25.80 | 22.90 | 23.90 | 27.60 | 29.30 | 32.30 | 38.40 | 30.70 | 45.10 | 41.40 | 33.90 |
| marian | 23.50 (+0.20, +0.86%) | 22.90 (+0.20, +0.88%) | 25.90 (+0.10, +0.39%) | 23.00 (+0.10, +0.44%) | 23.90 (0.00, 0.00%) | 27.70 (+0.10, +0.36%) | 29.50 (+0.20, +0.68%) | 32.30 (0.00, 0.00%) | 38.50 (+0.10, +0.26%) | 30.80 (+0.10, +0.33%) | 45.10 (0.00, 0.00%) | 41.60 (+0.20, +0.48%) | 32.60 (-1.30, -3.83%) |
| google | 23.70 (+0.40, +1.72%) | 23.60 (+0.90, +3.96%) | 26.50 (+0.70, +2.71%) | 24.10 (+1.20, +5.24%) | 24.70 (+0.80, +3.35%) | 28.80 (+1.20, +4.35%) | 30.90 (+1.60, +5.46%) | 33.70 (+1.40, +4.33%) | 38.60 (+0.20, +0.52%) | 31.50 (+0.80, +2.61%) | 47.80 (+2.70, +5.99%) | 43.50 (+2.10, +5.07%) | 36.50 (+2.60, +7.67%) |
| microsoft | 24.00 (+0.70, +3.00%) | 23.90 (+1.20, +5.29%) | 27.20 (+1.40, +5.43%) | 23.70 (+0.80, +3.49%) | 25.30 (+1.40, +5.86%) | 28.80 (+1.20, +4.35%) | 32.20 (+2.90, +9.90%) | 34.30 (+2.00, +6.19%) | 40.50 (+2.10, +5.47%) | 33.10 (+2.40, +7.82%) | 48.70 (+3.60, +7.98%) | 43.80 (+2.40, +5.80%) | 36.10 (+2.20, +6.49%) |

![Results](img/en-de.png)

## en-es

| Translator/Dataset | wmt08 | wmt09 | wmt10 | wmt11 | wmt12 | wmt13 |
| --- | --- | --- | --- | --- | --- | --- |
| bergamot | 28.90 | 29.70 | 36.60 | 37.70 | 38.60 | 34.70 |
| marian | 28.90 (0.00, 0.00%) | 29.80 (+0.10, +0.34%) | 36.70 (+0.10, +0.27%) | 37.70 (0.00, 0.00%) | 38.70 (+0.10, +0.26%) | 34.70 (0.00, 0.00%) |
| google | 30.00 (+1.10, +3.81%) | 30.90 (+1.20, +4.04%) | 38.80 (+2.20, +6.01%) | 39.90 (+2.20, +5.84%) | 40.50 (+1.90, +4.92%) | 36.90 (+2.20, +6.34%) |
| microsoft | 29.90 (+1.00, +3.46%) | 30.70 (+1.00, +3.37%) | 37.80 (+1.20, +3.28%) | 39.10 (+1.40, +3.71%) | 40.00 (+1.40, +3.63%) | 35.70 (+1.00, +2.88%) |

![Results](img/en-es.png)

## en-et

| Translator/Dataset | wmt18 |
| --- | --- |
| bergamot | 25.20 |
| marian | 25.30 (+0.10, +0.40%) |
| google | 26.60 (+1.40, +5.56%) |
| microsoft | 27.60 (+2.40, +9.52%) |

![Results](img/en-et.png)

## es-en

| Translator/Dataset | wmt08 | wmt09 | wmt10 | wmt11 | wmt12 | wmt13 |
| --- | --- | --- | --- | --- | --- | --- |
| bergamot | 27.20 | 29.50 | 35.90 | 34.30 | 38.20 | 35.30 |
| marian | 27.20 (0.00, 0.00%) | 29.50 (0.00, 0.00%) | 35.90 (0.00, 0.00%) | 34.40 (+0.10, +0.29%) | 38.20 (0.00, 0.00%) | 35.40 (+0.10, +0.28%) |
| google | 28.30 (+1.10, +4.04%) | 31.60 (+2.10, +7.12%) | 37.00 (+1.10, +3.06%) | 35.20 (+0.90, +2.62%) | 38.80 (+0.60, +1.57%) | 35.70 (+0.40, +1.13%) |
| microsoft | 26.80 (-0.40, -1.47%) | 29.60 (+0.10, +0.34%) | 35.40 (-0.50, -1.39%) | 33.70 (-0.60, -1.75%) | 37.80 (-0.40, -1.05%) | 35.30 (0.00, 0.00%) |

![Results](img/es-en.png)

## et-en

| Translator/Dataset | wmt18 |
| --- | --- |
| bergamot | 31.00 |
| marian | 31.10 (+0.10, +0.32%) |
| google | 32.10 (+1.10, +3.55%) |
| microsoft | 34.10 (+3.10, +10.00%) |

![Results](img/et-en.png)