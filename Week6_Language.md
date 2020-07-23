# Language - CS50AI Lecture 6

## Natural Language Processing:

Algorithms that allow our AI to process and understand natural language

- Automatic summarization
- information extraction
- language identification
- machine translation
- named entity recognition
- speech recognition
- text classification
- word sense disambiguation
- ...

## Syntax and Semantics:

Just like programming languages have their own specific syntax, the languages we humans speak have their own syntax(grammar). For example, we can agree that the following sentence has good grammar, "just before nine o'clock, Sherlock Holmes stepped briskly into the room." However, this sentence does not have good grammar, "Just before Sherlock Holmes nin o'clock stepped briskly the room."

Then, there's the idea of semantics. The idea of what do sentences mean? "Just before nine o'clock Sherlock Holmes stepped briskly into the room." has a different structure than "Sherlock Holmes stepped briskly into the room just before nine o'clock" but they mean the same thing. We can also have a sentence that is grammatically correct but means absolutely nothing: "Colorless green ideas sleep furiously." This problem can get complicated very quickly.

## Context-Free Grammar:

**Generating sentences in a language using symbols and rewriting rules.**

Represent each word as a terminal symbol and assign a non-terminal symbol to each terminal symbol.

![symbols](images/Week6_Language/../6_Language/symbols.png)

To Help us translate non-terminal symbols into terminal symbols where the "|" represents possible choices for that non-terminal symbol.

![nttot](images/Week6_Language/../6_Language/nt-to-t.png)

New non-terminal symbols can be constructed using existing non-terminal symbols.
- A noun phrase = a noun OR a determiner followed by a noun: `NP -> N | D N`.
- A verb phrase = a verb OR a verb followed by a noun phrase: `VP -> N | V NP`.
- Sentence = noun phrase followed by a verb phrase: `S -> NP VP`


### Syntax Trees:

Using language syntax trees, we can start to see the structure of language from while assembling sentences and/or phrases. Here are some examples.

Noun Phrase: Determiner followed by a noun

![city](images/Week6_Language/../6_Language/npTheCity.png)

Verb Phrase: A verb followed by a noun phrase

![vpnp](images/Week6_Language/../6_Language/vpnp.png)

A Sentence: Noun phrase followed by a verb phrase

![sent](images/Week6_Language/../6_Language/sent.png)

## Natural Language Took Kit (nltk):

A useful python library for natural language processing.

```python
import nltk

grammar = nltk.CFG.fromstring("""
    S -> NP VP

    NP -> D N | N
    VP -> V | V NP

    D -> "the" | "a"
    N -> "she" | "city" | "car"
    V -> "saw" | "walked"
""")

parser = nltk.ChartParser(grammar)

sentence = input("Sentence: ").split()
try:
    for tree in parser.parse(sentence):
        tree.pretty_print()
        tree.draw()
except ValueError:
    print("No parse tree possible.")
```
As a simple example, running the above code with input "she walked" would give us the output:

![nltkOutput](images/Week6_Language/../6_Language/nltkOutput.png)

This is still a very basic example but we can start to see how this process can get complicated very quickly. If we were to increase the grammar knowledge, more sentences and sentence structures can be formed:

```
S -> NP VP

AP -> A | A AP
NP -> N | D NP | AP NP | N PP
PP -> P NP
VP -> V | V NP | V NP PP

A -> "big" | "blue" | "small" | "dry" | "wide"
D -> "the" | "a" | "an"
N -> "she" | "city" | "car" | "street" | "dog" | "binoculars"
P -> "on" | "over" | "before" | "below" | "with"
V -> "saw" | "walked"
```

nltk also can show us all possible sentence structures, that is to say, the sentence "she saw a dog with binoculars" can be represented as:

![dog1](images/Week6_Language/../6_Language/dog1.png)

OR:

![dog2](images/Week6_Language/../6_Language/dog2.png)

## _n_-gram

A contiguous sequence of _n_ items from a sample of text.

- Unigram: A continuous sequence of 1 item from a sample of text - _n_ = 1.
- Bigram: A continuous sequence of 2 items from a sample of text - _n_ = 2.
- Trigram: A continuous sequence of 3 items from a sample of text - _n_ = 3.
- Character _n_-gram: A contiguous sequence of _n_ characters form a sample text.
- Word _n_-gram - A contiguous sequence of _n_ words form a sample text.

Ex. Trigrams in "I'm learning a lot in CS50AI."

1) "I'm learning a"
2) "learning a lot"
3) "a lot in"
4) "lot in CS50AI"

Why might this be useful? Often when computers analyze text, they don't look at the whole text at once. Even we humans read word by word or phrase by phrase. With the above approach, there is a likelihood that the AI has never seen this exact text before but it could have seen phrases like "learning a lot." 

## Tokenization:

The task of splitting a sequence of characters into pieces (tokens)

- Word tokenization: the task of splitting a sequence of characters into words.

## Markov Models:

We've seen Markov models before and we can use them to predict words that might appear in a sentence. For example, each unit(or previous _x_ units) can predict what the value of the following unit will be based on tokenization information.

![munits](images/Week6_Language/../6_Language/markovUnits.png)

## Text Categorization:

Classifying text into categories.

Example: Given a sentence, is it positive or negative.
- 😃 "My grandson loved it! So much fun!"
- 🙁 "Product broke after a few days."
- 😃 "One of the best games I've played in a long time."
- 🙁 "Kind of cheap and flimsy, not worth it."

Example: Given words in an email classify the email as either words or spam.

![inboxSpam](images/Week6_Language/../6_Language/inboxSpam.png)

### Bag-of-Words Model:

Model that represents text as an unordered collection of words. In this case, ignore sentence meaning and just search for keywords.

## Naive Bayes:

Recall that Bayes' Rule is:

<p align="center">
  <img src="https://render.githubusercontent.com/render/math?math=$P(b | a) = \frac{P(a | b)*P(b)}{P(a)}$">
</p>

Given a comment, we want to be able to say: what is the probability it is positive - _P_(😃) and what is the probability it is negative - _P_(🙁). We can formulate this using conditional probability by saying _P_(😃 | "My grandson love it") or, _P_(😃 | "My", "grandson", "loved", "it"). In this case, _b_ = 😃 and _a_ = "My", "grandson", "loved", "it".

**Using Bayes' Rule,** 

_P_(😃 | "My", "grandson", "loved", "it") = _P_("My", "grandson", "loved", "it" | 😃)_P_(😃) / _P_("My", "grandson", "loved", "it")

We can further simplify the above equation because we aren't exactly looking for exact probabilities. Since the denominator is the same regardless of + or -, we can formulate it using joint probabilities:

_P_(😃, "My", "grandson", "loved", "it") = _P_(😃)_P_("My" | 😃)_P_("grandson" | "My", 😃), etc...

Now, this approach raises a few concerns. You can imagine if we wanted to find out _P_("grandson") it would be quite hard and arbitrary to do that just being given "My" and 😃. Instead, we can treat each word as a separate probability which means that the probability of "grandson" being in the sentence if it's 😃 won't change even if other words are present.

_P_(😃, "My", "grandson", "loved", "it") is naively proportional to _P_(😃)_P_("My" | 😃)_P_("grandson" | 😃)_P_("loved" | 😃), etc...

### Calculation:

_P_(😃) = number of positive samples / number of total samples.  
_P_("loved" | 😃) = number of positive samples with "loved" / number of positive samples

**Let's calculate the probabilities**

Sentence:  
_P_(😃)_P_("My" | 😃)_P_("grandson" | 😃)_P_("loved" | 😃)_P_("it" | 😃)

Known Probabilities:

| 😃 | 🙁 |
|-----|----|
| 0.49| 0.52|

| | 😃 | 🙁 |
|----|-----|----|
| my | 0.30| 0.20|
| grandson | 0.01| 0.02|
| loved | 0.32| 0.08|
| it | 0.30| 0.40|

Using the able probabilities we can compute the joint probability for the above sentence which turns out to be: 😃 - 0.00014112. Alone, this number doesn't give us much information so we then compute a similar joint probability but multiply all the negative values instead. This gives us the value 🙁 - 0.00006528. After normalizing the values, we get:

😃 = 0.6837
🙁 = 0.3183

We are 68.37% confident that the above sentence is positive. Once again, there are downsides to this approach. Let's say the probability of "grandson" occurring in a positive sentence was 0.00. Our final probability would result in 0 which isn't exactly accurate because we are essentially ignoring all the other probabilities. Below are some possible solutions.

### Additive Smoothing:

Adding a value _α_ to each value in our distribution to smooth the data.

### Laplace Smoothing:

Adding 1 to each value in our distribution. Pretending we've seen each vale one more time than we have.

### Summary:

The main goal of naive bayes is to ignore words that appear to be equally likely in both positive and negative sentences. What makes the difference when it comes to classification is when a probability for one word is much higher for one sentiment rather than another.

## Information Retrieval:

The task of finding relevant documents in response to a user query

### Topic Modeling:

Models for discovering the topics for a set of documents

### Term Frequency:

Number of times a term appears in a document

This might not provide us with an accurate subject of a document simply because English grammar words(and, but, a, of, etc...) will most likely be the most used words regardless of the doc subject.

- Function words - words that have little meaning on their own but are used to grammatically connect other words
  - E.g. the, and, am, is, yet, which, etc...
- Context words - words that carry meaning independently
  - E.g. algorithm, category, computer, etc...

To solve this problem, we can print out the most common words that are not in a list of function words. That way, we eliminate words that don't give us much meaning. However, even this poses a couple concerns. In a series like Harry Potter, it is probably safe to assume that the words "Harry" and "Hermione" and "Ron" might appear the most often in each book but it still isn't telling us the difference between them. What we really want is to find words that occur more frequently in one document but less frequently in other documents.

### Inverse Document Frequency:

Measure of how common or rare a word is across documents

Calculated using:

<img src="https://latex.codecogs.com/gif.latex?log%5Cfrac%7BTotalDocuments%7D%7BNumDocumentsContaining%28word%29%7D">

As the denominator(num documents that contain word) increases, the argument(total/num docs) to the logarithm decreases making the inverse document frequency smaller. If the argument equals 1, that word has an inverse argument frequency of 0.

### tf-idf:

Ranking of what words are important in a document by multiplying term frequency(TF) by inverse document frequency(IDF)

## Information Extraction:

The task of extracting information from documents

**Examples:**

"<span style="color: #1a73e8;">When **Facebook** was founded in **2004**</span>, it began with a seemingly innocuous mission: to connect friends. Some seven years and 800 million users later, the social network has taken over most aspects of our personal and professional lives, and is fast becoming the dominant communication platform of the future."  
-Harvard Business Review, 2011

"Remember, back <span style="color: #1a73e8;">when **Amazon** was founded in **1994**</span>, most people thought his idea to sell books over this thing called the internet was crazy. A lot of people had never even hard of the internet."  
-Business Insider, 2018

### Concept:

Using text templates like the part highlighted above, we can let our AI search the web and try and find out useful information that we may be looking for.

When {company} was founded in {year}, ...

Websites might write their description of the above with a different template and of course, the AI would fail. However, we can give the AI data rather than specific templates. Something like "Amazon: 1994" and "Facebook: 2004". Now the AI can look to see where "Amazon" & "1994" showed up together and where "Facebook" & "2004" showed up together and discover templates for itself.

## Word Representation:

Represent the meaning of a word so the AI can understand it

### One-Hot Representation:

Representation of meaning as a vector with a single 1, and with other values as 0.

"He wrote a book."

he - [1, 0, 0, 0]  
wrote - [0, 1, 0, 0]  
a - [0, 0, 1, 0]  
book - [0, 0, 0, 1]

Now for the drawbacks: Imagine a dictionary with 50,000 words. We would have enormously large vectors as well as the fact that words would have completely distinct vectors despite having a similar meaning.

### Distribution Representation:

Representation of meaning distributed across multiple values

![distRep](images/Week6_Language/../6_Language/distRep.png)

We can define a word in terms of the words that show up around it; based on the context in which the words appear.

## Word2Vec:

Model for generating word vectors

### Skip-Gram Architecture:

Neural Network architecture for predicting context words given a target word. 

Given training data of words and what other words appear in context, our AI can try and predict similar words. For example, given the word "lunch" try and predict what words are going to appear around it i.e. "For", "he", "she", "ate", etc...

![w2v](images/Week6_Language/../6_Language/word2vec.png)

The general idea here is that if two words are similar, their weights will be similar. This essentially allows us to use the weights themselves as the vector values - the word's definition. More generally, start with a random arrangement of words:

![wordSpread](images/Week6_Language/../6_Language/spreadWords.png)

As the neural network learns, we can start grouping words that have similar context words and meanings.

![groupedWords](images/Week6_Language/../6_Language/groupedWords.png)

Now, given two vectors that represent words, we can subtract them to find out what the distance or relationship between those two words is. In practice, it might not make sense to "subtract" words but since the computer represents them as numbers, we can do so. Then we can try and predict similar words for something else by adding the difference(analogies).

![subVec](images/Week6_Language/../6_Language/subVec.png)

### Example 1:

Vector that takes us from "france" to "paris"
```
words["paris"] - words["france"]
```

Add to england to get a new vector. Find closest word given that vector
```
words["paris"] - words["france"] + words["england"]
```

Amazingly, we get "london"
```
'london'
```

### Example 2:

Vector that takes us from "school" to "teacher"
```
words["teacher"] - words["school"]
```

Add to "hospital" to get a new vector. Find closest word given that vector
```
words["paris"] - words["france"] + words["hospital"]
```

Amazingly, we get "nurse"
```
'nurse'
```