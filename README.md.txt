%
% File acl2015.tex
%
% Contact: car@ir.hit.edu.cn, gdzhou@suda.edu.cn
%%
%% Based on the style files for ACL-2014, which were, in turn,
%% Based on the style files for ACL-2013, which were, in turn,
%% Based on the style files for ACL-2012, which were, in turn,
%% based on the style files for ACL-2011, which were, in turn, 
%% based on the style files for ACL-2010, which were, in turn, 
%% based on the style files for ACL-IJCNLP-2009, which were, in turn,
%% based on the style files for EACL-2009 and IJCNLP-2008...

%% Based on the style files for EACL 2006 by 
%%e.agirre@ehu.es or Sergi.Balari@uab.es
%% and that of ACL 08 by Joakim Nivre and Noah Smith

\documentclass[11pt]{article}
\usepackage{acl2015}
\usepackage{times}
\usepackage{url}
\usepackage{latexsym}
\usepackage{graphicx}
\usepackage{tabularx}
    \newcolumntype{L}{>{\raggedright\arraybackslash}X}

%\setlength\titlebox{5cm}

% You can expand the titlebox if you need extra space
% to show all the authors. Please do not make the titlebox
% smaller than 5cm (the original size); we will check this
% in the camera-ready version and ask you to change it back.


\title{Shifting Gender Associations in Word Embeddings}

\author{Madeleine Bulkow-Macy \\
  Natural Language Processing Final Project \\
  MIDS Program \\
  University of California, Berkeley \\
  {\tt madeleinebulkow@gmail.com} \\}

\date{}

\begin{document}
\maketitle
\begin{abstract}
  The documented biases encoded in vector representations of words present difficulties for those hoping to use these embeddings in practical applications, but also present an opportunity to study the way in which language is used to carry cultural biases and associations. This paper investigates this relationship between culture and language by trying to discern whether the significant changes in gender roles and politics over the past two centuries can be observed through language. Although the results are inconclusive, the general finding is that gender related words show significant changes, but that these changes may not necessarily translate neatly into a decreased measure of bias.
\end{abstract}

\section{Introduction}

Given the widespread use of word embeddings in natural language processing, the presence of undesired biases in these embeddings poses a significant liability to many potential applications. While various attempts have been made to eliminate these biases \cite{bolukbasi16a} \cite{bolukbasi16b}, the implicit and often subtle biases of the training data have proved difficult to fully excise \cite{lipstick}. Rather than offering an algorithm that claims to solve the problem, this paper seeks to shed light on the roots of the problem by examining various measures of bias in word embeddings based on data spanning the last two centuries.

\section{Background}

The underlying biases in word embeddings were brought to the attention of the wider natural language processing community by Bolukbasi in 2016 \cite{bolukbasi16a}. This paper h