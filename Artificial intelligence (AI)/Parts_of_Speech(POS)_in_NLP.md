# 🧠 Parts of Speech (POS) Tagging in NLP

### 📖 Description  
Parts of Speech (POS) Tagging is a fundamental step in **Natural Language Processing (NLP)** where each word in a sentence is assigned a specific grammatical label, such as **noun**, **verb**, **adjective**, etc.  
It helps machines understand the **structure**, **meaning**, and **context** of human language.

In NLP, POS tagging is commonly performed using libraries like **NLTK (Natural Language Toolkit)**.  
Each tag represents the word’s grammatical category — for example:  
- `NN` → Noun  
- `VB` → Verb  
- `JJ` → Adjective  
- `RB` → Adverb  

These tags are used in many NLP tasks such as **text classification**, **sentiment analysis**, **chatbots**, and **information extraction**.

---

### 🏷️ POS Tags and Their Descriptions

| **Tag** | **Description** | **Examples** |
|----------|------------------|---------------|
| **CC** | Coordinating conjunction | and, but, or |
| **CD** | Cardinal number | one, two, 3 |
| **DT** | Determiner | the, a, an, this |
| **EX** | Existential there | there is, there are |
| **FW** | Foreign word | bonjour, gracias |
| **IN** | Preposition / Subordinating conjunction | in, on, at, because |
| **JJ** | Adjective | beautiful, tall |
| **JJR** | Comparative adjective | bigger, faster |
| **JJS** | Superlative adjective | biggest, fastest |
| **MD** | Modal | can, should, will |
| **NN** | Singular noun | dog, car |
| **NNS** | Plural noun | dogs, cars |
| **NNP** | Proper noun, singular | Moiz, India |
| **NNPS** | Proper noun, plural | Americans, Indians |
| **PRP** | Personal pronoun | I, he, she |
| **PRP$** | Possessive pronoun | my, his, her |
| **RB** | Adverb | quickly, slowly |
| **RBR** | Comparative adverb | faster, better |
| **RBS** | Superlative adverb | fastest, best |
| **VB** | Verb (base form) | run, eat |
| **VBD** | Verb (past tense) | ran, ate |
| **VBG** | Verb (gerund / present participle) | running, eating |
| **VBN** | Verb (past participle) | eaten, driven |
| **VBP** | Verb (non-3rd person singular present) | run, eat |
| **VBZ** | Verb (3rd person singular present) | runs, eats |
| **TO** | “to” (infinitive marker) | to go, to eat |
| **UH** | Interjection | oh, wow, hey |
| **WDT / WP / WRB** | Wh- words | what, who, where, when |

---

### 💡 Example in Python (Using NLTK)

```python
import nltk
from nltk.tokenize import word_tokenize

nltk.download('punkt')
nltk.download('averaged_perceptron_tagger')

text = "Moiz is learning Natural Language Processing."
words = word_tokenize(text)
pos_tags = nltk.pos_tag(words)
print(pos_tags)



---



