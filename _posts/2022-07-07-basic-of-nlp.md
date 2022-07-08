---
title:  "Basic Introduction to Natural Language Processing"
date:   2022-07-07 09:29:17 +0545
categories: Natural-Language-Processing
tags:
  - Natural Language Understanding
  - Natural Language Processing
  
header:
  teaser: "assets/NLP/Basic_of_nlp/syntax_structure.png"
  overlay_image: "assets/NLP/Basic_of_nlp/syntax_structure.png"
toc: true
---

# Basic Introduction of NLP 
NLP is a Short form of natural language processing. It is subfield of artificial intelligence.The study of how to program computers to comprehend and use natural language led to the development of the area. In simple word NLP is process of making computer understand human language like English, Nepali. As name suggest natural language processing deal with the different form of language which can be text, audio, video and image.

 It is in the confluence of several other closely related fields, including linguistics, mathematics, computer science, statistics, and neuroscience.  

![image]({{site.url}}/assets/NLP/Basic_of_nlp/Intersection.png)

NLP has two main component,

* Natural Language Understanding
* Natural Language Generation

**Natural Language Understanding**: 

A kind of artificial intelligence known as "natural language understanding" use computer software to comprehend input in the form of spoken or written phrases. Human-computer interaction is made possible via NLU. Computers can understand commands without the codified syntax of computer languages since they can understand human language, such as English, Nepali, Spanish, and French, for example. NLU also makes it possible for computers to converse with people in their own languages.

NLU's major goal is to develop chat- and voice-capable bots that can communicate with the public unsupervised. NLU projects are now being worked on by many well-known IT firms, including startups and Amazon, Apple, Google, and Microsoft. [source](https://www.techtarget.com/searchenterpriseai/definition/natural-language-understanding-NLU)

**Natural Language Generation** :
A software method called natural language generation uses natural language processing to generate written or spoken text from both organized and unstructured data.

Natural language generation is used by chatbots, voice assistants, and artificial intelligence blog writers, to name a few. Based on pre-defined templates, NLG systems may transform numerical data into tales. They can anticipate the words that should be generated next (in an email, for example, that you're currently composing). Alternatively, the most advanced algorithms are capable of creating full summaries, articles, or responses.



## What is Language

In plain English, it is a device used to convey one person's thought to another. It is also described as a structured form of communication that employs creative arrangements of its constituent parts, such as words, phrases, and characters. In different parts of the world, people speak a variety of languages. Although Nepali is the official language of the country, people from various localities also speak other languages as a means of communication. There is more room for NLP work here in Nepali terms as well. There have been many difficulties for the researcher to learn more about Nepal's local language because there aren't enough people to work on the project and there aren't enough resources. 

Systematic study of language is called *Linguistics*. It's crucial to comprehend some linguistics ideas regarding how language is formed in order to learn NLP.

## Building Blocks of Language and Their Applications

### Phonemes

smallest linguistic units of sound. Even while they might be meaningless on their own, when combined with other words, they can create new meanings. They are either single letters or a combination of letters. Especially crucial in speech understanding applications like text to speech conversion, speech recognition, and speech-to-text transcription. There are consonant phonemes and vowel phonemes. Example of consonant phonemes are bat, cat, dog, fan, sun etc similarly example of vowel phonemes are ant, egg, on, in, coin, rain etc.

### Morphemes and Lexemes
**Morphemes**
Smallest meaning-containing unit in language is simply known as morphemes. Morphemes are formed by combination of *phonemes*. All prefixes and suffixes are morphemes, however not all morphemes are words.

**Lexemes** 
Lexemes are the structural variations of morphemes related to one another by meaning. For example, “run” and “running” belong to the same lexeme form.


By examining its morphemes and lexagrams, morphological analysis examines the structure of words. Serves as a building piece for numerous NLP tasks, including part of speech tagging, leaning word embeddings, tokenization, and stemming.

Example of Morphemes 

![image]({{site.url}}/assets/NLP/Basic_of_nlp/morphem.png)

### Syntax

A set of guidelines for turning words and phrases in a language into sentences that are grammatically accurate is commonly known as syntax. Syntactic structure in linguistics is represented in many different ways. A common approach is the parse tree representation.

**What is parse tree?**

Its vocabulary is organized hierarchically, starting with words at the lowest level, moving up through part-of-speech tags, phrases, and ending with sentences at the highest level. A set of linguistic grammar rules govern the syntactic structure, which in turn governs some of the basic language processing operations like parsing. Some NLP activities that build on the understanding of parsing include entity extraction and relation extraction. Different techniques may be required for each language due to the differences in syntax across different languages. 

Example 

![image]({{site.url}}/assets/NLP/Basic_of_nlp/Parse_tree.png)

#### Syntax structure

### Context
Context describes how different elements of a language combine to convey a specific meaning. Along with the words' and phrases' explicit meanings, this also takes into account extensive references, general knowledge, and common sense. Given that some words and phrases might have more than one meaning depending on the context, the meaning of a statement may vary. Generally, context is composed from semantics and pragmatics.

>>Semantics without any further context, semantics is the straightforward meaning of words and sentences.
Pragmatics adds world knowledge and external context of the 
conversation to enable us to infer implied meaning.

Contexts are used extensively in complex NLP tasks including topic modeling, summarization, and sarcasm detection.






## Natural Language Task

**Question Answering**
Creating a system that can instantly respond to queries in Natural Language.
 

**Machine Translation**
 The process of translating text from one language to another. Google translate is the common example of this task.
 
**Topics Modeling**
Discovering a big collection of papers' thematic organization. Text mining software that is widely utilized in fields ranging from bioinformatics to literature.
  
 ![image]({{site.url}}/assets/NLP/Basic_of_nlp/syntax structure.png)



## Why Natural Language Processing is Challenging

Natural Language Processing still has a lot of jobs to investigate. It is also evident that this subject has a vast array of research topics. Even if there are still more jobs to complete in the sector in Nepal, it is evolving more slowly than in other nations. It goes without saying that NLP's difficulty is one of the key causes of its delayed development. Although Nepal has achieved linguistic diversity, difficulties could follow from it. Some of the challenge in NLP are listed below.

**Common Knowledge**

Essential feature of any human language. Refers to the collection of all knowledge that the majority of people have. Common knowledge is constantly used by people to comprehend and process all languages. Compare the two sentences
 `“Man bit dog”`, `“Dog bit man”`. Here two sentence seems to be same but there meaning is drastically different. How to accurately encode all of the information that is common knowledge to people in a computational model is one of the main issues in NLP.
 
**Creativity**

Language has a creative component as well as being rule-driven. A language uses a variety of styles, dialects, genres, and variants. Making machines understand creativity is a challenging topic in AI in general, not just NLP.

**Diversity Across Languages**

There isn't a direct mapping between any two languages' vocabularies for the majority of languages spoken worldwide. Thus, it is challenging to port an NLP solution from one language to another. It is conceptually very difficult to provide a language-neutral solution, and it takes a lot of work and effort to create language-specific solutions for each language.


## Applications Of NLP

**Core Applications**

Email platforms that use NLP to implement features like auto-complete, priority inboxes, calendar event extraction, etc.
NLP approaches used by voice-based assistants in their communication with users. NLP is used in conjunction with modern search engines to efficiently retrieve information. It is also use in services for Machine Translation.

**Additional Applications**

• Increasing Social Media Use and Analysis.

• Widespread application of NLP in e-commerce platforms

• Growing trends in usage in other fields, such as law, finance, and healthcare.

• NLP is the foundation of tools for grammar and spelling checks.

• IBM Watson AI triumphing on the well-known game show Jeopardy.

• Used in a variety of tools and technologies for learning and assessment (automatic GRE exam scoring, plagiarism detection, intelligent tutoring systems, language learning apps).

• The use of NLP to create expansive knowledge bases like the Google Knowledge Graph


```python

```
