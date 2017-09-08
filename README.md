# PDF Classifier for a Mortgage Company

Often mortgage companies get hundreds of PDFs a day and many hours are spent by
employees to classify and file these PDFs.  This essentially costs businesses a
lot of money because employees need to spend time sorting and filing these PDFs
instead of completing other tasks essential to the business, so my goal was to
create a classifier that could address this issue and ultimately save both employees
time and the business money.  This pipeline contains scripts to decrypt these PDFs
to allow for text extraction, extract and analyze the text, and then predict
their classification based on various models.


# Prerequisites

1. QPDF
2. PDFminer
3. PyOCR

Tips to installing PDFminer:
https://media.readthedocs.org/pdf/pdfminer-docs/latest/pdfminer-docs.pdf
Tips to installing PyOCR:
https://pythontips.com/2016/02/25/ocr-on-pdf-files-using-python/


# Getting Started

Step One:

Decrypt the files

1. Decrypt PDFs so that text extraction is possible
2. Covert PDFs to text files
  1. convert_pdfDir() - uses PDFminer to convert PDFs with forms or text layers
  2. strip_blank - gets rid of blank documents that PDFminer could not extract
      text from and uses OCR to complete those documents
3. Run models



# Running the PDFminer model:

dictionary = get_dict('/Users/matthewwong/dsi-capstone/miner_Text/')
docs, labels = seperate(dictionary)
training_docs, test_docs, training_labels, test_labels = train_test_split(\
   docs, labels, stratify=labels, test_size=0.25)
categories = categories(dictionary)
tfidfed = tfidf.fit_transform(training_docs)


nb_predictions = classify_nb(test_docs, tfidfed, training_labels)
cos_predictions = classify_avg_cos(categories, test_docs, tfidfed, training_labels)
knn_predictions = classify_knn_cos(test_docs, tfidfed, training_labels)



# Running the PDFminer and PyOCR model:

dictionary = get_dict('/Users/matthewwong/dsi-capstone/Text/')
docs, labels = seperate(dictionary)
training_docs, test_docs, training_labels, test_labels = train_test_split(\
   docs, labels, stratify=labels, test_size=0.25)
categories = categories(dictionary)
tfidfed = tfidf.fit_transform(training_docs)


nb_predictions = classify_nb(test_docs, tfidfed, training_labels)
cos_predictions = classify_avg_cos(categories, test_docs, tfidfed, training_labels)
knn_predictions = classify_knn_cos(test_docs, tfidfed, training_labels)



# Running the PyOCR model:

dictionary = get_dict('/Users/matthewwong/dsi-capstone/OCR_Text/')
docs, labels = seperate(dictionary)
training_docs, test_docs, training_labels, test_labels = train_test_split(\
   docs, labels, stratify=labels, test_size=0.25)
categories = categories(dictionary)
tfidfed = tfidf.fit_transform(training_docs)


nb_predictions = classify_nb(test_docs, tfidfed, training_labels)
cos_predictions = classify_avg_cos(categories, test_docs, tfidfed, training_labels)
knn_predictions = classify_knn_cos(test_docs, tfidfed, training_labels)



# Notes on accuracy:

Just looking at kNN(5 or 7) model with PDFminer and PyOCR:
On average:
Almost always predicts Conditions and Property labels wrong.
Of PDFs labelled as Certification, Closing_Docs predicts around ~50-75% accuracy
Of PDFs labelled as Disclosures and Lock_Desk predicts around ~80-85% accuracy
Usually predicts other documents with ~90+ accuracy
