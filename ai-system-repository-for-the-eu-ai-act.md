---
slug: /AI-agent-repository
hide_title: true
title: AI System Repository for the EU AI Act
---

# AI System Repository for the EU AI Act

## Introduction

The EU AI Act requires organizations to maintain an inventory of AI systems, understand where they are used, assess their risk, and demonstrate appropriate governance throughout their lifecycle.

Many organizations already operate numerous AI systems across different applications, cloud platforms, and departments. Without a structured architectural inventory, it becomes difficult to identify AI systems, understand their business context, assess regulatory obligations, or demonstrate compliance during audits.

This pattern describes a pragmatic approach to modelling AI systems such as AI agents, chatbots, and MCP tools in ADOIT using ArchiMate. The pattern is aligned with the [ADOIT Lean Profile](https://docs.boc-group.com/adoit/en/docs/user_manual/mmconf-000000/#mmconf-220000) for Enterprise Architecture. It focuses on building an AI inventory that supports governance, risk assessment, and compliance with the EU AI Act while remaining suitable for Enterprise Architecture analysis and planning.

## Design Principle

- **Model AI Systems in Their Enterprise Context**

    An AI system should never be documented as an isolated technical component.

  - Effective AI governance requires understanding:

    - where an AI system is provided,
    - which business processes it supports,
    - which business data it processes,
    - which organizational responsibilities are associated with it,
    - which AI model powers it,
    - which governance controls apply,
    - and how it was discovered and inventoried.

  The AI repository therefore combines business, application, information, technology, and governance perspectives into one consistent architecture model.

## Modelling Structure

- **AI Systems as Application Services**

    Each AI system is modelled as an **Application Service** using the specialization **&lt; AI system &gt;**.

    **The AI system is modelled as an Application Service because it represents an AI service rather than the application hosting it**.

    It serves as the central element of the AI inventory.

  - Typical examples include:

    - Customer Support agents
    - Code Generation agents
    - Procurement copilots
    - MCP servers

- **Providing Applications**

    While usually embedded within an existing Application Component, an AI system can also be realized as a standalone infrastructure element.

    The Application Component represents the software product or application in which the AI functionality is implemented. It provides architectural context, ownership, lifecycle management, and integration into the application portfolio.

    ![Icon](./media/006.jpg "Icon") **Application Component → Realization → Application Service &lt; AI system &gt;**

    This answers:

    Which application provides this AI system?

- **Business Context**

    AI systems support one or more Business Processes.

    This establishes the business context required for governance and enables organizations to identify AI systems used in regulated or potentially high-risk business activities.

    ![Icon](./media/006.jpg "Icon") **Application Service &lt; AI system &gt; → Serving → Business Process**

    This answers:

    Which business process is supported by this AI system?

- **Business Responsibilities**

    AI systems also serve one or more **Business Roles** that interact with or are responsible for their operation and governance.

  - Within the context of the EU AI Act, organizations typically distinguish three key responsibilities:

    - **Owner** - accountable for the business use, lifecycle, and governance of the AI system within the organization.
    - **Provider** - responsible for developing or placing the AI system on the market. This may be an internal development team or an external software vendor.
    - **Deployer** - responsible for operating or using the AI system within its intended business context.

  These responsibilities are modelled as **Business Roles**, allowing them to be reused across multiple AI systems and assigned to the appropriate organizational actors.

  ![Icon](./media/006.jpg "Icon") **Application Service &lt; AI system &gt; → Serving → Business Role**

  This answers:

  Which organizational responsibilities are associated with this AI system?

- **Data Usage**

  - The business data processed by an AI system is modelled using **Business Objects**.

  - Typical examples include:

    - Employee
    - Customer
    - Product
    - Order
    - Invoice
    - Contract
    - Supplier
    - Asset

  - Business Objects represent business-relevant information concepts rather than technical implementation details such as prompts, embeddings, vector stores, or payload formats.

    ![Icon](./media/006.jpg "Icon") **Application Service &lt; AI system &gt; → Access → Business Object**

  - This supports:

    - transparency of which business data is processed by AI systems,
    - data governance and ownership,
    - impact analysis,
    - documentation required by the EU AI Act.

- **AI Model**

  - The AI model powering an AI system is modelled as **System Software**.

  - Typical examples include:

    - GPT-5
    - Claude Sonnet
    - Gemini
    - Llama
    - Mistral Large
    - Phi-4
    - Custom Foundation Model

  - The AI model represents the software component that provides the intelligence behind the AI system.

    ![Icon](./media/006.jpg "Icon") **System Software → Serving → Application Service &lt; AI system &gt;**

    This documents which Foundation Model or LLM powers the AI system and supports impact analysis when models are upgraded, replaced, or retired.

- **Discovered Artifacts**

    Organizations often discover potential AI systems or their components/configurations automatically from enterprise platforms such as Microsoft Entra, Azure AI Foundry, ServiceNow, GitHub, or other AI management solutions.

    These technical findings are modelled as **Discovered Artifacts**. They provide evidence that an AI system exists and support the continuous synchronization between automated discovery sources and the architecture repository.

    Discovered Artifacts are used to identify, validate, or create AI systems within the repository while maintaining human oversight over the inventory.

    ![Icon](./media/006.jpg "Icon") **Discovered Artifact → Realization → Application Service &lt; AI system &gt;**

  - This supports:

    - automated AI discovery,
    - continuous inventory synchronization,
    - validation of documented AI systems,
    - identification of undocumented AI systems.

- **AI Governance Controls**

    AI governance controls are modelled as **Constraints**.

    Constraints capture mandatory governance, compliance, security, or organizational rules that apply to an AI system. They represent obligations arising from the EU AI Act, internal governance policies, or other regulatory frameworks.

  - Typical examples include:

    - Human oversight required
    - Transparency obligations
    - Logging and monitoring required
    - Data quality controls
    - Bias monitoring
    - Human review before deployment
    - Periodic compliance review

  ![Icon](./media/006.jpg "Icon") **Constraint → Association → Application Service &lt; AI system &gt;**

### The pattern

![Architecture Diagram](./media/001.jpg "Architecture Diagram")

### Do / Don't - AI System Modelling

- ![Icon](./media/002.jpg "Icon") **Do**

  - Model every AI system explicitly as an Application Service.
  - Connect every AI system to the Application Component that provides it.
  - Link AI systems to the Business Processes they support.
  - Document the relevant Business Roles (such as Owner, Provider, and Deployer) associated with each AI system.
  - Document the business data processed by AI systems using Business Objects.
  - Model the Foundation Model / LLM separately from the AI system.
  - Integrate automated discovery by linking Discovered Artifacts to AI systems.
  - Record AI governance controls using Constraints.
  - Use the architecture repository as the authoritative AI inventory.
  - Model prompts, embeddings, or implementation details as Artifacts.

- ![Icon](./media/003.jpg "Icon") **Don't**

  - Don't model AI systems as Application Components.
  - Don't model Foundation Models as AI systems.
  - Don't document AI systems without business context or organizational responsibilities.
  - Don't maintain separate spreadsheets for AI inventories.
  - Don't ignore automatically discovered AI-related artifacts.

## Scope and Intent

- This pattern supports:

  - AI inventories required by the EU AI Act
  - AI governance and ownership
  - AI risk classification
  - governance and compliance workflows
  - transparency of AI usage across the enterprise
  - architecture impact analysis
  - enterprise-wide AI governance

- It is **not** intended to:

  - replace AI model registries or MLOps platforms,
  - describe deployment or runtime architecture,
  - replace detailed technical AI documentation.
