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
pip install -U spacy
```
#### spaCy Models




