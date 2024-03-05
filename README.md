# Named entity recognition

- Link to task data in Google Drive: https://drive.google.com/drive/folders/1Bh-kk8O1iyXPoo4yCGq_EdtgnvSUftOX?usp=sharing

### Dataset preparation:
For the NER task, it is crucial to introduce different classes apart from the class for which the model 
was designed.

For the "back-bone" dataset, I used the [CrossNER dataset](https://github.com/zliucr/CrossNER/tree/main/ner_data/science) which includes classes such as scientist, person, 
university, organization, country, location, discipline, enzyme, protein, chemical compound, chemical 
element, event, astronomical object, academic journal, award, theory, and miscellaneous.

I then prompted ChatGPT-3.5 to generate similar sentences about mountains and added all the classes 
used after the sentences.

The generated data was manually corrected and structured in the same formatting as the "back-bone" 
data. A fraction of the "back-bone" dataset was concatenated with the data generated by GPT-3.5, 
preprocessed, and loaded as a CSV file with text and corresponding labels for each word.

### Dataloader preparation:
To preprocess the CSV file into batched tokens, I utilized a pretrained BERT tokenizer. 
Then, I wrote a function to preserve the correct label for each token, as initially, labels 
were assigned for each word.

Upon creating tokenized text, attention masks, and labeled tensors, I define a dataloader for model 
training. For the NER task, I used the BERT base unbiased model.
### Model inference
For model inference, I used the training portion of the CSV file. The model achieved these results:

Precision: 65,12 %
Recall: 90,32 %
F1 Score: 75,68 %

### Model demonstration
The model demonstration operates with the same test data used in model inference but has a cell 
where you can choose a random sentence from the test set. Then, the model attempts to find all 
mountains mentioned in the text.