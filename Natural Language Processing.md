# [Natural Language Processing (NLP)](../Spring_24/natural_language_processing.pdf)
- Humans communicate primarily through language
- Vast amounts of knowledge is stored as machine readable natural language text
	- This information is inaccessible to traditional computing methods which require structured data
- NLP provides a method to process textual information and therefore a method to access this human knowledge
- Speech and text is becoming an important form of human-computer interaction

# NLP Applications
- Information retrieval
	- Accessing the documents/text that are relevant to you
- Question answering
	- Providing answers to questions you ask
- Chat-bots
	- Conversational agents for a variety of purposes(question answering, etc)
- Sentiment Analysis
	- Determining the sentiment (positive, negative, neutral) of text
- Machine Translation
	- Automatically translating from one language to another
- Text Summarization
	- Creating a summary of multiple and/or lengthy text

# NLP Tasks
- Applications can be solved as pipeline of NLP tasks
	- Question answering 
		- Can pose as Causal Language Modeling (Generative/Abstractive QA)
			- Just one step – predict the next most probable token
		- Or, a pipelined approach: (Extractive QA)
			- Information Retrieval to retrieve relevant documents
			- Snippet Extraction to retrieve relevant sentences
			- Span detection to retrieve the answer within a sentence

# Token Classification Tasks
- The goal of token classification tasks is to generate labels for each input token
- "Text" may consist of multiple words and may be phrases, sentences, Tweets, posts, paragraphs, documents, etc...
- Examples include:
	- Part of speech tagging, named entity recognition, word sense disambiguation, de-identification, etc.

# NLP Pipeline
![[nlp_pipeline.png]]

# Pyramid of Language Meaning
- Morphological
	- Captures sub-word meaning, such as prefixes and suffixes 
- Lexical
	- Captures individual words (called unigrams), pairs of words (called bi-grams) or sequences of n words (referred to as ngrams) 
- Syntactic
	- Syntactic information captures how words are structured within a sentence or phrase, such as part of speech (POS) tags indicating whether a word is a noun, verb, adjective, etc. 
- Semantic
	- Captures the meaning of a word, such as whether it refers to a person's name, a location, a disease, etc. 
- Discourse
	- Captures information about how sentences, paragraphs, or documents are structured, such as document sections or document types 
![[pyramid_language_meaning.png]]

![[pyramid_language_meaning_example.png]]

## Featurization
- The goal of featurization is to represent text as numeric values which can be used for classifcation
- What a "sample" is depends on the application
- Typical samples are:
	1. Words(Terms, Tokens)
		- A sample is a token which may be a word or multi-word term
		- For token classification tasks
	2. Text Snippets, Sentences, Documents
		- Consists of multiple words
		- For text classification tasks

## Word Vectors
- One-hot Vectors (Sparse - Vocabulary Size)
	- Vectors are all zero except for a single one at the word’s index
- Co-occurrence vectors (Sparse - Vocabulary Size)
	- Iterate over a corpus and collect co-occurrence information. At each cooccurrence increment co-occurrence count at word-word index
- Word Embeddings (Dense – Fixed Size)
	- Iterate over a corpus and use a neural network to create vector representations based on word co-occurrences

“You shall know a word by the company it keeps” ~Firth

### One-hot Vectors
Assign each word an index and encode vector with a one at that index


|         | I   | walked | the | dog | in  | morning | cat | evening |
| ------- | --- | ------ | --- | --- | --- | ------- | --- | ------- |
| I       | 1   | 0      | 0   | 0   | 0   | 0       | 0   | 0       |
| walked  | 0   | 1      | 0   | 0   | 0   | 0       | 0   | 0       |
| the     | 0   | 0      | 1   | 0   | 0   | 0       | 0   | 0       |
| dog     | 0   | 0      | 0   | 1   | 0   | 0       | 0   | 0       |
| in      | 0   | 0      | 0   | 0   | 1   | 0       | 0   | 0       |
| morning | 0   | 0      | 0   | 0   | 0   | 1       | 0   | 0       |
| cat     | 0   | 0      | 0   | 0   | 0   | 0       | 1   | 0       |
| evening | 0   | 0      | 0   | 0   | 0   | 0       | 0   | 1       |
Basic word representation –very large and very sparse vector space. No representation of word meaning

### Co-occurrence Vectors 
"I walked the dog in the morning"
![[cooccurrence_vectors_example.png]]

### Text Segment Vectors
- To represent text segments, sentences, documents, etc.. We typically assume that the text is the combined meaning of its constituent words 
	1. Bag of words Representation = take the sum of average constituent one-hot vectors
	2. Term frequency - Inverse Document Frequency (TF-IDF) vector = TF-IDF value of each of its constituent terms. TF-IDF value is the number of times a word occurs in that document divided by the number of times it occurs in all documents
	3. Mean or sum of word embeddings

#### TF-IDF Vectors
![[tf_idf_vectors.png]]

#### Word Embeddings
- Co-occurrence vectors are large, sparse, and noisy. They contain integer values
- Word embeddings are small(er), dense, and less noisy. They contain real number values

Word embeddings are dense vectors of real-values rather than sparse vectors of binary or integer values. Dimensionality varies, but typically between 50 and 500 dimensions

- Word Embeddings are vectors which are the learned internal weights of an artificial neural network
- The network is trained to predict either:
	1. The context given a word (skip-gram)
	2. a word given the context (continuous bag of words (cbow))

"You shall know a word by the company it keeps" ~Firth

![[word_embeddings.png]]

# Recap
- Words can be represented as:
	- One-hot encoding - no meaning is encoded, high dimensional, sparse
	- Co-occurrence vectors - some meaning is encoded, high dimensional, sparse
	- Word embeddings - meaning is encoded, low dimensional, dense

- Text segments can be represented as
	1. Bag of Words Representation = take sum or average constituent one-hot vectors
	2. Term Frequency - Inverse Document Frequency (TF-IDF) vector = TF-IDF value of each of its constituent terms. TF-IDF value is the number of times a word occurs in that document divided by the number of times it occurs in all documents
	3. Mean of sum of word embeddings

# Token Classification Example: Named Entity Recognition
- Named Entity Recognition is a token classification task
- For each token, decide if it is an entity of interest (e.g. a person's name)
![[token_classification_example.png]]


# Language Models
- Language models have become ubiquitous in NLP
	- Language models are deep neural networks trained on massive corpora
- Language models generate contextualized word embeddings and (sometimes) text segment embeddings
	- These embeddings consider both the meaning of a word (using word embeddings) and its surrounding context to generate a vector representation of the word's meaning it is current context
	- I ate by the river **bank** vs. I deposited money in the **bank**
	- "bank" has the same word embedding for both contexts, language models add context to the embedding of a word
- A language model is therefore a trained deep neural network that generates a vector representation of a sequence of words

- A sentence is input as a series of static word vectors (e.g. word embeddings)
- The language model does a transformation based on its learned weights
- The sentence is output as a series of contextualized embeddings

Then, you can use whatever classifier you want using the contextualized embeddings as input with or without other features

Popular language models include:
- eLMO - BiLSTM based
- BERT - Transformer based
- GPT - Transformer based
- LLaMa - Transformer based

Lots of others:
- ERNIE
- XLNet
- Megatron

## How do the models learn?
**Self-Supervised Learning**
- These models are pre-trained to predict the next word in a sequence
	- And also sometimes the next sentence in a sequence
- This is really clever and it means that any text can be used as labeled training data

You can use whatever classifier you want. The embeddings are just features

Typically though, neural networks are used, since it allows backpropagation through the whole network (although this is possible with many other classifiers too)

