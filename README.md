================================================================================
LANCEDB REMOTE SEARCH API
================================================================================

This is a lightweight REST API server built with FastAPI that provides remote 
access to a local LanceDB vector database.

It allows external applications (such as Open Web UI) to perform semantic 
search queries against indexed documents.

--------------------------------------------------------------------------------
REQUIREMENTS
--------------------------------------------------------------------------------

1. Python 3.8+
2. A configured LanceDB database 
   (Location: data/lancedb, Table: docling)

--------------------------------------------------------------------------------
INSTALLATION
--------------------------------------------------------------------------------

1. Ensure Python is installed.
2. Install the required dependencies:

   pip install fastapi uvicorn lancedb pandas

NOTE: If using OpenAI for embeddings, ensure the OPENAI_API_KEY environment 
variable is set.

--------------------------------------------------------------------------------
USAGE
--------------------------------------------------------------------------------

The server is configured to listen on all network interfaces (0.0.0.0).

To start the server, run:

   python lancedb_server.py

Output should indicate the server is running on port 8000.

--------------------------------------------------------------------------------
API SPECIFICATION
--------------------------------------------------------------------------------

[POST] /search

Description:
Performs a semantic search in the vector database.

Request Body (JSON):
- text (string, Required): The query text to search for.
- limit (integer, Optional): Max number of results (default: 5).

Example Request (cURL):

   curl -X POST "http://localhost:8000/search" \
     -H "Content-Type: application/json" \
     -d "{\"text\": \"what is ai\", \"limit\": 3}"

Example Response (JSON):

   [
     {
       "text": "Artificial Intelligence is...",
       "metadata": {
         "filename": "lecture.pdf",
         "page_numbers": [12],
         "title": "Intro to AI"
       },
       "_distance": 0.451
     }
   ]

--------------------------------------------------------------------------------
CONFIGURATION
--------------------------------------------------------------------------------

Configuration variables are defined at the top of 'lancedb_server.py':

- Database Path: data/lancedb
- Table Name:    docling
- Port:          8000
