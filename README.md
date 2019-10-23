# Entity-Relation Extraction as Multi-turn Question Answering

This repository contains the implemention of our paper [Entity-Relation Extraction as Multi-turn Question Answering
](https://arxiv.org/pdf/1905.05529.pdf) (ACL 2019).

## Information Extraction as Multi-turn QA
### Introduction
As extracting entities and relations from unstructured texts has become a core task in natural language processing, it's still challenging to jointly extract entities and their relations accurately, mostly due to the following existing problems:
- the lack of consideration of hierarchical entity relation behind semantic dependencies
- more complicated realities compared to specially constructed datasets

In this paper, we regard joint entity-relation extraction as a **multi-turn question answering task (multi-turn QA)**: each kind of entity and relation can be described by a QA template, through which the corresponding entity or relation can be extracted from raw texts as answers.

In addition to multi-QA, we also utilize **reinforcement learning** to better extract answers with long template chains. We also design a strategy to automatically generate question templates and answers. More details please refer to our paper.


### Datasets
We trained and evaluated the model using the following datasets:
- **ACE 2004/2005**: the widely used entity-relation extraction benchmarks defining 7 entity types including `PER`, `ORG`, `GPE`, `LOC`, `FAC`, `WEA` and `VEH`, and 7 relation types including `PHYS`, `PER-SOC`, `EMP-ORG`, `ART`, `OTHER-AFF`, `GPE-AFF` and `DISC` for **ACE 2004** while `PHYS`, `PER-SOC`, `EMP-ORG`, `ART`, `GPE-AFF` and `PART-WHOLE` for **ACE 2005**
- **CoNLL 2004**: an entity-relation extraction dataset which defines 4 entity types `LOC`, `ORG`, `PER` and `OTHERS` and 5 relation types including `LOCATED_IN`, `WORK_FOR`, `ORGBASED_IN`, `LIVE_IN` and `KILL`
- **RESUME**:  a newly constructed dataset for joint entity-relation extraction in this paper. This dataset involves hierarchical entity relations consisting of 845 paragraphs from chapters describing teams in IPO prospectuses. **RESUME** defines 4 entity types including `PERSON`, `COMPANY`, `POSITION` and `TIME`. 

### Results
- Results on **RESUME** dataset (F1 score is reported)

  | *Type* | multi-turn QA | multi-turn QA+RL | tagging+dependency | tagging+relation |
  |--|   --- |   ---| --- | --- |
  |PERSON| **98.6** | **98.6** |  97.1 | 97.1 |
  |COMPANY| 84.9 | **85.5** | 84.2 |83.5|
  |POSITION| 97.8 | **98.1** | 97.0 | 96.0 |
  |TIME| 97.7 | **97.9** | 95.7 |94.9 |
  |*All*|92.1|**92.5**|90.8|89.8|

- Results on **ACE 2004** test set (Precision, Recall and F1 are reported)

   *Models* | Enity P | Entity R | Entity F | Relation P | Relation R | Relation F
   --- | --- | --- | --- | --- | --- | --- 
   Li and Ji (2014) |*83.5* | 76.2 | 79.7 | **60.8** |36.1|49.3
   Miwa and Bansal (2016) | 80.8 | **82.9** | *81.8* | 48.7 |*48.1*|*48.4*
  Katiyar and Cardie (2017) | 81.2 | 78.1 | 79.6 | 46.4 | 45.3 | 45.7 
  Bekoulis et al.(2018) | - | - | 81.6 | - | - | 47.5 
  Multi-turn QA| **84.4** | **82.9** | **83.6** | 50.1 | **48.7** | **49.4(+1.0)** 
  
- Results on **ACE 2005** test set (Precision, Recall and F1 are reported)

  | *Models* | Enity P | Entity R | Entity F | Relation P | Relation R | Relation F|
  | --- | --- | --- | --- | --- | --- | --- |
  |Li and Ji (2014)| **85.2** | 76.9| 80.8| **65.4**| 39.8| 49.5|
  |Miwa and Bansal (2016)| 82.9| *83.9*| 83.4| 57.2| 54.0 |55.6|
  |Katiyar and Cardie (2017)| 84.0| 81.3| 82.6| 55.5| 51.8|53.6|
  |Zhang et al. (2017)| -| -| 83.5 |-|- |57.5|
  |Sun et al. (2018) |83.9 |83.2| *83.6*| 64.9| *55.1*| *59.6*|
  |Multi-turn QA |84.7 |**84.9**|**84.8** |64.8| **56.2**| **60.2 (+0.6)**|
  
- Results on **CoNLL 2004** dataset (Precision, Recall and F1 are reported)

  | *Models* | Enity P | Entity R | Entity F | Relation P | Relation R | Relation F|
  | --- | --- | --- | --- | --- | --- | --- |
  |Miwa and Sasaki (2014)| – |– |80.7| –| – |61.0|
  |Zhang et al. (2017) |– |–| 85.6 |– |–| *67.8*|
  |Bekoulis et al. (2018)| – |– |83.6| –| – |62.0|
  |Multi-turn QA |**89.0**| **86.6**| **87.8** |**69.2** |**68.2**| **68.9**| (+1.1)|

## Usage
### Dependencies

### Training

### Evaluation

## Citation

Please cite the following if you find this repo useful :)

```
@inproceedings{li-etal-2019-entity,
    title = "Entity-Relation Extraction as Multi-Turn Question Answering",
    author = "Li, Xiaoya  and
      Yin, Fan  and
      Sun, Zijun  and
      Li, Xiayu  and
      Yuan, Arianna  and
      Chai, Duo  and
      Zhou, Mingxin  and
      Li, Jiwei",
    booktitle = "Proceedings of the 57th Annual Meeting of the Association for Computational Linguistics",
    month = jul,
    year = "2019",
    address = "Florence, Italy",
    publisher = "Association for Computational Linguistics",
    url = "https://www.aclweb.org/anthology/P19-1129",
    doi = "10.18653/v1/P19-1129",
    pages = "1340--1350",
}
```

## License
Refer to [LICENCE](https://github.com/ShannonAI/Entity-Relation-As-Multi-Turn-QA/blob/master/LICENSE) for details.
