---
title: sense2vec and ngrams
author: Thinkful
team: grading
time: 60
uuid: a6517690-b93b-47a5-b9d4-04008a6ef927
---

##More than words

In our previous introduction to NLP, we created features based on individual words.  Sometimes we even reduced the words to their root forms, called lemmas.  Now we’re going to go in the opposite direction, and create features using combinations of words with other information.  

## Sense2vec: Words and syntax

You may recall that word2vec is an algorithmic approach to modeling the similarity of various words by representing each word as a vector in space.  Words that are often close to other words in sentences have vectors near one another, while words that usually aren’t near one another end up with distant vectors.  Each time a sentence is processed, the vectors move in a ‘push-pull’ fashion, with nearby words moving closer together while pushing other words farther away.

A problem arises, however, when two words look the same but have different meanings (homonyms).  For example, the word ‘break’ in “Give me a break” vs “Break a leg.”  In the first sentence, ‘break’ is a noun that refers to a stop or short interruption in an activity.  In the second, ‘break’ is a verb that means to shatter or split into multiple pieces.  If both meanings are forced to share a vector, as in word2vec, that vector will end up occupying an uneasy place in the space between vectors for words like ‘vacation’ and ‘stop’ on one hand and words like ‘accident’ and ‘divide’ on the other.  This can cause the words ‘vacation’ and ‘divide’ to seem more similar than they truly are, because their vectors are drawn together by the shared association with ‘break’.

Sense2vec is a modification of word2vec that incorporates information on parts of speech- whether a word is a noun, verb, adjective, etc.  In a sense2vec model, `break_NOUN` has a vector completely separate from `break_VERB`.  In spaCy, text parsing includes tagging each word with its part of speech, which is inferred from the word’s context.  To create a sense2vec model, each word in a sentence should be replaced by a string containing the word and its part of speech.  After that, we apply the word2vec model-- the push-pull process and vectorization are the same, only the inputs (words vs word_pos strings) change.

Combining words with their parts of speech doesn’t need to be restricted to word2vec-type-models.  They can also be used to create features and term-document matrices.  Any modeling approach that typically uses words as features can also use words+POS.

## Ngrams: Words in context

Consider the word ‘vain’ in these two sentences:

“She labored in vain, the rock would not move.”
“She was so vain, her bathroom mirror was covered in lip prints.”

In both sentences, ‘vain’ is an adjective.  In sentence 1, it signals a lack of success.  In sentence 2, the same word means vanity.  Since the two usages can’t be distinguished by their part of speech, how can we tell them apart?  

Ngrams incorporate context information by creating features made up of a series of consecutive words.  The ‘N’ refers to the number of words included in the series.  For example, the 2-gram representation of sentence 1 would be:

She labored
labored in
in vain
vain the
the rock
rock would
would not
not move

The 3-gram representation of sentence 2 would be:

She was so
was so vain
so vain her
vain her bathroom
her bathroom mirror
bathroom mirror was
mirror was covered
was covered in
covered in lip
in lip prints

Each of the word sets could then operate as its own feature.  Ngrams can be used to create term-document matrices (though it would now be ngram-document matrices), or used in topic modeling.  In addition, ngrams are useful for text prediction as they can be used to determine what words are most likely to follow in a sentence, phrase, or search query.  

For a sentence with *X* words, there will be *X-(N-1)* Ngrams.  2-gram phrases are also called ‘bigrams,’ 3-gram phrases are called ‘trigrams,’ etc.

# Why use words alone?

Given the benefits of incorporating parts of speech or word context for distinguishing between different meanings of a word, why would any NLPer worth their salt ever use simple word features?  Models based on single words have several advantages.  

First, unlike POS models, single-word models don’t require any pre-existing knowledge of the syntax or structure of the language being modeled.  If we wanted to build an NLP model incorporating parts of speech on a corpus written in Afrikaans, we would have to create a POS-tagging system from scratch.  This would take a long time.

Second, ngram models are considerably more sparse than single-word models.  The two ‘vain’ sentences above share four words (‘she’, ‘in’, ‘vain’, ‘the’) but zero ngrams.  Sparseness does mean that an ngram model can be stored in a more memory-efficient way (for example, in a dict that only lists the ngrams that are present in each sentence rather than a set of columns with 1 if an ngram is present and 0 otherwise).  However, it also means that a larger corpus may be needed to detect any shared patterns across documents.  In other words, ngram models may need more documents before they start to give good results.

Single-word models are straightforward to implement, while models incorporating parts of speech or ngrams are more sensitive to fine distinctions of meaning.  Which to choose depends on the goals of the NLP project and the trade-offs in time and performance for the specific corpus you are modeling.