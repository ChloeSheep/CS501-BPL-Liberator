
# Downloading Data
Download data using the ```./utils/download-liberator.py``` and the included CSV file 

Currently this downloads ALL of the data, which may quickly eliminate all your free space (needs editing).

# Pipeline Overview 
Full pipleline demonstration in [PipelineExample.ipynb](https://github.com/SikandAlex/CS501-BPL-Liberator/blob/main/ocr/PipelineExample.ipynb)

## Column Detection (Using Frequency Information)
Pipeline capable of [detecting columns](https://github.com/jscancella/NYTribuneOCRExperiments/blob/master/findText_usingSums.py) from newspaper scans without using any deep learning (using frequency information) in OpenCV

<img src="./ocr/tester-contours.jpeg" width="400"/>

## OCR (Optical Character Recognition) 
Google Cloud Vision - [Document Text Detection](https://cloud.google.com/vision/docs/ocr)

<img src="./media/google-cloud-vision-ocr.png" height="250"/>

## Spell Correction
[autocorrect](https://github.com/fsondej/autocorrect) Python library

## OOTB NER
```python -m spacy download (en_core_web_sm or en_core_web_trf)```
### (NO GPU)
```spacy.load('en_core_web_sm')``` (small model)
### (GPU)
```spacy.load('en_core_web_trf')``` (transformer based model)

# Object Detection 
Proposed faster-rcnn model to extract article start/stop markers from the newspaper
[faster-rcnn implementation](https://colab.research.google.com/github/a8252525/detectron2_example_PCBdata/blob/master/PCBdata_fasterRCNN_colab.ipynb#scrollTo=WyR8yIqPFcNn)

## Extracting Articles from Column Image OCR
Detect titles + start/end article markers using a 1-3 class object detection model

## Labeling Data for Object Detection (not completed)
1) Label the data with bounding boxes using [Label Studio](labelstud.io)
2) Export in COCO format 

# Prototype NER (Named Entity Detection) LoC Entity Labeling Tool 

### Starting the web-app
streamlit run ```./ner/app.py```

Assuming that we need to know more than just the type of entity, we also need to assign the entity to a Library of Congress identifier. For this purpose, we have created a basic web application using [Streamlit](streamlit.io). 

<img src="./media/web-app.png" height="500"/>

The sample text is hard-coded for now but you can select one of the recognized entities in the sidebar and attempt to retrieve the top search results from the Loc API. 

To Do: It needs to be better and more tightly integrated with the LoC API. In addition, currently, when fetching data, the UI hangs because it's not being done asynchronously or something so that needs to be handled. We also need a submit button and a way to somehow save the labels to a data structure or file. 

<img src="./media/loc-retrieve.png" height="400"/>

