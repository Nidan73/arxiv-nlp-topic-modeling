# arXiv CS Topic Modeling (R)

Collects computer science abstracts from arXiv, cleans them, and fits a 10-topic LDA model in R.

## Scripts

1. `data_collection_api.r`: queries the arXiv API (`aRxiv`) for `cat:cs.*` in two-month windows from 2025-01-01 to today, 500 records per request, with retries and a backup CSV after each window, then removes duplicate ids.
2. `text_data_preprocessing.r`: lowercases the abstracts, expands contractions, keeps letters only, removes English stopwords (`tm`) and lemmatises (`textstem`).
3. `modeling_topic_lda.r`: builds a document-term matrix (terms of 3 or more letters that appear in at least 100 documents and at most 90% of them), fits Gibbs-sampled LDA with k = 10 (seed 1234, burn-in 1,000, 2,000 iterations), applies hand-written topic labels, and exports the top terms per topic, document-topic weights and word clouds.

## Outputs

`lda_topic_terms1.csv`, `lda_document_topics_labeled1.csv`, `wordclouds_all_topics1.pdf`, `topic_wordclouds_all_terms.pdf`, `lda_model.rds`, `dtm.rds` and `corpus.rds`. None of these are committed.

## Before running

The file names do not line up between the scripts. The collector writes `arxiv_cs_complete(2024-2025).csv`; preprocessing reads `arxiv_cs_complete(2020-2025).csv` and writes `token_text_arxiv_preprocessed.csv`; the modeling script reads `cleaned_text_arxiv_preprocessed.csv` (column `cleaned_text`) from an absolute path. Align the names and paths first.

## Packages

aRxiv, dplyr, lubridate, purrr, readr, stringr, textclean, textstem, tm, tokenizers, topicmodels, tidytext, broom, ggplot2, scales, tidyr, slam, reshape2, wordcloud, RColorBrewer.
