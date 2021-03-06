---
title: 'Semantic preserving quantization of word embeddings'
date: 2020-02-14
---

Introduction
======
Dense vector representations of words, or word embeddings, have been applied to a wide range of downstream natural language
processing and information retrieval tasks. These word vectors are learned from the co-occurrence of word representations 
in large text corpora using a single layer neural network. After training the word vectors hold syntactic and semantic information about words.

Using continuous representations in large-scale information retrieval tasks, such as web information retrieval, 
has two important disadvantages. First, the continuous representations have significant memory requirements since each
element of the vector is represented as a floating-point number. As a result, fewer documents can be held in main memory. 
Second, comparing continuous vectors requires floating-point similarity measures, such as cosine similarity or dot-product.

 These are more expensive than for example calculating the Hamming distance. Both disadvantages significantly hinder 
 the applicability of continuous representations in large scale information retrieval tasks. 
 A popular approach for decreasing the computational requirements while retaining semantic information is called semantic hashing

Semantic preserving quantization
======

One  solution for this problem is to preserve input topology by introducing a novel hashing method that directly enforces 
retainment of semantic information through a semantics-preserving loss function. Our research focussed on developing a 
Siamese autoencoder architecture that directly tried to optimise the distance between words in the input and latent
space. Our hypothesis was that directly enforcing the semantic similarity in latent space would increase the generated
codes. 



Results 
======

Table 2 shows the P@K scores for three text document collections. The scores for the continuous representations are 
shown in the Cont. column. We make several interesting observations. First, the autoencoder with the semantic preservation
 loss performed best in all but two retrieval tasks at various bit sizes. Furthermore, our model performed statistically 
 significant better for > 0.05 compared to the best performing baseline method at each individual task. Second, 
 for the best performing 256-bit semantic preserving autoencoder the degradation with respect to the continuous 
 representations for the 20 newsgroup and Reuters dataset is 5% and 2.7% respectively. Interestingly, the 256-bit
  semantic preserving model has a 4.2% higher P@K score over the continuous representations for the AG news dataset. 
  A similar phenomenon has been observed for the STS14 dataset in Table 1. Third, the semantic preserving model performs 
  better than the vanilla Siamese autoencoder in all but two retrieval tasks and is statistically signiccant for > 0.05 
  for three of the nine tasks.
  
  <img src="http://woutermostard.github.io/files/document_classification.png" align="middle" width="500" height="500">
  
  
 Finally, we were interested into determining whether our Siamese autoencoder learned semantic codewords in the 
 codebook decoder. To determine this we retrieved the most activated bit from the 10 nearest neighbors from each 
 cluster prototype. Since additive vector quantization is used to decode the binary representation the index of the 
 most activated bit corresponds to the most activated code word in the decoder. Table 4 shows the 10 semantically most 
 similar words given the highest activated bit for each cluster prototype.
 
   <img src="http://woutermostard.github.io/files/interpretability.png" align="middle" width="500" height="500">
 
 Some interesting information can be deducted from these code words. First, we see that the fourth bit is frequently
  activated for the Science cluster which seems to be about IT technology. The 20th bit seems to detect verbs and 
  adjectives that would frequently be used in political discussions. The ￿rst bit seems to be detecting names, which
   would often occur in a sports article. Bit number six seems to be about unionization of the work force. Some 
   irrelevant terms, such as paleo and nachos, are also nearest neighbors of the sixth bit. The nearest neighbors of
    the codewords associated with the most activated bits seem relevant for the nearest neighbor of the cluster 
    prototypes given in Table 3. For example, document 1824 seems to be about labor and industry, which is strongly 
    activated with the bit as shown by words such as unionism and Unionists.