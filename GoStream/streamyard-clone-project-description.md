# Project: BuildStream - A StreamYard Clone

## Overview
BuildStream is a web-based live streaming studio that allows users to create professional live streams, interviews, and shows. This project aims to replicate the core functionality of StreamYard using a microservices architecture, with a focus on scalability, real-time performance, and concurrent processing.

## Tech Stack
- Frontend: React
- Backend: Go
- Message Broker: RabbitMQ
- Search Engine: Elasticsearch
- Databases: MySQL (primary data store) and Redis (caching)

## Key Features
1. User authentication and authorization
2. Studio creation and management
3. Real-time video/audio streaming
4. Chat functionality
5. Screen sharing
6. Custom branding and overlays
7. Multi-platform streaming (YouTube, Facebook, Twitch, etc.)
8. Analytics and reporting

## Microservices Architecture
The application should be divided into the following microservices:

1. User Service
2. Studio Service
3. Streaming Service
4. Chat Service
5. Analytics Service
6. Notification Service

## Requirements

### 1. User Service
- Implement user registration, login, and profile management
- Use MySQL for storing user data
- Implement JWT-based authentication

### 2. Studio Service
- Manage studio creation, configuration, and deletion
- Store studio settings in MySQL
- Use Elasticsearch for quick studio search and filtering

### 3. Streaming Service
- Handle real-time video/audio streaming using WebRTC
- Implement screen sharing functionality
- Manage multi-platform streaming integrations
- Use Go's concurrency features to handle multiple simultaneous streams

### 4. Chat Service
- Implement real-time chat functionality using WebSockets
- Store chat messages in Redis for quick retrieval
- Use RabbitMQ for managing chat message queues

### 5. Analytics Service
- Track and store user engagement metrics
- Generate real-time and historical reports
- Use MySQL for storing analytics data
- Implement concurrent processing of analytics events

### 6. Notification Service
- Handle in-app and email notifications
- Use RabbitMQ for managing notification queues

## Additional Requirements
1. Implement service discovery and load balancing
2. Use Docker for containerization of microservices
3. Implement API Gateway for routing requests to appropriate microservices
4. Ensure fault tolerance and implement circuit breakers
5. Implement distributed logging and monitoring
6. Write unit and integration tests for each microservice
7. Document the API for each microservice using Swagger/OpenAPI

## Bonus Points
- Implement CI/CD pipeline
- Add support for custom RTMP ingest
- Implement a recommendation system for content discovery

## Evaluation Criteria
1. Code quality and organization
2. Proper use of Go's concurrency features
3. Effective implementation of microservices architecture
4. Scalability and performance of the system
5. Proper use of specified technologies (RabbitMQ, Elasticsearch, MySQL, Redis)
6. Security considerations
7. Documentation and test coverage

Please provide a high-level system design, implementation plan, and a working prototype of at least two interconnected microservices to demonstrate your approach to this project.
