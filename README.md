AI-Powered Incident Management Platform
Overview
This project implements an AI-powered incident management platform using event-driven microservices architecture.
The system automatically:
	• Classifies IT incidents
	• Assigns priority and SLA
	• Retrieves knowledge base solutions
	• Generates resolution steps using AI
The platform uses Kafka-based asynchronous processing to ensure scalability and resilience.

Architecture
Microservices communicate using Apache Kafka events.
Client → API Gateway → Incident Service → Kafka → AI Service → Kafka → Incident Service → MySQL

Components:
Service	Responsibility
API Gateway	Entry point for client requests
Incident Service	Ticket management and persistence
AI Service	AI classification, knowledge retrieval, resolution generation
Kafka	Event-driven communication
MySQL	Ticket storage

Key Features
Event-Driven Microservices
Ticket processing is asynchronous:
Ticket Created → Kafka Event → AI Processing → Ticket Updated


AI Incident Classification
AI classifies incidents using LangChain4j + OpenAI:
Example:
Input:
VPN not connecting
Output:
category: Network
priority: P2
impactedSystem: VPN

Knowledge Base Retrieval
Uses vector embeddings and cosine similarity to find relevant solutions.

AI Resolution Agent
Generates resolution instructions automatically.
Example output:
1. Verify VPN client installation
2. Check corporate credentials
3. Reset VPN profile

Resilience Patterns
The system implements:
	• Circuit Breaker (Resilience4j)
	• Retry mechanism
	• Dead Letter Queue
	• Fallback AI classification
	• Distributed correlation IDs

Containerized Deployment
Entire system runs using Docker Compose.
Services:
api-gateway
incident-service
ai-service
kafka
zookeeper
mysql
Start system:
docker compose up --build

API Endpoints
Create ticket
POST /tickets
Example:
{
  "description": "Unable to reset password"
}
Check ticket status
GET /tickets/{id}

Tech Stack
Backend
	• Java 17
	• Spring Boot
	• Spring Cloud Gateway
	• Spring Kafka
	• Spring Data JPA
AI
	• LangChain4j
	• OpenAI API
Infrastructure
	• Apache Kafka
	• Docker
	• MySQL
Resilience
	• Resilience4j
	• Retry
	• Circuit Breaker
	• DLQ
