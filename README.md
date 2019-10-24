# Entity-Relation Extraction as Multi-turn Question Answering

This is the implementation of the work [Entity-Relation Extraction as Multi-turn Question Answering (ACL 2019)
](https://arxiv.org/pdf/1905.05529.pdf) from [Shannon.AI](http://www.shannonai.com). The implementation is on top of PyTorch.  

## Introduction
- the lack of consideration of hierarchical entity relation behind semantic dependencies
- more complicated realities compared to handcrafted datasets

In this paper, we regard joint entity-relation extraction as a **multi-turn question answering task (multi-turn QA)**: each kind of entity and relation can be described by a QA template, through which the corresponding entity or relation can be extracted from raw texts as answers.

In addition to multi-QA, we also utilize **reinforcement learning** to better extract answers with long template chains. We also design a strategy to automatically generate question templates and answers. More details please refer to our paper.


## Experimental Results

Evalutations are conducted on the widely used datasets `ACE 2004`, `ACE 2005` and `CoNLL 2004`.  
We report micro precision, recall and F1-score for entity and relation extractions. 
We only list the experimental comparion between the proposed method and **previous** `state-of-the-art` model. More experimental comparions are shown in paper. 

- Results on **ACE 2004**:

   *Models* | Enity P | Entity R | Entity F | Relation P | Relation R | Relation F
   --- | --- | --- | --- | --- | --- | --- 
   Miwa and Bansal (2016) | 80.8 | 82.9 | 81.8 | 48.7 | 48.1 | 48.4 
  Multi-turn QA| 84.4 | 82.9 | **83.6** | 50.1 | **48.7** | **49.4 (+1.0)** 
  
- Results on **ACE 2005**:

  | *Models* | Enity P | Entity R | Entity F | Relation P | Relation R | Relation F|
  | --- | --- | --- | --- | --- | --- | --- |
  |Sun et al. (2018) |83.9 s|83.2| 83.6| 64.9| 55.1| 59.6|
  |Multi-turn QA |84.7 |84.9|**84.8** |64.8| 56.2| **60.2 (+0.6)**|
  
- Results on **CoNLL 2004**:

  | *Models* | Enity P | Entity R | Entity F | Relation P | Relation R | Relation F|
  | --- | --- | --- | --- | --- | --- | --- |
  |Zhang et al. (2017) |– |–| 85.6 |– |–| 67.8|
  |Multi-turn QA | 89.0 | 86.6 | **87.8** | 69.2 | 68.2 | **68.9 (+1.1)**|

## Usage
### Dataset Preparation 
1. Download original datasets from:
	* ACE 2004 `https://catalog.ldc.upenn.edu/LDC2005T09`
	* ACE 2005 `https://catalog.ldc.upenn.edu/LDC2006T06`
	* CoNLL 2004 `https://cogcomp.seas.upenn.edu/Data/ER/conll04.corp`
2. Split datasets following the previous work: 
	* ACE 2004 `https://github.com/tticoin/LSTM-ER/`
	* ACE 2005 `https://github.com/tticoin/LSTM-ER/`
	* CoNLL 2004 `https://github.com/bekou/multihead_joint_entity_relation_extraction/tree/master/data/CoNLL04`
3. Transform data to Question-Answering scheme:
	
	Convert data from `Relation(Entity1, Entity2)` to `(Question, Answer, Context)`. 
	
	Take `ACE 2004` dataset for example: 

	```bash 
	export TASK_NAME=ace2004 
	export ORIGIN_DATA_PATH=/path/to/ace2004
	export EXPORT_DATA_PATH=/path/to/convert_qa_scheme
	
	cd utils/
	python3 prep_qa_data.py --data_sign $TASK_NAME \
		--origin_data_path $ORIGIN_DATA_PATH \
		--export_data_path $EXPORT_DATA_PATH 
	```
	After this, you will have a `ace2004` subdirectory under the folder of `/path/to/convert_qa_scheme`. The folder of `ace2004` contains the experiments files for entity and relation extraction tasks. 
	
	The `TASK_NAME` can be `ace2004`, `ace2005`, `conll2004`.
	
	
	
	
	The folder of `ace2004` contains train/validate/test files for the task of entity extraction and relation classification. 

### Software Dependencies
* Python version >= 3.6
* PyTorch == 1.1.0
* Download and unzip `BERT-Large, English` pretrained model. 
* Install `pip install pytorch-pretrained-bert==1.1.0`
* Transform the model checkpoint from `*.ckpt` to `*.bin`.   
	`*.ckpt` represents the TensorFlow checkpoint. `*.bin` represents the PyTorch checkpoint. 

	```bash 
	export BERT_BASE_DIR=/path/to/bert/chinese_L-12_H-768_A-12

	pytorch_pretrained_bert convert_tf_checkpoint_to_pytorch \
	$BERT_BASE_DIR/bert_model.ckpt \
	$BERT_BASE_DIR/bert_config.json \
	$BERT_BASE_DIR/pytorch_model.bin
	```


### Training
pass 



### Evaluation
In order to evaluate the performance of a saved checkpoint, you need to use the `utils/evaluate_performance.py` file. Please use the following command:

```bash 
pass 
```


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
Refer to [LISENCE](https://github.com/ShannonAI/Entity-Relation-As-Multi-Turn-QA/blob/master/LICENSE) for details.