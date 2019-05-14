# Shifting Gender Associations in Word Embeddings

 for Natural Language Processing Final Project 
  MIDS Program 
  University of California, Berkeley 
  madeleinebulkow@gmail.com


  The documented biases encoded in vector representations of words present difficulties for those hoping to use these embeddings in practical applications, but also present an opportunity to study the way in which language is used to carry cultural biases and associations. This paper investigates this relationship between culture and language by trying to discern whether the significant changes in gender roles and politics over the past two centuries can be observed through language. Although the results are inconclusive, the general finding is that gender related words show significant changes, but that these changes may not necessarily translate neatly into a decreased measure of bias.


## Introduction

Given the widespread use of word embeddings in natural language processing, the presence of undesired biases in these embeddings poses a significant liability to many potential applications. While various attempts have been made to eliminate these biases \cite{bolukbasi16a} \cite{bolukbasi16b}, the implicit and often subtle biases of the training data have proved difficult to fully excise \cite{lipstick}. Rather than offering an algorithm that claims to solve the problem, this paper seeks to shed light on the roots of the problem by examining various measures of bias in word embeddings based on data spanning the last two centuries.

## Background

The underlying biases in word embeddings were brought to the attention of the wider natural language processing community by Bolukbasi in 2016 \cite{bolukbasi16a}. This paper highlighted the problem through the use of analogy completion. The ability of word embedding to solve logical analogies through simple vector addition is one of its more surprising traits, and useful as a metric of the "accuracy" of the relationship inferred by the training algorithm - it is at times even used as a formal metric for assessing the quality of a model \cite{mikolov13}. However, Bolukbasi illustrated a more uncomfortable side to these analogies: many of the completions suggested by the geometry of the embedding space showed offensive biases- for instance, "man:woman :: doctor:nurse" \cite{bolukbasi16a}.

Of course, such offensive analogies could arise occasionally from chance alignments. A formal test of the hypothesis that word embeddings show bias was introduced by Caliskan et al. in the form of of the Word Embedding Association Test (WEAT) \cite{caliskan16}. In this test, two target groups are compared by looking at their mean cosine similarity with each of two attribute groups. That is, for each target group $X$, we evaluate the sum:
$$ \sum_{x\in X} \texttt{mean}_{a\in A}cos(a,x) - \texttt{mean}_{b\in B}cos(b,x) $$
where $A$ and $B$ are attribute groups (cite). In essence, this test provides a formal statistic for judging the relative proximity of the target groups to each of the attribute groups. A significant result in this statistic suggests bias exists in the relationship of the target groups to the attribute groups: for instance, if a target group of typically female names is closer to art-related attributes and further from science-related attributes than a corresponding group of typically male names, this suggests bias exists in this dimension.

Recent research by Gonen and Goldberg suggests that even where solutions can "neutralize" bias with respect to this kind of metric, the persistent clustering of associated terms can allow for recovery of the biased dimension \cite{lipstick}. This means that while minimizing the appearance of bias, current "debiasing" techniques leave enough bias-informed residue for an NLP algorithm to nonetheless learn biased results. As such, it is more important than ever to understand the biases that are transmitted by our language data.

## Methods

Our overall approach was to learn a distinct set of word embeddings for every decade over the past two centuries, then measure and visualize the degrees of biases (both in terms of analogies and in terms of the WEAT statistic) over time. 

To train our embeddings, we used portions of the Google Ngram English One Million dataset, which provides phrases and their frequencies over the past several hundred years \cite{ngram}. This dataset offers consistent coverage of the time period we wish to study, since for every year after 1800, the corpus the phrases are drawn from exceeds 100 million words. For consistency, and in order to obtain a vocabulary that was appropriate for the entire time period, we also used this dataset to select relatively frequent words (specifically, those that appeared more than 500,000 times in the dataset, since this gave us a manageably sized vocabulary of around 10,000 words). 

The embedding algorithm we chose was Skip-gram with noise-contrastive estimation, due to its strong performance on analogies in \cite{mikolov13}, relative ease of implementation \cite{tfskipgram} and its prevalence in literature. This algorithm seeks to guess the context words that exist in a window (in our case, four words on either side) around a given input word, by creating a lower dimensional (in our case, 300 dimensional) embedding on the input word, then evaluating the likelihood of various output words (both the correct output, and a sample of counter-examples). The embedding matrix and the noise-contrastive estimation weights were initialized uniformly at random to values between -1 and 1. By using the same random seed in every decade, we sought to encourage a similar geometry of embeddings, so that any differences in the learned embeddings could be attributed fully to differences in training data.

The first step in evaluating the bias in these embeddings was visual inspection of the performance of analogies over time. That is, given a target word "d" and an analogy "a:b :: c: ?", we graphed the degree of cosine similarity between "c - a + b" and "d" over time. This was meant to give a rough inspection of the degree to which the relationship between "d" and "c" could be characterized as analogous to the relationship between "a" and "b." However, likely due to insufficient training time, our model performed extremely poorly on analogies in general, so this was not included among our results.

For a more quantitative measure of bias, we turned to the WEAT statistic developed by Caliskan \cite{caliskan16}. Following their examples we use the stimuli found in Nosek \cite{nosek2002math} to evaluate math vs. art-related target groups with respect to masculine vs. feminine attribute groups. We did the same with domestic and math-related target groups, and domestic and art-related target groups. The target and attribute lists used are given in 

\begin{table}
    \centering
\begin{tabularx}{\linewidth}{|L|L|} 
    \hline
\textbf{Art Target}  & poetry, art, Shakespeare, dance, 
         literature, novel, symphony, drama \\
    \hline
\textbf{Math Target}  & math, algebra, geometry, calculus, equations, computation, numbers, Newton \\
   \hline
\textbf{Domestic Target}  & house, home, clean, sew, children, cook, garden, laundry\\
    \hline
\hline
\textbf{Feminine Attribute}  & sister, mother, aunt, grandmother, daughter, she, hers, her\\
    \hline
\textbf{Masculine Atrribute}  & brother, father, uncle, grandfather, son, he, his, him\\
\hline
\end{tabularx}
\caption{Target and Attribute word groups for use with the WEAT statistic.}
    \label{tab:my_label}
    \end{table}
Finally, in the interest of better understanding the underlying representation of gender in our vector space, we looked at the cosine similarity between third person pronouns over time. Since pronouns are more common than any specific name and most gender-related words, they had the most related data available in every decade. 

\section{Results}

The necessary caveat to this section is that due to technical constraints, neither the training time nor the size of the vocabulary was as large as might be hoped. This led to difficulties in successfully predicting analogies, biased or otherwise. However, sufficient observations relating to mere cosine similarity were made to justify presentation here, in the hopes of prompting future investigation.

The performance of the WEAT statistic over time (Figure. \ref{fig:weat}) does not show any immediately obvious trends over the full time period. All three relationships seem to remain approximately neutral across most of the time frame. Further training might help smooth some of the jitter that is attributable to random noise. Additionally, there are areas of the plot where trends might be visible (for instance, over the last forty years) if examined in higher resolution, or if the beginning and end of that era were examined with a specific hypothesis in mind.

\begin{figure*}
  \centering
  \includegraphics[width=6in]{weat.png}
  \caption{Relative proximity of target groups to feminine or masculine attribute groups. A positive value indicates the first target group is embedded as more feminine or less masculine than the second.}
  \label{fig:weat}
\end{figure*}

The cosine similarity of pronouns (Figure. \ref{fig:pronouns}) over time is more suggestive. There seems to be a positive trend in the relationship between "she" and "he", and "she" and "they", while the relationship between "he" and "they" remains approximately stable. 

Given the nature of the Skip Gram algorithm, we expect two words to have similar embeddings if they occur in similar contexts. Since "she" and "he" are both singular third person pronouns, the grammar of the surrounding phrase should be the same. The positive trend, then, indicates that "she" and "he" are more likely to be used in approximately interchangeable ways now than they were two hundred years ago. 

Also of interest is the relative proximity of "they" to "he" rather than "she". Although "they", in either its singular or plural sense, is gender neutral, the relationship with "he" is consistently positive, while "she" is initially negative. The positive trend in the "she/they" relationship mirrors the "she/he" relationship closely. This might suggest that while "he" and "they" have remained approximately stationary in terms of their contexts, "she" has undergone a significant context shift which has brought it closer to the other third-person pronouns. 


\begin{figure*}
  \centering
  \includegraphics[width=6in]{cos_sim_pronouns_third.png}
  \caption{Cosine similarity between third person pronouns over time. Higher cosine similarity indicates that the pronouns appear in similar contexts.}
  \label{fig:pronouns}
\end{figure*}

## Conclusion

The behaviour of gender-related words over time does not appear to  be as neat as initially hoped. While there does seem to be a gender-related shift in the geometry of word-embeddings, it is not as simple as a monotonically decreasing level of bias.

Further research is needed into the specifics trends in diachronic word embeddings. Since the main difficulty encountered during this research was the difficulty of training distinct embeddings for twenty decades worth of data, we would suggest further research focus on a shorter time period. Additional training, as well as the implementation of subsampling to better represent rare words (as in \cite{mikolov13}) could produce more reliable analogy-solvers, and hopefully eliminate some of the noise seen in the WEAT statistic. 

Finally, the results of this paper encourage further study of the shifting contexts surrounding gendered words such as "he" and "she". Although not a solution to bias on its own, better understanding of the relationship of bias, culture, and language may help us learn to recognize and combat gender bias in NLP.
 