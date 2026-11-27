# Day 5 – PDF Question Answering with OCR and RAG

Upload a PDF in Google Colab and ask questions about its contents. The notebook extracts text from the document, uses OCR for pages without selectable text, and searches for relevant passages before asking a Groq model to answer. This workflow is called **retrieval-augmented generation (RAG)**.

**Notebook:** [DAY-5.ipynb](./DAY-5.ipynb)

## How it works

1. **Extract text.** PyMuPDF first tries to read the text layer on each page. If it finds no text, it renders the page as an image and uses Tesseract for English OCR.
2. **Split the text.** The extracted text is divided into 500-character chunks with 100 characters of overlap.
3. **Create a search index.** Sentence Transformers converts the chunks into normalized embeddings using `all-MiniLM-L6-v2`. FAISS stores the vectors in memory and ranks them by similarity to the question.
4. **Generate an answer.** The notebook sends up to three matching chunks and the question to Groq's `openai/gpt-oss-20b` model. The prompt asks the model to answer from those chunks and say when the answer is unavailable.

An introductory cell also compares the embedding shapes of `all-MiniLM-L6-v2` and `all-mpnet-base-v2`. The PDF search uses MiniLM.

## Run in Google Colab

1. Open `DAY-5.ipynb` in Colab. Run the installation cell immediately below the embedding comparison **before** running the comparison, so `sentence-transformers` is installed.
2. Run the PDF upload and extraction cell. It installs the OCR dependencies, then prompts you to select one PDF. Check the extracted text preview before continuing.
3. Run the chunking and FAISS indexing cells. If Colab reports that no text was extracted, try a clearer PDF before building the index.
4. Run the Groq setup cell and enter your Groq API key at the hidden prompt.
5. Run the interactive cell. Enter a question, press **Enter**, and type `exit` when you're done.

The core workflow uses PyMuPDF, Pillow, pytesseract, Tesseract OCR, Sentence Transformers, NumPy, FAISS, and the Groq Python SDK. The separate Poppler/EasyOCR installation cell can be skipped for this workflow.

## Example questions

For a sample train-ticket PDF, try:

- What is the journey date?
- What are the boarding and destination stations?
- What class is listed on the ticket?

In the saved run, the notebook used OCR on page 1 and extracted **959 characters**. The displayed preview contains the first **500 characters** of that text.

## Limitations and data handling

OCR can misread names, numbers, and dates, especially on low-quality scans. Check important details against the original PDF. Answers depend on the passages retrieved, so a detail elsewhere in the document can be missed.

Retrieved passages and questions are sent to Groq. Use a sample or redacted PDF for a public demo, and clear notebook outputs containing ticket identifiers or passenger details before publishing.
