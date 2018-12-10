---
title: 'Challenge: social network analysis'
author: Thinkful
team: grading
time: 90
uuid: 65aea860-2fe8-4538-8f02-78330e78f7b9
---

# Challenge

As we mentioned at the beginning, this data is drawn from an academic article on [The human disease network](http://www.pnas.org/content/104/21/8685.full).  The article actually includes [three networks](http://www.pnas.org/content/104/21/8685/F1.large.jpg): The disease network we've been working with, the [disease gene network](https://web.archive.org/web/20150203073042/http://www.barabasilab.com:80/pubs/CCNR-ALB_Publications/200705-14_PNAS-HumanDisease/Suppl/gene.net.w) (which links genes by their shared diseases), and a bipartite network that contains [both diseases and their genetics](https://web.archive.org/web/20150203073034/http://www.barabasilab.com:80/pubs/CCNR-ALB_Publications/200705-14_PNAS-HumanDisease/Suppl/bipartite.net).   A bipartite network is a network that can be broken into two sets of nodes (diseases and genes, in this case) with every node in each set connected to a node in the other set.  If you're interested in this data, the article contains an in-depth examination of the networks from the perspective of disease science.

Your challenge is to take one of the other networks (or a network of your choice) and tell a data story about it, similar to the one we did here.  You should have an overarching question (ours was whether diseases would cluster into gene-mutation-based groups that matched their medical classifications) but also explore other aspects of your network.  Use both visualizations and statistics.  Specifically:
Generate at least two visualizations of the network itself
Identify the most central nodes
Generate network-level descriptive statistics (connectivity, clustering, etc)
Perform at least two analyses that involve node attributes (weight, group membership, etc)

The networkx documentation is [very thorough](https://networkx.readthedocs.io/en/stable/reference/algorithms.html) and has a lot of methods we haven't covered but which you may find useful as you proceed.

