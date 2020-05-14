# Biomedical Discourse Analysis and Event Extraction for CORD-19

<a href="https://pluslabnlp.github.io/"><img src="https://pluslabnlp.github.io/images/Logos/logo_transparent_background.png" height="120" ></a>
<a href="https://www.isi.edu/"><img src="https://pluslabnlp.github.io/images/usc-logo.png"  height="120"></a>



## Introduction
With the increasing concern about the COVID-19 pandemic, researchers have been putting much effort in providing useful insights into the [COVID-19 Open Research Dataset Challenge (CORD-19)](https://www.kaggle.com/allen-institute-for-ai/CORD-19-research-challenge/). This repo contains two types of NLP annotations on the CORD-19 dataset, using the capability we developed under the NIH R01 project ["Evidence Extraction for the Molecular Interaction Literature" (LM012592)](https://projectreporter.nih.gov/project_info_description.cfm?aid=9543557&icde=41363289&ddparam=&ddvalue=&ddsub=&cr=1&csb=default&cs=ASC&pball=), Including

* __Biomedical discourse tagging__: The discourse analysis results can be found [here](https://drive.google.com/file/d/1vZyL-V7JOgygVGwVorJu-pFFEMbi9Biv/view?usp=sharing).
* __Biomedical event extraction__: The extracted events for the PMC proportion can be found [here](https://drive.google.com/file/d/1FXN2QRBoFzQmLwQztUhULm8WVKxyRwu3/view?usp=sharing).


## Description
We provide more details about how do we generate these NLP annotations and some benchmark performances of these annotations.

#### Biomedical discourse tagging

#### Biomedical event extraction 

We took reference from the pipeline described in  *Generalizing Biomedical Event Extraction (Bjorne et al. 2009)*, where the pipeline can be broken into 3 stages: trigger detection, edge detection and unmerging. 
<p align="center"><img src="https://github.com/jbjorne/TEES/wiki/TEES-process.png"   style="margin:auto"></p>


We leveraged SciBERT from *SciBERT: A Pretrained Language Model for Scientific Text (Ammar et al. 2018)* as our base model. It is a language model based on BERT pre-trained on 1.14M scientific papers from Semantic Scholar with the same configuration as BERT-BASE. SciBERT has demonstrated SOTA performance on a number of NLP tasks in various domains, including Biomedicine. We use SciBERT to produce contextualized embeddings <img src="https://render.githubusercontent.com/render/math?math=h_{i}"> that contain rich semantic and syntatic information.

The model was trained in a pipeline-multitask setting, consisting of trigger classification and relation classification. For trigger classification, each token is associated with a label indicating its trigger type or protein. If a token is neither a trigger nor a protein, it is labeled as *None*. The output is obtained by feeding the contextualized representation to a feed-forward network  <img src="https://render.githubusercontent.com/render/math?math=\hat{y}^{tri}_{i} = \textrm{FFN}^{tri}(h_{i})"> for the *i*-th token. In the relation classification stage, all possible combinations of triggers and arguments are gathered, labelled with their corresponding argument roles. We concatenate the representations of the head and tail embeddings and feed it to a another feed-forward network <img src="https://render.githubusercontent.com/render/math?math=\hat{y}^{rel}_{i} = \textrm{FFN}^{rel}(h_{i})">. We use cross entropy for both tasks as follows,

<img src="https://render.githubusercontent.com/render/math?math=L^{t} = - \frac{1}{N^{t}}\sum_{i=1}^{N^{t}}  y^{t}_{i} \cdot \log\hat{y}^{t}_{i}, ">  
where t denotes different tasks, and <img src="https://render.githubusercontent.com/render/math?math=N^{t}"> denotes the number of instances for task t. The model was optimized with BERTAdam by minimizing the sum of the two losses.



## Performance

* Biomedical discourse tagging

* Biomedical event extraction 

Currently, this repo contains only the fine-tuned SciBERT Baseline on the GENIA dataset, whose performance is on par with the previous SOTA result. The best performing model with UMLS (a large biomedical knowledge grapah) and GNN incorporation will soon be released.

| Model        | Dev Set F1           | Test Set F1  |
| ------------- |-------------:| -----:|
|   SciBERT Baseline    | 59.33      |   58.50  |
|   SciBERT w/ UMLS & GNN (coming soon)   | **60.38** | **60.06** |
| [Previous SOTA](https://www.aclweb.org/anthology/N19-1145.pdf) | N/A      |   58.65  |
