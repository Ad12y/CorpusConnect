# CorpusConnect
Powerful Python tool for corpus analysis, term network generation, and textual insight discovery.

A comprehensive text analysis tool that processes a corpus of text to generate a network of term co-occurrences. Here's a detailed breakdown of its functionality:
1. Initialization and Configuration

The class is initialized with several configurable parameters, including options for text flattening, handling parentheses, and removing leaf nodes.
It also sets up session management and callback functionality, likely for handling large-scale or distributed processing.

2. Text Cleaning and Preprocessing

The input text (stored in map_of_lines) undergoes several cleaning operations:

Accent removal (optional)
Conversion to lowercase
The cleaned text is stored in a sorted dictionary (map_tree)



3. Tokenization

The cleaned text is tokenized using a custom UmigonTokenizer.
There's special handling for content within parentheses, which can be optionally skipped.

4. N-gram Generation

The code generates n-grams (sequences of n words) up to a specified maximum length.
It uses a SentenceLikeFragmentsDetector to break the text into sentence-like units before n-gram generation.
Duplicate n-grams within a line are removed to prevent over-representation.

5. Stopword Removal

A StopWordsRemover is initialized with language-specific stopwords.
User-supplied stopwords can be added, and scientific stopwords are included for relevant corpora.
Stopword removal is performed in two rounds, once before and once after lemmatization.

6. Lemmatization

If enabled, each n-gram is lemmatized (reduced to its base form) using a language-specific lemmatizer.
This helps in grouping related terms and reducing vocabulary size.

7. Term Frequency Analysis

The code counts the frequency of each n-gram across the entire corpus.
It applies filters based on minimum character count and frequency thresholds.
The top MOST_FREQUENT_TERMS (set to 2000) are retained for further analysis.

8. Co-occurrence Calculation

The code calculates how often terms appear together within the same line or sentence.
It uses a custom PerformCombinationsOnNGrams class to efficiently generate all possible co-occurrences.
Infrequent co-occurrences are filtered out based on the total number of co-occurrences found.

9. Graph Construction

A network graph is constructed using the NetworkX library.
Nodes represent terms, with attributes for term frequency.
Edges represent co-occurrences, with attributes for co-occurrence frequency and strength.
Edge weights are calculated using either raw co-occurrence counts or PMI (Pointwise Mutual Information), depending on the specified correction method.
Edge weights are rescaled to a 0-10 range for consistency.

10. Graph Optimization

The code includes logic to handle cases with too many edges relative to nodes.
If the edge count exceeds a threshold, it retains only the most significant edges to keep the graph manageable.

Throughout the process, there are several optimizations and filters applied to manage computational complexity and ensure the resulting graph is meaningful and not overwhelmed by noise or insignificant relationships.
This tool provides a powerful way to analyze large text corpora, identifying key terms and their relationships. The resulting graph can be used for various applications, including topic modeling, content analysis, and information retrieval enhancement.
