# 22i-1978_22i-1891_22i-1931_A-02

( REPORT )


Introduction:

Search engines are fundamental tools for information retrieval, especially in managing large volumes of data with minimal latency. This report outlines the development process of a basic search engine utilizing the MapReduce paradigm. It focuses on two primary tasks: Document Indexing and Query Processing, implemented within the Apache Hadoop MapReduce framework.

Document Indexing:

Document Indexing involves creating an index of terms present in the corpus along with their respective frequencies and document IDs. This process is split into mapper and reducer functions.

Mapper (document_indexing_mapper.py):


Function: Extracts words from each document and emits (word, document_id) pairs.
Implementation: Utilizes regular expressions to extract words from text and emits key-value pairs.
Reducer (document_indexing_reducer.py):

Function: Aggregates emitted pairs to calculate the frequency of each word in the corpus.
Implementation: Counts the occurrences of each word across documents and emits (word, frequency) pairs.
Indexer:
The Indexer computes the TF-IDF (Term Frequency-Inverse Document Frequency) for each term-document pair, providing a measure of the importance of a term in a document relative to its occurrence in the entire corpus. This process also involves mapper and reducer functions.

Mapper (indexer_mapper.py):

Function: Computes the TF-IDF values for each term-document pair.
Implementation: Calculates TF-IDF values for each word-document pair using the TF-IDF formula.
Reducer (indexer_reducer.py):

Function: Combines TF-IDF values emitted by mappers to generate a dictionary of TF-IDF values for each term.
Implementation: Aggregates TF-IDF values for each term across documents and produces a dictionary of TF-IDF values.
Query Processing:
Query Processing involves ranking documents based on their relevance to a given query. This process also comprises mapper and reducer functions.

Mapper (query_processor_mapper.py):

Function: Vectorizes the query and computes relevance scores for each document.
Implementation: Constructs a TF-IDF vector for the query and computes relevance scores for each document.
Reducer (query_processor_reducer.py):

Function: Ranks documents based on their relevance scores.
Implementation: Sorts documents based on their relevance scores in descending order.
Conclusion:
The development of a basic search engine using MapReduce involves implementing Document Indexing and Query Processing tasks. By leveraging the parallel processing capabilities of MapReduce, we can efficiently handle large-scale text corpora. The mapper and reducer functions facilitate parallelization and scalability, making it suitable for processing massive datasets. This project serves as a foundational step towards building more sophisticated search engines and highlights the effectiveness of distributed computing in information retrieval tasks.


SOME OF THE MAIN ASPECTS OF THE CODES ARE EXPLAIND BELOW:

Explanation:
The DocumentIndexingMapper class contains a method extract_words that takes a line of text from the input data. It splits the line into an article ID and section text, converts the text to lowercase, extracts words using regex, and yields key-value pairs where the key is a word and the value is the article ID.
The DocumentIndexingReducer class has a method count_documents that receives word-article pairs. It counts the number of unique articles each word appears in and returns a list of tuples containing the word and its count.


Explanation:
The IndexerMapper class defines a method compute_tfidf that calculates the TF-IDF value for each word in a document. It receives a tuple containing the word, document count, current article ID, and section text. It computes TF-IDF using the provided formula and yields key-value pairs where the key is the word and the value is a tuple containing the document ID and TF-IDF value.
The IndexerReducer class has a method combine_tfidf that receives TF-IDF values emitted by mappers. It combines these values into a dictionary where the key is the word and the value is its TF-IDF score.



Explanation:
The QueryProcessorMapper class has a method vectorize_query that converts the query into a TF-IDF vector. It splits the query into words, converts them to lowercase, and yields key-value pairs where the key is a word and the value is 1.
The QueryProcessorReducer class defines a method calculate_relevance that computes the relevance of each document to the query. It receives TF-IDF values emitted by mappers, constructs a query vector, computes the dot product between the query vector and document TF-IDF vectors, and yields the relevance score for each document.
