# Lineblocs

[![Build Status](https://img.shields.io/badge/build-passing-brightgreen)]()
[![License](https://img.shields.io/badge/license-MIT-blue)]()

Lineblocs is a modular, open communications platform designed for telecom operators, UCaaS providers, and enterprises who want to build white-label Voice, WebRTC, and messaging services. It separates business logic from real-time voice infrastructure while offering developer-centric APIs, SDKs, and deployment flexibility.

---

## Architecture Overview

Lineblocs is split into two core Helm charts:

- **Web Helm Chart**: handles user-facing portals, admin dashboard, APIs, business logic  
- **VoIP Helm Chart**: handles SIP signaling, media servers, call control, and billing  

They share a **central database** and communicate via APIs for user operations and real-time communication logic.  
This separation allows the Web stack and VoIP stack to scale independently while remaining tightly integrated.

### Architecture Diagram

```mermaid
graph LR
	subgraph Web Helm
		A[User Portal & Flow Editor]
		B[Admin Dashboard]
		C[User API]
		D[Internals API]
		DB[(Shared Database)]
	end

	subgraph VoIP Helm
		E[OpenSIPS Proxy]
		F[Asterisk Backend]
		G[Asterisk Media Server]
		H[RTP Proxy Pool]
		I[VoIP Workers]
	end

	A --> C
	B --> C
	C --> D
	D --> E
	D --> F
	E --> G
	F --> G
	G --> H
	I --> DB
	C --> DB
	D --> DB
```