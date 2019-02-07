---
title: Text summarization
author: Thinkful
team: grading
time: 60
uuid: f548f6c7-54b1-4471-89a9-16c6033a3f4b
---

## Summarizing Text

In addition to discovering underlying themes and ideas, one of the goals of the summary method of topic extraction is to represent the information in text in a more concise way.

It's not hard to imagine the appeal of being able to sum up a long piece of text into a few words or sentences. Google uses summarization to produce the brief website descriptions that appear on its search page, as do content aggregators of all kinds. Summarization is also done by human beings: There are whole publishing groups devoted to boiling down popular nonfiction books into their core messages for consumption by busy professionals.

There are NLP techniques that are intended specifically for summarization. Text summarization techniques fall into two categories: Extractive, and abstractive. We are going to focus on extractive techniques, with a brief mention of abstractive.

## Extractive text summarization
Extractive techniques do exactly what their name suggests-they extract parts of the text. The intention is for the extracted parts to stand in place of the whole text. These parts can be sentences, phrases, or single words (keywords). In the case of sentences or phrases, the extracts are identified by similarity-- the aspects of a text that are similar to many other parts of the text are assumed to be representative of the text as a whole. For example, the chorus of "Happy" by Pharrell is:

```
Because I'm happy
Clap along if you feel like a room without a roof
Because I'm happy
Clap along if you feel like happiness is the truth
Because I'm happy
Clap along if you know what happiness is to you
Because I'm happy
Clap along if you feel like that's what you wanna do
```

The two phrases that have the most similarity to other phrases in the song are 'Because I'm happy', repeated four times, and 'clap along', also repeated four times. Each of those repetitions is identical to each other repetition, giving each instance of the phrase a very high similarity score. So an extractive summary of 'Happy' might be 'Clap along because I'm happy.'

## Supervised Extraction

If we have a training set that provides labels to guide our model (a sentence may be labeled ‘topic sentence’, for example), we can use any of the usual supervised learning techniques from the supervised NLP lesson.  The more interesting case comes in when we don’t have a training set:

## Unsupervised Extraction: Sentences and Similarity

In the absence of labels and guides, we can identify representative sentences as those which are highly similar to other sentences.  When measuring similarity, we want to prioritize sentences that share important words.  One way to identify which words are ‘important’ is to compute a term frequency-inverse document frequency (tfidf) matrix.  We worked with tfidf matrices in the first NLP lessons earlier on.  You  may recall that they count how often a word appears within a document or sentence (term-frequency or tf), divided by how many documents or sentences the word appears in (inverse document frequency, or idf).

Once we have the tfidf matrix, we measure how similar two sentences are by multiplying the matrix by its transpose. (A matrix is transposed by switching the row and column indices, so a value at M[1,6] becomes a value at M.T[6,1].)  Let’s work through how this results in a measure of similarity, using a sample tfidf matrix of three sentences:

"The best Monty Python sketch is the one about the dead parrot, I laughed so hard."
"I laugh when I think about Python's Ministry of Silly Walks sketch, it is funny, funny, funny, the best!"
"Chocolate is the best ice cream dessert topping, with a great taste."


|           | A | B | C | 
|-----------|---|---|---|
| Monty     | 1.585 | 0 | 0 |
| Python    | 1 | 1 | 0 | 
| sketch    | 1.585| 1.585 | 0 | 
| laugh     | 1 | 1 | 0 | 
| funny     | 0 | 4.755 | 0 | 
| best      | .585 | .585 | .585 | 
| ice cream | 0 | 0 | 1 | 
| dessert   | 0 | 0 | 1.585 | 
| taste     | 0 | 0 | 1 |

Using the tfidf, each sentence is represented by a vector. To multiply two vectors using matrix multiplication, each element of vector A is multiplied by the element in the same position in vector B. So VecA[0] x VecB[0], VecA[1] x VecB[1], etc. Then, the products are summed. This is convenient, because it means that by multiplying the two sentence vectors together, we get a one-number index of similarity.  (This is by no means the only way to test whether two sentences are similar. Any similarity algorithm can be inserted at this step- this one is common.)

## Drill: Matrix multiplication and similarity

Why would multiplying the tfidf vectors of two sentences give information about how similar they are to one another? Try to figure it out by multiplying the vectors for sentence A with the other two sentences. Do it by hand, if you can- you'll be multiplying sentence A's tfidf score for ‘Monty’ with sentence B's tfidf score for ‘Monty’, for example. Which sentence does intuition tell you is most similar? Does the math bear it out?

Once you think you've figured out why the matrix multiplication results in a similarity score, write an explanation in your own words and discuss it with your mentor.

(You can submit your work at the bottom of this lesson)

## Rank rather than mere similarity: Choosing sentences using TextRank

We could potentially stop here, by choosing the sentence with the highest mean or median similarity score to be our representative sentence.  Sometimes this approach is just fine.  However, this method is prone to bias.  If a document has two instances of the same sentence, for example, they are going to have very high similarity scores compared to the scores of other sentences.  This is fine if those two sentences are important, but if they are something generic such as 'Thank you very much,' then we're not going to find them very valuable as summaries.  

What we really want is to find a sentence or sentences that are very similar to many other sentences that are *themselves* very similar to many other sentences: The best sentence in a cluster of similar sentences.  

The algorithm we're going to use is called [TextRank](https://web.eecs.umich.edu/~mihalcea/papers/mihalcea.emnlp04.pdf).  At a conceptual level, the idea behind TextRank is that a sentence's rank is determined by the number and the rank of the sentences that it is similar to.   A sentence that is highly similar to a few high-ranked sentences will have a higher TextRank than a sentence that is similar to a lot of low-ranked sentences.  

The algorithm is iterative.  Since each sentence's rank depends on the rank of other sentences, any adjustment in the rank of one sentence can result in adjustments to the rank of many other sentences.  Iteration proceeds until the change in ranks falls below a user-provided threshold.

In addition, there is a 'damping' parameter.  This parameter keeps the calculation for the rank of an individual sentence from going on forever (the rank of sentence A is based on the rank of sentence B which is based on the rank of sentence C which is...).  The damping parameter represents the probability that the model will ‘jump’ to another sentence entirely and start over again.  A damping parameter close to 1 means the model is likely to only go a few sentences deep for its rank calculation before jumping to a new sentence and starting again.  A damping parameter close to 0 means the model will probably be able to incorporate the ranks of a large number of sentences before jumping.

The formula for the TextRank score for a sentence $V_i$ of a list of sentences $V$ requires the following information:

$d$: A damping factor: Traditionally set to .85  
$V_j\epsilon V_i$: The set of sentences $V_j$ that have similarity scores > 0 with $V_i$.  
$w_{ji}$: The similarity of sentences $V_i$ and $V_j$.  
$V_k\epsilon V_j$ The set of sentences $V_k$ that have similarity scores > 0 with $V_j$.  
$R(V_j)$: The rank of sentence $V_j$.  

$$Rank(V_i)=(1-d)+d\sum_{V_j\epsilon V_i}\dfrac{w_{ji}}{\sum\limits_{V_k\epsilon V_j} w_{jk}}R(V_j)$$

In words, the rank of sentence $V_i$ is calculated by:

1. The rank of sentence $V_j$ multiplied by:  
2. The sum of the similarity scores ($w_{ji}$) for all the sentences with sentence $V_i$, where each is each divided by the sum of the similarity scores ($w_{jk}$) for all the sentences with sentence $V_k$.  
3. This is multiplied by the damping factor $d$, and added to $(1-d)$.  

## Keywords and co-occurrence

Another method of summarizing text is to choose relevant keywords that identify the central topics.  Extracting keywords can be done by similarity or by co-occurrence: Words that appear frequently are likely to be useful keywords. Key phrases can be built by combining two frequently adjacent keywords.

Quantifying co-occurrence involves defining how close a word needs to be to another word to count as being ‘nearby’.  This window can vary widely depending on the type of text.  Many keyword extraction algorithms only use nouns and adjectives when searching for keywords, as these are more likely to contain descriptive information.

Once the ‘co-occurrence’ of words has been calculated, the TextRank algorithm can be used to identify the most important words.

## More extraction

We have focused on using similarity or co-occurrence information to identify important sentences, phrases, or words, but there are other methods.  For example, news articles use an ‘inverted pyramid’ structure where the most important details are presented first.  Knowing this, an algorithm summarizing news stories could use sentence order as an indicator of weight.  Some grammatical structures may also be more likely to contain important information; it all depends on the type of text you want to summarize.

## Abstractive text summarization

The goal of abstractive text summarization is to summarize like a human being.  Abstractive summaries are often shorter than extractive ones, but are much more challenging to generate.  For example, here are examples of extractive and abstractive summaries of the opening sentence of A Tale of Two Cities by Charles Dickens:

“It was the best of times, it was the worst of times, it was the age of wisdom, it was the age of foolishness, it was the epoch of belief, it was the epoch of incredulity, it was the season of Light, it was the season of Darkness, it was the spring of hope, it was the winter of despair, we had everything before us, we had nothing before us, we were all going direct to Heaven, we were all going direct the other way – in short, the period was so far like the present period, that some of its noisiest authorities insisted on its being received, for good or for evil, in the superlative degree of comparison only.”

Extractive: It was... like the present ...in the superlative degree of comparison.
Abstractive: It was a time of contradictions.

Abstractive methods rely on neural networks to identify the core of a text and to produce a summary that reflects the core, without necessarily using the same words as in the original text.  Abstractive text summarization is sufficiently complex and cutting-edge that it would require an entire course to do it justice.  If you want to read more about it, [this article](http://www.jatit.org/volumes/Vol59No1/7Vol59No1.pdf) has a high-level overview of the methods used in the field.  Also, this [post by Google’s Research Blog](https://research.googleblog.com/2016/08/text-summarization-with-tensorflow.html) introduces their abstractive text summarization algorithm using TensorFlow.  Be warned, however, that their algorithm requires a huge corpus and days to weeks of computing time to produce useful results.