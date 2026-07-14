AI Document Search System (MERN + AI + Cloud)

An AI-powered document search system that allows users to upload documents, extract text, generate embeddings, and perform both keyword-based and meaning-based (semantic) search.

The application follows modern Retrieval-Augmented Search concepts used in knowledge systems and document management platforms.

Table of Contents

Overview

Features

Architecture Summary

Tech Stack

AI Model Used

Core Concepts

System Flow Summary

API Endpoints

Environment Variables

Deployment (Render + Cloudinary)

Token Efficiency Strategy

Limitations

Future Enhancements

Notes

1. Overview

The application supports:

Uploading PDF and DOCX files

Automatic text extraction

Generating AI embeddings

Storing searchable content in MongoDB

Keyword search

AI semantic search

Secure cloud-based file storage

Manage, list, and delete uploaded documents

It is designed to be scalable, predictable in cost, and easy to extend.

2. Features
Keyword Search

Search documents by text match in title and content.

AI Semantic Search

Retrieve documents based on meaning, even if wording differs.

Document Upload

Supports:

PDF

DOCX

Automatically extracts text and embeds content.

Cloud Storage

Documents are stored securely using Cloudinary instead of local storage.

Document Management

View all documents

Delete stored documents

3. Architecture Summary

High-level layers:

React frontend

Node.js + Express backend

MongoDB database

Cloudinary file storage

OpenRouter AI embeddings

Deployment on Render

4. Tech Stack
Frontend

React

Fetch API / Axios

CSS

React Toastify

Backend

Node.js

Express

Multer

pdf-parse

mammoth

Axios

Database

MongoDB

Mongoose

AI / Embeddings

OpenRouter

Model: openai/text-embedding-3-small

Cloud

Render (hosting)

Cloudinary (file storage)

5. AI Model Used

Embedding Provider: OpenRouter
Model: openai/text-embedding-3-small

Used to convert:

document text into vectors

user queries into vectors

Supports accurate similarity search and is optimized for search workloads.

6. Core Concepts
Embeddings

Vector representation capturing text meaning.

Cosine Similarity

Used to measure similarity between query embeddings and document embeddings.

Higher score = more similar.

7. System Flow Summary
Upload

User uploads PDF/DOCX

Text extracted

Embedding generated

File uploaded to Cloudinary

Stored in MongoDB

Search

User enters query

Query embedded

Compared to stored vectors

Best-matching documents returned

8. API Endpoints
Upload File

POST /api/documents/upload

Form-Data:

file

Add Manual Document

POST /api/documents/add

{
  "title": "Example",
  "content": "Some text here"
}

Keyword Search

GET /api/documents/search?q=keyword

AI Search

GET /api/documents/ai-search?q=query

Get All

GET /api/documents/all

Delete

DELETE /api/documents/:id

9. Environment Variables
Backend
MONGO_URI=
OPENROUTER_KEY=

CLOUD_NAME=
CLOUD_API_KEY=
CLOUD_API_SECRET=

PORT=5000

Frontend
REACT_API_BASE=https://ai-dock-search.onrender.com/api/documents


Do not commit environment variables to GitHub.

10. Deployment (Render + Cloudinary)
Backend (Render Web Service)

Root directory: backend

Install: npm install

Start: node server.js

Add all backend environment variables

Frontend (Render Static Site)

Root directory: frontend

Build: npm install && npm run build

Publish directory: build

Add:

REACT_API_BASE=https://ai-dock-search.onrender.com/api/documents

Cloudinary

Enable PDF delivery

Use resource_type: raw

Store secure_url in database

11. Token Efficiency Strategy

Document embedded only once

Stored embeddings reused

Only user query generates new embedding

Similarity computed in backend, not AI

This keeps costs predictable and low.

12. Limitations

Long documents may need chunking

Requires internet for embeddings

Larger files increase processing time

Single embedding per document reduces accuracy in very large texts

13. Future Enhancements

Paragraph-level embeddings

Authentication and roles

Vector database integration

AI-generated summaries

Filters, search history, pagination

14. Notes

This project demonstrates a production-ready AI semantic search pipeline:

modern web development

cloud deployment

secure storage

efficient AI usage

It serves as a starting point for enterprise document search systems.
