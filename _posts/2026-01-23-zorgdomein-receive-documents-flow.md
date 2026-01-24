---
title: "Zorgdomein Receive Documents Flow Explained: Secure Certificate-Based .NET Architecture"
date: 2026-01-24
image: /assets/images/Zorgdomain-FHIR-Integration.png
header:
  teaser: 
  thumbnail: /assets/images/Zorgdomain-FHIR-Integration.png
  og_image: /assets/images/Zorgdomain-FHIR-Integration.png
categories: 
    - Healthcare
tags: 
    - FHIR
    - IIS
    - Certificate Authentication
    - Zorgdomein
excerpt: "Zorgdomein Receive Documents is a certificate-based server-to-server flow where healthcare systems securely receive and acknowledge clinical documents. This article explains the trust model, certificate validation, and receive-confirm architecture in .NET."
redirect_from:
  - /healthcare/bidirectional-patient-data-exchange-with-zorgdomein/
---

![image](/assets/images/Zorgdomain-FHIR-Integration.png)
## TL;DR
The Zorgdomein Receive Documents flow is a certificate-secured, server-to-server integration where your system acts as a trusted document endpoint. A correct implementation depends on strict certificate validation, a clearly defined receive–validate–process–confirm sequence, and disciplined separation of responsibilities. This article explains how to architect that flow in .NET from a practical, implementation-focused perspective.

## What Is the Zorgdomein Receive Documents Flow?

The Zorgdomein Receive Documents flow is a secure inbound integration pattern in which Zorgdomein delivers clinical documents directly to an external system that has been pre-approved through certificate exchange.

In this flow, the receiving system must authenticate Zorgdomein using client certificates, validate the incoming message, process the document according to internal rules, and return a protocol-level confirmation. The correctness of this sequence not business logic determines whether the integration behaves reliably in production.

## Introduction

Zorgdomein integrations often fail not because of document parsing or data models, but because trust is implemented incorrectly. Before a single document can be processed, the receiving system must be able to prove cryptographically that the request originates from Zorgdomein.

The Receive Documents flow is therefore not just an API endpoint. It is a trust boundary. Zorgdomein initiates the connection, presents its client certificate, and expects the receiving system to validate that identity before allowing the request to enter the application layer.

This article focuses exclusively on the Receive Documents flow and explains how to design certificate exchange, certificate validation, and the internal receive–validate–confirm lifecycle in a .NET-based system.

## Role of the Receiving System in the Receive Documents Flow

In this integration, your SaaS platform acts as the **document endpoint**. Zorgdomein pushes documents to you; you do not poll or fetch them.

Your system is responsible for:

- Accepting inbound HTTPS requests initiated by Zorgdomein  
- Verifying Zorgdomein’s identity using certificates  
- Parsing and validating the incoming message  
- Processing the validated document  
- Returning a confirmation response  

These responsibilities must be explicitly separated at the architectural level. Treating this flow as a single request handler increases coupling and makes failures harder to reason about.

## Certificate Exchange: Establishing Trust Before Runtime

Trust between your system and Zorgdomein is established **before** any documents are exchanged.

This certificate exchange process typically involves:

- Agreement on the client certificate Zorgdomein will present  
- Configuration of trusted root or intermediate certificate authorities  
- Server-side configuration to require and validate client certificates  

The architectural takeaway is simple: certificate exchange is an onboarding activity, but certificate **enforcement** is a runtime responsibility. Your system must reject any request that does not satisfy the agreed trust conditions.

## How the Receiving System Verifies Zorgdomein Using Certificates

When Zorgdomein sends a document, identity verification happens at the transport layer using mutual TLS.

Before the request reaches application logic, the system must ensure:

- A client certificate is present  
- The certificate chains to a trusted authority  
- The certificate is valid and not expired  
- The certificate identity matches the agreed Zorgdomein identity  

Only after these checks pass should the request be forwarded to the application pipeline. Once this boundary is crossed, application code can safely assume that the sender is Zorgdomein.

This is a critical architectural principle: **identity validation must happen before parsing, validation, or processing**.

## End-to-End Receive Documents Architecture

The following sequence shows the complete Receive Documents flow, starting from certificate validation and ending with confirmation back to Zorgdomein.

![image](/assets/images/zorgdomein-receive-document-flow-the-good-engineers.png)

This diagram reflects the core principle of the flow: certificate validation gates everything. If trust fails, the request never becomes an application concern.

## Receiving and Logging the Incoming Request

Once the TLS layer has validated Zorgdomein’s certificate, the request enters the system as a trusted call.

At this stage, the system should:
- Log receipt of the request
- Capture correlation identifiers
- Record minimal metadata needed for traceability

No parsing or business logic should occur here. This boundary-level logging ensures that every inbound document is traceable, even if later validation fails.

## Parsing and Validating the Incoming Message

After receipt, the incoming message is parsed into the expected structural model. Parsing answers only one question: is the message structurally readable?

Validation follows parsing and confirms that the message is semantically acceptable for processing. This may include:
- Required fields present
- Internal consistency checks
- Conformance to expected document structure

Validation acts as a gate. Messages either pass and continue or fail and stop. Mixing validation with processing makes error handling ambiguous and increases coupling.

## Processing the Validated Document

Only validated messages proceed to processing. This stage is intentionally application-specific and may involve:
- Transforming the document into internal domain structures
- Triggering downstream workflows
- Persisting data for later use

From an architectural standpoint, processing should be decoupled from the receive endpoint. The endpoint’s responsibility is to accept and acknowledge documents, not to embed deep domain logic.

This separation is especially important in large systems implementing [Zorgdomein integration in .NET Core for enteprise healthcare apps](/), where internal workflows evolve independently of external integration contracts.

## Responding With Confirmation

The final responsibility of the Receive Documents flow is returning a confirmation response to Zorgdomein.

This confirmation indicates that:
- The request was received
- The sender was authenticated
- The message was accepted according to protocol expectations

It does not represent downstream business success. Retry handling and delivery guarantees are owned by Zorgdomein in this flow, not by the receiving system.

## Common Architectural Mistakes to Avoid

Several recurring mistakes weaken Receive Documents implementations:
- Allowing requests to reach application code before certificate validation
- Combining receive, validate, and process into a single step
- Delaying confirmation until deep business logic completes
- Treating confirmation as proof of successful internal processing

These issues are architectural, not technical, and are best addressed through clear responsibility boundaries.

## Conclusion

The Zorgdomein Receive Documents flow is fundamentally about trust, not transport. Certificates are not an implementation detail; they are the contract that defines who is allowed to send documents into your system.

For CTOs and engineering managers, the key takeaway is clear: design the system so that identity is proven early and unequivocally, and structure the receive flow around explicit stages: receive, validate, process, confirm.

When certificate validation gates the flow and responsibilities are clearly separated, the integration becomes predictable, maintainable, and resilient under real operational conditions.

