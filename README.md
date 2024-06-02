# readqg
The training/inference/evaluation codes for ReadQG.

## Document-centric pairs 
We first built a document-centric pairs from MSMARCO Passage ranking dataset.
We use the pseudo labels calculated by SBERT: [hard-negative](cross-encoder-ms-marco-MiniLM-L-6-v2-scores.pkl.gz). More details can be found in [Huggingface](https://huggingface.co/datasets/sentence-transformers/msmarco-hard-negatives)

This preprocessing code include (1) document-centric aggregation amd (2) rescaling with MinMax.
```
python src/data/nils.py \
  --input_pkl <hard-negative.pkl> \
  --collection <msmarco-passage-corpus.jsonl> \
  --queries <queries.jsonl> \
  --min_n 2 --max_n 10 \
  --output_jsonl <saved-path.jsonl>
```
Here is an example:
```python3
{
    "passage": "Marjorie Morningstar (novel) First edition (publ. Doubleday) Marjorie Morningstar is a 1955 novel by Herman Wouk, about a woman who wants to become an actress. In 1958, the book was made into a Hollywood feature movie starring Natalie Wood, also titled Marjorie Morningstar.", 
    "positive": ["who wrote marjorie morningstar?", "founder of morningstar", "what is morningstar direct", "doubleday publisher", "who is marjorie winks", "meaning of name marjorie"], 
    "negative": ["who is marjorie bach", "vhcox morningstar", "apache morningstar", "what year was the first phone book publ", "when was the new edition movie made", "when was the little prince book publ", "where is marjorie congdon", "what does first anchor books edition", "what dashiell hammett mystery novel was made into a classic film", "what is morningstar economic moat"], 
    "positive_score": [1.0, 0.5943120530026602, 0.5729755012543724, 0.5485032574115749, 0.5227704165498473, 0.5184035127541687], 
    "negative_score": [0.5019643744555538, 0.48854984330862333, 0.48256438933225276, 0.48065411202876335, 0.4775776822910094, 0.3258133069202288, 0.3125255552925462, 0.30954225698795557, 0.2606488628335376, 0.2474956552307656]
}
```

