# Claim Extraction for Scientific Publications

Detecting claim from scientific publication using discourse and sentence embedding.


## Training discourse model

Running AllenNLP to train discourse model as follows

```bash
python -m allennlp.run train pubmed_rct.json -s output --include-package discourse
```

or

```bash
allennlp train pubmed_rct.json -s output --include-package discourse
```

We point data location to Amazon S3 directly in `pubmed_rct.json`
so you do not need to download the data locally. Change `cuda_device` to `-1` in `pubmed_rct.json`
if you want to run on CPU.

**Note** that you have to remove `output` folder first before running.


## Web service

You can download trained model

```bash
wget https://s3-us-west-2.amazonaws.com/pubmed-rct/model.tar.gz
```

and run web service for discourse prediction task as follow

```bash
bash web_service.sh
```

To test the train model with provided examples [`fixtures.json`](pubmed-rct/PubMed_200k_RCT/fixtures.json),
simply run the following to predict labels.


```bash
allennlp predict \
    model.tar.gz \
    pubmed-rct/PubMed_200k_RCT/fixtures.json \
    --include-package discourse \
    --predictor discourse_classifier
```


## Predicting claim

First, download fastText pre-trained word vector and unzip it, put in this folder

```bash
wget https://s3-us-west-1.amazonaws.com/fasttext-vectors/wiki.en.zip
```

You can test running `flask` app to detect the claim as follows

```bash
export FLASK_APP=main.py
flask run --host=0.0.0.0 --port 5000
```

The interface will look something like this

<p float="left">
  <img src="static/interface.png" width="600" />
</p>


We will release a dataset and model of scientific claims tagged by expert soon (in few months).


## Requirements

- [Pubmed RCT](https://github.com/Franck-Dernoncourt/pubmed-rct) - dataset
- [AllenNLP](https://github.com/allenai/allennlp)
- [spacy](https://github.com/explosion/spaCy)
- [fastText](https://github.com/facebookresearch/fastText)


## Acknowledgement

This project is done at the [Allen Institute for Artificial Intelligence](https://allenai.org/)
and [Konrad Kording lab, University of Pennsylvania](http://kordinglab.com/)
