# Search Engine from Scratch

A search engine built from the ground up in Python — crawler, positional inverted index, and TF-IDF ranking, no external search/indexing libraries.

## About

Given a starting URL, this crawls a live website, builds a searchable index of everything it finds, and answers queries — from single words up to full natural-language sentences — ranked by relevance.

## How it works

- **Crawler** — a BFS-style crawler that fetches pages, extracts text with BeautifulSoup, and follows links matching a given URL pattern, up to a configurable depth. Demonstrated crawling Wikipedia from `en.wikipedia.org/wiki`.
- **Indexing** — builds a *positional* inverted index: for every term, which documents it appears in and at which positions, after lowercasing, stemming (Porter stemmer), and stopword removal.
- **Ranking** — computes TF-IDF scores for every term/document pair (term frequency × smoothed inverse document frequency).
- **Querying** — supports single-word search, boolean AND/OR/NOT between terms, and full-sentence search. Sentence search cascades through fallbacks when the exact query has no matches: strict AND across all terms → OR across all terms → WordNet-synonym expansion with AND → WordNet-synonym expansion with OR — so a query degrades gracefully instead of returning nothing.

## Example

Crawling Wikipedia and querying `"play games on your phone"` returns ranked, scored matches with their real source URLs — pages under `meta.wikimedia.org` and `foundation.wikimedia.org` — ordered by TF-IDF relevance.

## Stack
Python · requests · BeautifulSoup · NLTK (stopwords, Porter stemmer, WordNet) · NumPy
