
# Cyberpunk 2077: Building and Evaluating a RAG Chatbot

**Generative AI | Natural Language Processing | Python | Retrieval-Augmented Generation**

## Project Overview

For this DSC 670 project, I built a retrieval-augmented generation (RAG) chatbot using information from the Wikipedia article about Cyberpunk 2077.

My goal was to see whether a chatbot could retrieve relevant information from an external source and use it to generate accurate answers.

I also wanted to understand what happens when the retriever finds useful information but the language model still produces an incorrect answer.

## Project Objectives

- Retrieve and process text from Wikipedia.
- Divide the article into searchable text chunks.
- Generate semantic embeddings using Sentence Transformers.
- Retrieve relevant information based on user questions.
- Generate answers using a Hugging Face language model.
- Test different retrieval approaches and investigate incorrect answers.
- Build an interactive question-and-answer chatbot.

## Tools and Technologies

- Python
- JupyterLab
- Requests
- Beautiful Soup
- NumPy
- Sentence Transformers
- Hugging Face Transformers
- `all-MiniLM-L6-v2`
- `google/flan-t5-small`

## Data Source

The project uses the Wikipedia article for Cyberpunk 2077:

https://en.wikipedia.org/wiki/Cyberpunk_2077

I retrieved the article using Python Requests and extracted its text with Beautiful Soup.

During the original experiment, I collected 69 paragraphs containing approximately 52,775 characters.

The article was initially divided into 81 overlapping text chunks for semantic retrieval.

Because Wikipedia content changes over time, running the notebook again may produce different text and results.

## Methodology

### Retrieving the Article

I collected the Wikipedia article and extracted its paragraph text.

### Preparing the Text

I divided the article into chunks of up to 800 characters, with an overlap of 150 characters.

The overlap was intended to preserve some context between neighboring chunks.

### Semantic Retrieval

I used the `all-MiniLM-L6-v2` Sentence Transformer model to convert text into numerical embeddings.

I compared question embeddings with article embeddings to retrieve relevant passages.

### Answer Generation

I used `google/flan-t5-small` to generate answers based on the retrieved context.

The prompt instructed the model to use the supplied information rather than rely on unrelated knowledge.

### Testing and Refinement

I experimented with several versions of the RAG approach.

The original version sometimes failed even when the retrieved passages contained the answer.

During troubleshooting, I discovered that one prompt contained 657 tokens while the model's configured input limit was 512 tokens. This meant important context could be truncated.

I then tested shorter passages, focused retrieval, and sentence-level retrieval to improve the information supplied to the model.

### Interactive Chatbot

The final notebook includes an interactive chatbot that accepts questions about Cyberpunk 2077.

Users can type `quit` or `exit` to end the conversation.

## Results and Findings

The project produced mixed results.

The chatbot successfully answered some questions, including questions about Night City, Johnny Silverhand, and the actor portraying him.

However, it also generated incorrect answers for some questions, even when the retrieved information appeared relevant.

For example, earlier versions confused the game's developer and the main playable character.

The experiments showed that improving retrieval alone does not guarantee accurate answer generation.

Shorter, more focused context sometimes improved results, but the chatbot was not consistently reliable.

## Challenges and Limitations

- Relevant retrieved text did not always produce a correct answer.
- Long prompts could exceed the model's configured input limit.
- Character-based chunks sometimes separated important information.
- The smaller generation model struggled with certain factual questions.
- The project used a single Wikipedia article as its knowledge source.
- The chatbot was evaluated using a small set of questions rather than a large formal benchmark.
- Results may change as Wikipedia content or model dependencies change.

## What I Learned

This project helped me understand how retrieval and generation work together in a RAG system.

One of my biggest takeaways was that finding the correct information is only part of the problem. The language model must also interpret that information correctly.

I also learned how prompt length, text chunking, and retrieval methods can influence the quality of generated answers.

Troubleshooting the unsuccessful responses was an important part of the project because it helped me identify where the system was failing.

## Future Improvements

- Compare additional language models.
- Experiment with different chunk sizes and retrieval strategies.
- Add source citations to generated answers.
- Develop a larger question-and-answer evaluation dataset.
- Measure retrieval quality and answer accuracy separately.
- Add stronger checks for unsupported answers.

## How to Run the Project

1. Download or clone this repository.
2. Install Python and JupyterLab.
3. Open the uploaded `.ipynb` notebook in JupyterLab.
4. Run the installation cells and then execute the notebook in order.
5. Allow time for Wikipedia retrieval and model downloads.
6. When you reach the interactive chatbot, enter questions about Cyberpunk 2077.
7. Type `quit` to exit the chatbot.

The project requires an internet connection to retrieve Wikipedia content and download Hugging Face models.

The interactive chatbot waits for user input, so it is not designed to run completely unattended.

## Author

**Kevin Feracho**

Master of Science in Data Science  
Bellevue University

[GitHub Profile](https://github.com/kevinf529-cool) | [Data Science Portfolio](https://kevinf529-cool.github.io/)
