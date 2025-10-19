# Real-time Social Media Trend Tracking (NLP + Graph)

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue)](https://www.python.org/)
[![Kafka](https://img.shields.io/badge/Kafka-Streaming-black)](https://kafka.apache.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-API-green)](https://fastapi.tiangolo.com/)
[![Neo4j](https://img.shields.io/badge/Neo4j-GraphDB-teal)](https://neo4j.com/)
[![Docker](https://img.shields.io/badge/Docker-Ready-informational)](https://www.docker.com/)

End-to-end pipeline to detect emerging topics and influencers across social platforms using streaming NLP and graph analytics.

## Overview
- Ingestion: Streaming tweets/posts via APIs -> Kafka topics
- NLP: language detection, cleaning, embeddings (MiniLM), topic modeling (BERTopic), NER/hashtags
- Graph: build interaction graph (users, hashtags, entities); centrality, community detection (Louvain)
- Trends: burst detection, velocity/acceleration metrics; anomaly flags
- Serving: FastAPI for queries, WebSocket for live updates; dashboard-ready JSON

## Business Context
- Detect viral trends early for marketing and risk intelligence
- Identify key influencers and narratives; track campaign lift
- KPIs: topic purity > 0.8, detection lead time < 10 min

## Tech Stack
- Stream: Kafka, Faust/ksqlDB, Redis cache
- NLP: Transformers, sentence-transformers, BERTopic, spaCy
- Graph: NetworkX, Neo4j optional
- Serving: FastAPI, Uvicorn, Docker, Grafana panels

## Repository Structure
```
realtime-trends/
  ingestion/
    kafka_producer.py
    sources/
      twitter.py
  nlp/
    preprocess.py
    embed.py
    topics.py
  graph/
    build_graph.py
    metrics.py
  api/
    main.py
    ws.py
  configs/
  dashboards/
  docker/
```

## Sample Results (synthetic)
- Top-5 topics coherence: 0.62 (c_npmi)
- Influencer precision@20: 0.75
- Average end-to-end latency: 4.2s

## Installation
```
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
```

## Usage
Run API:
```
uvicorn api.main:app --host 0.0.0.0 --port 8080
```
Start stream (simulated):
```
python -m ingestion.kafka_producer --source sample
```

## Roadmap
- Cross-lingual topic alignment
- Bot detection heuristics and ML
- Sentiment flow and stance detection per community
