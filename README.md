# Project Descriptions
The projects used as notebooks are listed here. The details of the projects are given in the relevant sections.

## Embedding_Models
The mechanism and impact of tokenizers in transformers are studied in this project. We use `sentence-transformers` library from https://sbert.net/
and observe different parts of the transformer model to apply and output contextual embeddings after tokenizing.

## Tokenizers
In this notebook, 3 different tokenizers have been implemented from HuggingFace library - BPE, WordPiece and Unigram. These tokenizers produce different tokens with the same input text. The effects can be studied through this notebook

## Tokenization_Practicals
Here, we can see the practical implications of different tokenization methods. How different pretrained models tokenize and capture semantics differently. A very simple yet sophisticated case of 
semantics can be shown with these sets of query and documents. Suppose we have a large set of documents where each document has descriptions of a set of clothes bought for particular prices, like :

doc_1 -> "Sweatshirts for 45$"
doc_2 -> "Jeans for 35$"
		.
		.
		.
doc_n -> "Earmuffs for 20$"

Now when we have a query `q` -> "winter clothes under 45$", it should fetch the relevant documents following the appropriate semantics of strictly `winter clothes` and `clothes under 45$`. 
But sometimes the traditional encodings fail to capture these subtleties where the encodings do not separately retain the numeric or date or any other non-textual entities. So in this notebook, we look into 
techniques to capture as much semantics as possible using the vector embeddings of the models and some filtering mechanisms using a vector database storage (Like : Qdrant)

## Measuring_Search_Relevance

When we store our documents and their embeddings in a vector database like `Qdrant`, and we can use textual queries to fetch semantically similar documents from the db, we have multiple columns to choose from, to compare
the query semantics with the selected column records. To identify the most appropriate column to compare against, we first have to `evaluate` the `relevance results` on multiple columns against a **ground truth dataset**. This evaluation 
shows us how choice of a column affects the performance of the same set of queries for our particular interest. In this notebook, we explore such techniques and options of evaluation and relevance rankings against ground truth datasets.


# Setup

- Create a virtualenv environment using `python -m virtualenv path/to/your/virtualenv/<virtualenv_name>`
- Activate the virtualenv
- Prepare the virtualenv with appropriate libraries : `pip install -r requirements.txt`
- Download datasets inside `/data/` folder when necessary

## Qdrant (The Vector Database)

- Download docker image of **Qdrant** for local use by running `docker pull qdrant/qdrant`
- Qdrant quickstart guide : `https://qdrant.tech/documentation/quickstart/`
- Prepare qdrant container using 
`docker run -p 6333:6333 -p 6334:6334 \
    -v $(pwd)/qdrant_storage:/qdrant/storage:z \
    qdrant/qdrant`