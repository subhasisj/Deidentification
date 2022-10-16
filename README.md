We used i2b2 as an example to illustrate how Clinical-Longformer can be applied to NER tasks.
1. Download i2b2 2006, 2010, 2012, 2014 dataset at: https://portal.dbmi.hms.harvard.edu/projects/n2c2-nlp/. N2C2 access should be requested.
2. Pre-process i2b2 and formulate the dataset to .json format. We used this [repo](https://github.com/EmilyAlsentzer/clinicalBERT/tree/master/downstream_tasks/i2b2_preprocessing). Please also cite there NAACL paper, if you think it is useful.
3. On running the previous 2 steps, you shall have such directory structure

```
## Dowload pre-trained UmlsBERT model

In order to use pre-trained  UmlsBERT model for the word embeddings (or the semantic embeddings), you need to dowload it into the folder examples/checkpoint/ from the link:
```
 wget -O umlsbert.tar.xz https://www.dropbox.com/s/kziiuyhv9ile00s/umlsbert.tar.xz?dl=0
```

into the folder examples/checkpoint/ and unzip it with the following command:
```
tar -xvf umlsbert.tar.xz


**NER task**
- Due to the copyright issue of i2b2 datasets, in order to download them follow the [link](https://www.i2b2.org/NLP/DataSets/Main.php).

   - **Converting into an appropriate format**: Since we wanted to directly compare with the Bio_clinical_Bert we used their code in order to convert the i2b2 dataset to a format which is appropriate for the BERT architecture which can be found in the following link: [link](https://github.com/EmilyAlsentzer/clinicalBERT/tree/master/downstream_tasks/i2b2_preprocessing) 
   
   We  provide the code for converting the i2b2 dataset with the following instruction for each dataset:

- i2b2 2006:
  - In the folder *token-classification/dataset/i2b2_preprocessing/i2b2_2006_deid* unzip the **deid_surrogate_test_all_groundtruth_version2.zip** and **deid_surrogate_train_all_version2.zip**
  - run the **create.sh** scrip with the command
    ./create.sh
  - The script will create the files: label.txt, dev.txt, test.txt, train.txt  in the *token-classification/dataset/NER/2006* folder
- i2b2 2010:
  - In the folder *token-classification/dataset/i2b2_preprocessing/i2b2_2010_relations* unzip the **test_data.tar.gz**, **concept_assertion_relation_training_data.tar.gz** and **reference_standard_for_test_data.tar.gz**
  - Run the jupyter notebook **Reformat.ipynb**
  - The notebook will create the files: label.txt, dev.txt, test.txt, train.txt  in the *token-classification/dataset/NER/2010* folder

- i2b2 2012:
  - In the folder *token-classification/dataset/i2b2_preprocessing/i2b2_2012* unzip the **2012-07-15.original-annotation.release.tar.gz** and **2012-08-08.test-data.event-timex-groundtruth.tar.gz**
  - Run the jupyter notebook **Reformat.ipynb**
  - The notebook will create the files: label.txt, dev.txt, test.txt, train.txt  in the *token-classification/dataset/NER/2012* folder

- i2b2 2014:
  - In the folder *token-classification/dataset/i2b2_preprocessing/i2b2_2014_deid_hf_risk* unzip the **2014_training-PHI-Gold-Set1.tar.gz**,**training-PHI-Gold-Set2.tar.gz** and **testing-PHI-Gold-fixed.tar.gz**
  - Run the jupyter notebook **Reformat.ipynb**
  - The notebook will create the files: label.txt, dev.txt, test.txt, train.txt  in the *token-classification/dataset/NER/2014* folder

- We provide an example-notebook under the folder  *experiements/*:
  - [ *experiements/NER_task.ipynb*](https://github.com/gmichalo/UmlsBERT/blob/master/experiments/NER_task.ipynb)

or directly run UmlsBert on the *token-classification/* folder:

```
python3 run_ner.py --output_dir ./models/medicalBert-v1 --model_name_or_path  ../checkpoint/umlsbert    --labels dataset/NER/2006/label.txt --data_dir  dataset/NER/2006 --do_train --num_train_epochs 20 --per_device_train_batch_size 32  --learning_rate 1e-4  --do_predict --do_eval --umls --med_document ./voc/vocab_updated.txt
```