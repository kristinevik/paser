# Sentence Parser

A small natural-language parser that takes an English sentence, builds its grammatical **syntax tree**, and pulls out the **noun phrase chunks**.

```
$ python parser.py sentences/4.txt   # "Holmes sat in the red armchair and he chuckled."

                        S
             ___________|______________________
            S                         |        |
   _________|___                      |        |
  |             VP                    |        |
  |      _______|___                  |        |
  |     |           PP                |        |
  |     |    _______|___              |        |
  |     |   |           NP            |        S
  |     |   |    _______|______       |     ___|_____
  NP    |   |   |      AdjP    |      |    NP        VP
  |     |   |   |       |      |      |    |         |
  N     V   P  Det     Adj     N     Conj  N         V
  |     |   |   |       |      |      |    |         |
holmes sat  in the     red  armchair and   he     chuckled

Noun Phrase Chunks
holmes
the red armchair
he
```

## How it works

- **Preprocessing:** the sentence is lowercased, tokenized with NLTK, and stripped of anything that isn't a word.
- **Grammar:** I wrote a context-free grammar covering sentences, noun phrases, verb phrases, adjective and adverb phrases, prepositional phrases, and conjunctions (like "Holmes sat down **and** lit his pipe"). It is compact but still handles all the sample sentences, some with nested prepositional phrases.
- **Parsing:** NLTK's chart parser finds every valid tree for the sentence.
- **Noun phrase chunking:** the parser walks the tree and returns each `NP` that does not contain a smaller `NP` inside it.

The vocabulary comes from Sherlock Holmes stories, hence all the pipes and armchairs.

## Run it

```bash
pip install nltk
python -c "import nltk; nltk.download('punkt_tab')"
python parser.py sentences/10.txt   # parse a sample sentence
python parser.py                    # or type your own
```

## Built with

Python · NLTK
