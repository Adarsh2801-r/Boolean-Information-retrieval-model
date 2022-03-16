# Boolean-Information-retrieval-model

## Architecture of the information retrieval model

<p align="center">
  <img src="https://user-images.githubusercontent.com/66625110/158529803-f4cba367-d838-4b2b-9dd5-0843f7ae85ce.jpg"/>
</p>

## Procedure 

### PRE-PROCESSING 
**Document preprocessing :** 
1) Involves tokenizing, removing stopwords, case folding, stemming (PorterStemmer used) and building the inverted index structure. 
2) The function preprocess() takes path of folder where documents are stored as input and builds </br>
   a) The inverted index data structure which maps each term with list of documents in which the term appears </br>
   b) Doc_map which stores doc_id ==> doc_name </br>
   c) Set of vocabulary terms </br>
```
corpus="/content/corpus" # give path of location of folder containing the docs
preprocess(corpus)
# Creating vocabulary set from posting_list keys
vocab = set(posting_list.keys())
```
**Query preprocessing :** </br>
1) Tokenizes the query terms </br>
2) Replaces wildcard terms with equivalent boolean expression of terms</br>
3) Spelling correction of terms using edit-distance method </br>

To test the query-preprocessing and obtain list of tokens, run the following code snippet in the .ipynb file </br>
```
query = input("Enter query: ")
for term in query.split(" "):
  if('*' in term):
    query=query.replace(term,match_terms(term))
q_tokens = query_preprocess(query)
print(q_tokens)

```

### QUERYING

Expects a *well formed query* to be given as input

**Well-formed query:** 

*   Every word/symbol must be space seperated
*   The following symbols represent boolean operators : **AND = & , OR = | , NOT = ~**
*   If parenthesis are used, it must be ensured that they are properly balanced
*   In absence of parenthesis, the precedence order followed by operators is ~ > & > |
* Supports wildcard entries/terms of following formats: A\* , \*A , A\*B , A\*B\*C 

The below code snippet can be run obtain the docs satisfying the query </br>
```
query = input("Enter query: ")
for term in query.split(" "):
  if('*' in term):
    query=query.replace(term,match_terms(term))
q_tokens = query_preprocess(query)
ids=evaluate_and_match(q_tokens)
# Returns list of names of documents satisfying the query
get_docs(ids)

```



    
