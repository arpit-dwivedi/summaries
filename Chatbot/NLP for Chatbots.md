## Introduction

* Now we will learn the basic methods and techniques of NLP using an awesome open-source library called spaCy.
* We’ll be closely taking a look at POS tagging, stemming, entity detection, stopwords, dependency parsing, and noun chunks and finding similarity between words. All of these methods will be very helpful for you when you are building chatbots of your use-case.

### Need of NLP in Building a Chatbot
* It’s not that you can’t build a chatbot at all if you don’t know the method and techniques of NLP, but your scope will be somewhat limited. 
* You won’t be able to scale the application and keep the code clean at the same time.
*  NLP is considered the brain of chatbots that processes the raw data, does the munging, cleans it, and then prepares to take appropriate actions.

## spaCy
* spaCy is an open-source software library for advanced NLP, written in Python and Cython, built by Matthew Honnibal. 
* It provides intuitive APIs to access its methods trained by deep learning models.
* spaCy offers the fastest syntactic parser in the world.

spaCy claims to provide three promary things:
1. It is fastest library as spaCy does extremely well at extracting large-scale information. It is written from scratch with utmost care for memory with help of the Cython library.
2. spaCy is designed with “get things done” in mind. It helps us in accomplishing real-world NLP scenarios.
3. spaCy is one of the best libraries available in the open-source community to process text for deep-learning algorithms.

To install spaCy:

```linux
pip install -U spacy==2.0.11
```
#### spaCy Models

A model is a yield of an algorithm or, say, an object that is created after training data using a machine learning algorithm. spaCy has lots of such models that can be placed directly in our program by downloading it just like any other Python package.

To download models use:  ` sudo python3 –m spacy download en `

You can now load the model via `spacy.load('en_core_web_sm')`

## Fundamental Methods of NLP for Building Chatbots

### 1. POS Tagging
Part-of-speech (POS) tagging is a process where you read some text and assign parts of
speech to each word or token, such as noun, verb, adjective, etc.

This can be done using:

```python
nlp = spacy.load('en') #Loads the spacy en model into a python object
doc = nlp(u'I am learning how to build chatbots')
for token in doc:
    print(token.text, token.lemma_, token.pos_, token.tag_, token.dep_, token.shape_, token.is_alpha, token.is_stop) #prints the text and POS
```
POS tagging needed for chatbots to reduce the complexity of understanding a text that can’t be trained or is trained with less confidence.

### 2. Stemming and Lemmatization
* ***Stemming*** is the process of reducing inflected words to their word stem, base form.
     > A stemming algorithm reduces the words “saying” to the root word “say,” whereas    “presumably” becomes presum. As you can see, this may or may not always be 100% correct.

* ***Lemmatization*** is closely related to stemming, but lemmatization is the algorithmic
process of determining the lemma of a word based on its intended meaning.
     > the verb “to walk” may appear as “walk,” “walked,” “walks,” or “walking.” The base form, “walk,” that one might look up in a dictionary, is called the lemma for the word.

` spaCy doesn’t have any in-built stemmer, as lemmatization is considered more correct and productive.`

> Imagine you search with the text, “When will the next season of Game of Thrones be releasing?” In this case, the aforementioned query probably won’t match an article with a caption “Game of Thrones next season release date.” If we do the lemmatization of the original question before going to match the input with the documents, then we may get better results.

### 3. Named-Entity Recognition

* It is a process of finding and classifying named entities existing in the given text into pre-defined categories.
* The NER task is hugely dependent on the knowledge base used to train the NE extraction algorithm, so it may or may not work depending upon the provided dataset it was trained on.

* As per the documentation by spaCy, models trained on the OntoNotes 5 1 corpus support the following entity types.

|TYPE |DESCRIPTION|
|-----|-----------|
PERSON| People, including fictional
NORP |Nationalities or religious or political groups
FAC |Buildings, airports, highways, bridges, etc.
ORG |Companies, agencies, institutions, etc.
GPE |Countries, cities, states
LOC |Non-GPE locations, mountain ranges, bodies of water
PRODUCT |Objects, vehicles, foods, etc. (not services)
EVENT |Named hurricanes, battles, wars, sports events, etc.
WORK_OF_ART |Titles of books, songs, etc.
LAW |Named documents made into laws
LANGUAGE| Any named language
DATE |Absolute or relative dates or periods
TIME |Times smaller than a day
PERCENT| Percentage, including “%”
MONEY |Monetary values, including unit
QUANTITY| Measurements, as of weight or distance
ORDINAL |“first,” “second,” etc.
CARDINAL |Numerals that do not fall under another type

### 4. Stop Words
* Stop words are high-frequency words like a, an, the, to and also that we sometimes want to filter out of a document before further processing. 
* Stop words usually have little lexical content and do not hold much of a meaning.
* There are about 305 stop words defined in spaCy’s stop words list. You can always define your own stop words if needed and override the existing list

### 5. Dependency Parsing

* The parser can also be used for sentence boundary detection and lets you iterate over base noun phrases, or “chunks.”

* It helps in finding relationships between words of grammatically correct sentences.
* It can be used for sentence boundary detection.
* It is quite useful to find out if the user is talking about more than one context simultaneously.

### 6. Noun Chunks

You can think of noun chunks as a noun with the words describing the noun.

### 7. Finding Similarity

* Finding similarity between two words is a use-case you will find most of the time working with NLP. 
* While building chatbots you will often come to situations where you don’t have to just find similar-looking words but also how closely related two words are logically.
* spaCy uses high-quality word vectors to find similarity between two words using GloVe algorithm (Global Vectors for Word Representation).

When building chatbots, finding similarity can be very handy for the following
situations:


•	 When building chatbots for recommendation

•	 Removing duplicates

•	 Building a spell-checker

## Tokenization
Tokenization is one of the simple yet basic concepts of NLP where we split a text into
meaningful segments. spaCy first tokenizes the text (i.e., segments it into words and
then punctuation and other things).


## Regular Expressions

Regular expression can come handy for some fallback for a machine learning model.
It has the power of pattern-matching, which can ensure that the data we are processing
is correct or incorrect.
