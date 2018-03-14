## About
Keyphrase extraction is the task of identifying single or multi-word expressions that represent the main topics of a document. In this paper we present [TopicRank]((http://www.aclweb.org/anthology/I13-1062)), a graph-based keyphrase extraction method that relies on a topical representation of the document. Candidate keyphrases are clustered into topics and used as vertices in a complete graph. A graph-based ranking model is applied to assign a significance score to each topic. Keyphrases are then generated by selecting a candidate from each of the topranked topics. We conducted experiments on four evaluation datasets of different languages and domains. Results show that TopicRank significantly outperforms state-of-the-art methods on three datasets.

*Adrien Bougouin, Florian Boudin and Béatrice Daille. 2013. Topicrank: Graph-Based Topic Ranking for keyphrase Extraction. In Proceedings of the 6th International Joint Conference on Natural Language Processing (IJCNLP), Nagoya, Japan, October.*

## Algorithm
1. Use nltk to identify parts of speech of every word in text
1. Identify longest sequences of adjectives and nouns - they constitute keyphrases
1. convert each keyphrase to term frequency vector using bag of words, apply stemmer for better compression
1. find clusters of keyphrases using Hierarchical Agglomerative Clustering (HAC) algorithm to form topics:
- use `average` strategy
- identify cluster by max depth of 1.25
5. use clusters as graph vertices and sum of distances between each keyphare of topic pairs as edge weight
5. apply PageRank to identify most prominent topics
5. For topN topics extract most significant keyphrases that represent this topic. Possible strategies
- use a keyphrase which is closer to the beginning of the text (`first`)
- use center of the cluster from p.4 (`center`)
- use most frequent (`frequent`)

## Installation
```bash
pip install -e git+https://github.com/smirnov-am/pytopicrank.git#egg=pytopicrank
```

## Usage

```python
from topicrank import TopicRank

with open('tests/ion_exchange.txt') as f:
    text = f.read()
    tr = TopicRank(text)
    tr.get_top_n(n=2)

>>> ['ion exchange', 'mathematical model']
```
