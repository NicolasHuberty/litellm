# Qdrant review evidence

Screenshots for https://github.com/BerriAI/litellm/pull/46426, captured on October 14, 2026 with Playwright and Chrome from the actual dashboard

The before dashboard runs commit aa0279e0a23a4e983141e6df1556df9926a4f3ce. The after dashboard and proxy run commit b1ead988b9631d060067e15a7370d19e14f3432c. Both dashboards use the same local proxy and test data. Red boxes are annotations highlighting the provider list, configuration fields, and retrieved text

The local proxy uses a dedicated PostgreSQL database, Qdrant v1.19.0, and Ollama nomic-embed-text:v1.5. No network requests or provider responses are mocked. The query-embeddings alias is configured with model_info.mode set to embedding

Open /ui/vector-stores on the dashboard. Select Manage Vector Stores, Add Vector Store, and open Provider. Qdrant is absent before the change and present after it

Select Qdrant. Set Vector Store ID to litellm_qa_documents, API Base to http://127.0.0.1:16333, Embedding Model to query-embeddings, Text Field to text, Vector Name to dense, and Vector Store Name to qdrant-qa. Leave API Key blank for this local unauthenticated Qdrant instance. Click Create. The real POST /vector_store/new returns HTTP 200. The collection is registered through the dashboard rather than through vector_store_registry in the proxy YAML

Select Test Vector Store and qdrant-qa. Search for What is the capital of Belgium? Expand Result 1. The real POST /v1/vector_stores/litellm_qa_documents/search returns HTTP 200, Brussels is the capital of Belgium., score 0.90624547, file ID 2, and the stored metadata

The qdrant directory contains the screenshots and the actual successful registration and search response bodies. This branch holds review artifacts separately from the feature branch, so adding evidence does not change the PR tip or rerun its checks
