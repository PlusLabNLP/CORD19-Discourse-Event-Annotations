# Biomedical Discourse Analysis and Event Extraction for CORD-19

<a href="https://pluslabnlp.github.io/"><img src="https://pluslabnlp.github.io/images/Logos/logo_transparent_background.png" height="120" ></a>
<a href="https://www.isi.edu/"><img src="https://pluslabnlp.github.io/images/usc-logo.png"  height="120"></a>



## Introduction
With the increasing concern about the COVID-19 pandemic, researchers have been putting much effort in providing useful insights into the [COVID-19 Open Research Dataset Challenge (CORD-19)](https://www.kaggle.com/allen-institute-for-ai/CORD-19-research-challenge/). This repo contains two types of NLP annotations on the CORD-19 dataset, using the capability we developed under the NIH R01 project ["Evidence Extraction for the Molecular Interaction Literature" (LM012592)](https://projectreporter.nih.gov/project_info_description.cfm?aid=9543557&icde=41363289&ddparam=&ddvalue=&ddsub=&cr=1&csb=default&cs=ASC&pball=), Including

### Biomedical discourse tagging
The discourse analysis results can be found [here](https://drive.google.com/file/d/1vZyL-V7JOgygVGwVorJu-pFFEMbi9Biv/view?usp=sharing).
### Biomedical event extraction
The extracted events for the PMC proportion can be found [here](https://drive.google.com/file/d/1FXN2QRBoFzQmLwQztUhULm8WVKxyRwu3/view?usp=sharing).


## Description
We provide more details about how do we generate these NLP annotations and some benchmark performances of these annotations.

### Biomedical discourse tagging

### Biomedical event extraction 
<p align="center"><img src="https://github.com/jbjorne/TEES/wiki/TEES-process.png"   style="margin:auto"></p>


## Performance

### Biomedical discourse tagging

### Biomedical event extraction 
Currently, this repo contains only the fine-tuned SciBERT on the GENIA dataset, whose performance is on par with the previous SOTA result. The best performing model with UMLS (a large biomedical knowledge grapah) and GNN incorporation will soon be released.
| Model        | Dev Set F1           | Test Set F1  |
| ------------- |-------------:| -----:|
|   SciBERT Baseline    | 59.33      |   58.50  |
|   SciBERT w/ UMLS & GNN (coming soon)   | **60.38** | **60.06** |
| [Previous SOTA](https://www.aclweb.org/anthology/N19-1145.pdf) | N/A      |   58.65  |
