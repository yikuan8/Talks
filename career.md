```mermaid
flowchart TD
    A[Input Clinical Text Span] --> B[Step 1: Candidate Generation via MetaMap]
    B --> C{Step 2: LLM Judge Classifier}
    C -->|YES| D[Accept MetaMap CUI]
    C -->|NO| E[Light Refiner]
    C -->|PROBLEMATIC| F[Deep Refinement Path]

    subgraph Refinement_Agents
        F --> G[Abbreviation Agent]
        G --> H[Negation and Context Agent]
        H --> I{Retriever}
        I --> J[UMLS API]
        I --> K[Vector Database]
        J --> L[Merge and Re-rank]
        K --> L
        L --> M[Refiner Agent]
    end

    M --> N{Decision}
    N -->|Final CUI| O[Redundancy Resolution]
    N -->|Abstain| O
    D --> O
    E --> O
    O --> P[Auditing and Provenance]
    P --> Q[Output Final Mappings]

```
