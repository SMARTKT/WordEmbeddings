# WordEmbeddings

googledrive link : https://tinyurl.com/SWVECembeddings



# Instructions

## To download the embeddings :
1. Go to the google drive link above and download all of the files in the folder.
2. Place the embeddingClass.py file of the repository in the same path where the embedding files were downloaded.


After downloading word embeddings, dependencies can be installed with the help of requirements.txt in the repository.

```
pip install -r requirements.txt
```


## Using the word embeddings : 

The class for loading and using word embeddings is embeddingClass.py. Below are instructions and examples for some of the uses : 

### Importing embeddingModel

Import embeddingModel and EpochSaver from embeddingClass.py as

```
from embeddingClass import embeddingModel, EpochSaver
```


### Using embeddingModel

embeddingModel class provides four different word embeddings : 
1. cbow
2. elmo
3. elmo-max
4. elmo-concat

Of these, the word vector dimension for cbow, elmo and elmo-max is of size 200 and of size 400 for elmo-concat.

For each of these word embeddings, functions are provided to get vectors of each word given a sentence, to get a vector for a sentence(as average over vectors of words of the sentence) and to get a dictionary with words of sentence as keys and their vectors as values (vectors for words occuring multiple times are averaged).


### Example : 

Lets say the sentence is "will this computer network work"

```
test_sent = "will this computer network work"
```

We would first need to create an object of embeddingModel class and load the required embeddings.

#### For CBOW
```
eM = embeddingModel()
eM.load_CBOW_model()
```

Note : a compressed version of CBOW which requires only `corpus_book.bin` can also be used instead.

For loading it, use
```
eM = embeddingModel()
eM.load_CBOW_compressed_model()
```
The remaining functions i.e. functions to get word vector, sentence vector etc are same as the functions for the CBOW model.

#### For ELMO
```
eM = embeddingModel()
eM.load_ELMO_model()
```

#### For ELMO-max or ELMO-concat
```
eM = embeddingModel()
eM.load_CBOW_model()
eM.load_ELMO_model()
```


Now, we can use the eM object for different purposes

### Example : Get vectors of each of the words of the sentence

```
word_vecs = eM.get_embed_CBOW_sent(test_sent) # for CBOW
word_vecs = eM.get_embed_ELMO_sent(test_sent) # for ELMO
word_vecs = eM.get_embed_ELMO_CBOW_concat(test_sent) # for ELMO-concat
word_vecs = eM.get_embed_ELMO_CBOW_max(test_sent) # for ELMO-max
```

### Example : Get vector for the sentence
```
sent_vec = eM.get_embed_CBOW_sent_avg(test_sent) # for CBOW
sent_vec = eM.get_embed_ELMO_sent_avg(test_sent) # for ELMO
sent_vec = eM.get_embed_ELMO_CBOW_concat_avg(test_sent) # for ELMO-concat
sent_vec = eM.get_embed_ELMO_CBOW_max_avg(test_sent) # for ELMO-max
```

### Example : Get word-vector mapping for words of sentence as dictionary
```
wordwise_vec = eM.get_embed_ELMO_sent_wordwise(test_sent) # for ELMO
wordwise_vec = eM.get_embed_ELMO_CBOW_concat_wordwise(test_sent) # for ELMO-concat
wordwise_vec = eM.get_embed_ELMO_CBOW_max_wordwise(test_sent) # for ELMO-max
```

This isn't needed for CBOW. For CBOW, to get vector of a word, `use get_embed_CBOW_word`
```
word = "computer"
word_vec = eM.get_embed_CBOW_word(word)

```

### A complete example

A complete example for getting word vectors for Elmo-concat would be 

```
from embeddingClass import embeddingModel, EpochSaver

test_sent = "will this computer network work"

eM = embeddingModel()
eM.load_CBOW_model()
eM.load_ELMO_model()

word_vecs = eM.get_embed_ELMO_CBOW_concat(test_sent)
```
