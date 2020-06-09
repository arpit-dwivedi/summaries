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

