# Semantic Book Recommender

A web-based book recommendation system built using **LangChain** and **Gradio**. This application goes beyond simple keyword matching by using OpenAI Embeddings to perform **semantic search** on book descriptions, allowing users to find recommendations based on a descriptive query, a general category, and an emotional tone.

## Features

  * **Semantic Search:** Uses the OpenAI embedding model to find books that are contextually similar to a user's free-text query (e.g., "A story about forgiveness" or "Sci-fi thriller about time travel").
  * **Hybrid Filtering:** Allows users to filter semantic results by a general genre/category (e.g., Fiction, Nonfiction).
  * **Emotional Tone Filter:** Recommendations can be further sorted based on a predicted emotional tone of the book's description (Happy, Sad, Angry, Surprising, Suspenseful). The underlying data (`books_with_emotions.csv`) contains pre-calculated emotion scores (`joy`, `sadness`, `anger`, `surprise`, `fear`) used for this sorting.
  * **Caching for Cost/Speed:** The Chroma vector database is persisted locally (`chroma_db` folder), ensuring that embeddings are only generated once, significantly reducing API costs and application startup time on subsequent runs.
  * **Gradio Web Interface:** A simple, interactive web dashboard (`gradio_dashboard.py`) for easy use.

## Prerequisites

To run this application, you will need:

1.  **Python 3.9+** (preferably within a Conda or Virtual Environment).
2.  An **OpenAI API Key**.
3.  The required Python libraries.

### 1\. Environment Setup

It is highly recommended to use a virtual environment:

```bash
# Create and activate the virtual environment
python -m venv venv
source venv/bin/activate  # On macOS/Linux
venv\Scripts\activate     # On Windows
```

### 2\. Install Dependencies

Install the necessary libraries using the `requirements.txt` file:

```bash
pip install -r requirements.txt
```


### 3\. API Key Configuration

Create a file named **`.env`** in the root directory of the repository and add your OpenAI API key:

```ini
OPENAI_API_KEY=sk-proj-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

## How to Run

1.  Ensure you have completed the prerequisites above.

2.  Run the main application file from your terminal:

    ```bash
    python gradio_dashboard.py
    ```

3.  The application will start, and a local URL (e.g., `http://127.0.0.1:7860`) will be printed in the terminal. Open this URL in your web browser.

    *(**First Run Note:** The first time you run the script, it will take several minutes and incur API cost to generate the embeddings and save them to the `chroma_db` folder. Subsequent runs will be near-instant and free of embedding costs.)*

## Data Files

The following data files are required for the application to function:

| File Name | Description |
| :--- | :--- |
| `books_with_emotions.csv` | The master book catalog, including book metadata, categories, and pre-calculated emotion scores (joy, surprise, anger, fear, sadness) used for filtering. |
| `tagged_description.txt` | A plain text file containing book IDs and descriptions, formatted for processing into LangChain documents. |

## Application Screenshots

### Main Recommendation Dashboard

This screen shows the main search interface and the resulting gallery of recommended books after the user submits a query.

**[main\_ui.png]**

### Detailed Book Description View

This screen illustrates the detailed view that appears when a user clicks on any book from the recommendation gallery.

**[book\_description.png]**

## Code Structure

  * `gradio_dashboard.py`: Contains all the application logic, including the Chroma caching, semantic search function (`retrieve_semantic_recommendations`), data processing, and the Gradio user interface definition.
  * `chroma_db/`: Directory created on the first run, containing the persisted Chroma vector store for fast, offline similarity search.
  * `books_with_emotions.csv`: Input data for book metadata.
  * `tagged_description.txt`: Input data for generating vector embeddings.