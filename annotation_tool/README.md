# Sentence Annotation Tool (WIP)

Along with discourse and claim prediction tool, we also release
annotation tool that we made to collect claim dataset.


### Annotation Tool Web Service

All parameters are located in `params.yaml` include the following

- `pmids_path` is a path to list of PMIDs that you want to tag, default as `data/pmids.txt`
- `labels` is a list of labels that you want to annotate
- `output_path` is a path to output file, default as `data/labels.json`

The instructions for annotators can be edited in `flask_templates/index.html`.
After editing YAML file, you can run `flask` to start the annotation tool.

```bash
export FLASK_APP=main.py
flask run --host=0.0.0.0 # this will serve at port 5000
```

The data will be saved in default location at `data/labels.json` where
each lines contains JSON of title, abstract, sentences, and labels.
