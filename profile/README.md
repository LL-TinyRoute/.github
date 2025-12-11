# TinyRoute 🤓 

URL Shortener Backend — Requirements Specification

## Overview

This document describes the backend requirements for a serverless URL shortening service backed by a SQL database. The backend must generate short links, store and retrieve metadata, track click analytics, and expose APIs for integration with frontends or external clients, it does not require a frontend development for now.

## The service must:

* Generate a unique, collision-resistant short ID (6–10 characters)
* Support alphanumeric IDs (base62 recommended)
* Guarantee uniqueness (enforced through primary key constraint)
* Be able to expire and/or disable the short URL
* Track Metrics
* Scale up if it needs it

## Architecture Requirements
### Serverless Environment

The system must run using serverless compute (e.g., AWS Lambda, Azure Functions, or GCP Cloud Functions), with the following properties:

Auto-scaling based on traffic
Minimal idle cost
Stateless execution; all persistent data stored in SQL
Functions isolated per responsibility (e.g., create short URL, resolve short URL, record analytics)


### SQL Database

Use a SQL relational database (e.g., PostgreSQL, MySQL, SQL Server). Requirements:
* Strong consistency
* Support for transactions
* Good indexing capabilities

Able to handle bursts of read/write traffic

* Core Features
* Generate Short IDs

### Short ID strategies:

* Random base62 generator
* Hash-based generator with collision fallback

## Aggregated Analytics

The system should allow queries for:

* Total clicks per short URL
* Unique visitors count
* Top countries
* Browser breakdown
* Device type distribution
* Daily/weekly/monthly click history

## Security Requirements

* Input validation for all URLs
* Rate limiting on creation API

Bot detection best-effort for analytics

Use HTTPS everywhere

## Logging & Observability

* Log every creation event
* Log redirect errors (invalid or expired IDs)
* Log analytics processing failures
* Expose metrics:
* Redirect latency
* Failed redirects

## Extra Challenges

* Cache layer
* Use event queue
* Bot detection strategy

