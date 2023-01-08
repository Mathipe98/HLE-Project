# HLE-Project

This is a repository containing the code developed for a NLP-related project in the course HLE - Human Language Engineering, taken at UPC - Uinversitat Politècnica de Catalunya
in Autumn 2022.

The course in general dealt with advanced NLP-techniques and state-of-the-art models/architectures, and the main project was an open project with the requirement being relevancy
to modern NLP architectures and trying to focus on some area that hadn't already been completed.

In our case, we elected to focus on the Norwegian part of the NLP world, seeing as the large majority of all NLP-related projects are doing so in English. We therefore decided
to create an architecture that attempted to classify news articles such that it would be possible to distinguish between different "kinds" of articles. Thus we created our own
classification-problem.

To achieve this, we first scraped data from [Dagbladet](https://dagbladet.no) in order to generate a dataset. We arranged the data to consist of headline, subtitle (summary),
keywords, and category. The category was the classification-target, and we used the other variables for further processing.

We ran the scraped data through various pipelines based on pre-trained models from [Norwegian NLP Resources](https://github.com/web64/norwegian-nlp-resources).
This included nb-sbert-base for topic- and keyword-extraction, nbailab-base-ner-scandi for NER (Named Entity Recognition), and
finally nb-bert-large for the final classification. The latter model was the only one trained for fine-tuning, while the others
were used out of the box. The below figure shows the complete architecture:

![Architecture](/figures/architecture.jpg?raw=true "Complete Architecture")

## Directories

**_data_** contains the various CSV-files that were generated throughout the project, where the file "Preprocessed_Data.csv" is the
final version which is formatted into train/test.csv .

**_notebooks_** contains the various Jupyter Notebook-files that we used for different steps of the project:

* **Preprocessing.ipynb**: Notebook that contains all preprocessing applied to the original dataframe, including data-cleaning and feature engineering (through aforementioned NLP models)
* **Format_Data.ipynb**: Notebook that turns the preprocessed data into a format that is suitable for the main BERT-model. This includes one-hot encoding the target, as well as taking all processed features and combining them into one single text-sequence.
* **Train_Classification.ipynb**: Notebook that takes the formatted data, imports the pre-trained BERT-model, and tokenizes/embeds all inputs in order to start training. This is where we fine-tune the original model to our classification-problem.
* **Traditional_clf_baseline_results.ipynb**: Notebook containing a reference point for classification, where we used LRC (Logistic Regression Classifier), SVC (Support Vector Classifier), and DTC (Decision Tree Classifier). This was to have a comparison between our fine-tuned BERT-model and more traditional, mathematical approaches.

**_figures_** contains the various figures that were used and generated.