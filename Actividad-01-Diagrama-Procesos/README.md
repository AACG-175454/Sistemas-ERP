# Actividad 01 - Diagrama de Procesos

Diagrama de procesos realizado con Mermaid para la materia Sistemas ERP.

## Diagrama

```mermaid
flowchart LR

subgraph CRM["CRM / SRM"]
    direction TB

    ACT["Activities"]
    CUST["Customer"]
    LEAD["Lead"]
    SUPP["Supplier"]
    BPM["Business Partner Master"]

    ACT --> CUST --> LEAD --> SUPP --> BPM
end

subgraph CORE["Business Processes"]
    direction TB

    subgraph SERVICE["Service"]
        direction LR
        CEC["Equipment Card"] --> SC["Service Call"] --> SCON["Service Contract"] --> SB["Billing"]
    end

    subgraph SALES["Sales"]
        direction LR
        OPP["Opportunity"] --> PRIC["Pricing"] --> SQ["Quotation"] --> SO["Sales Order"] --> DN["Delivery"] --> ARI["AR Invoice"] --> INP["Incoming Payment"]
    end

    subgraph PURCHASING["Purchasing"]
        direction LR
        PR["Purchase Request"] --> PQ["Quotation"] --> PO["Purchase Order"] --> GRPO["Goods Receipt"] --> API["AP Invoice"] --> OUTP["Outgoing Payment"]
    end

    subgraph PRODUCTION["Production"]
        direction LR
        BOM["BOM"] --> MRP["MRP"] --> SRC["Sourcing"] --> PRO["Production Order"] --> ITP["Issue"] --> RFP["Receipt"]
    end

    subgraph INVENTORY["Inventory"]
        direction LR
        IM["Item Master"] --> WM["Warehouse"] --> DP["Demand Planning"]
    end

    subgraph FINANCE["Finance"]
        direction LR
        COA["Chart of Accounts"] --> GLA["G/L Accounts"] --> GLAD["Account Determination"] --> CA["Cost Accounting"] --> JE["Journal Entries"] --> APAR["AP / AR"] --> CM["Cash Management"] --> REC["Reconciliation"]
    end
end

subgraph REPORTING["Reporting"]
    direction TB

    BR["Backorders"]
    IAR["Inventory Audit"]
    ABR["Account Balances"]
    FR["Financial Reports"]
    PRR["Product Reports"]
end

CUST -.->|customer equipment| CEC
CUST -->|creates| OPP
LEAD -.->|sales lead| OPP
SUPP -->|purchase request| PR
SUPP -.->|sourcing| SRC

IM -->|items| SO
IM -->|items| PO
IM -->|materials| PRO
WM -.->|availability| SO
DP -->|demand| PO

SO ---|sales / purchasing| PO
PO ---|supply| PRO
DN ---|goods movement| GRPO
GRPO ---|material available| ITP
ARI ---|billing link| API
API ---|production cost| RFP
INP ---|cash flow| OUTP

SB -.->|posting| JE
ARI -.->|receivable| JE
API -.->|payable| JE
RFP -.->|production cost| JE
INP -.->|cash in| CM
OUTP -.->|cash out| CM

SO -.->|backorders| BR
JE -.->|inventory audit| IAR
JE -.->|balances| ABR
REC -->|financial results| FR
RFP -->|product data| PRR

classDef crm fill:#EAF7EC,stroke:#2E9B50,stroke-width:2px,color:#174D29
classDef service fill:#FFFCE3,stroke:#D6B600,stroke-width:2px,color:#665800
classDef sales fill:#FFF1E1,stroke:#F28C28,stroke-width:2px,color:#7A4300
classDef purchasing fill:#E8F5FF,stroke:#168AC1,stroke-width:2px,color:#07547A
classDef production fill:#F3E9FA,stroke:#7A3D98,stroke-width:2px,color:#4D2462
classDef inventory fill:#EFF2F4,stroke:#6C7780,stroke-width:2px,color:#343A40
classDef finance fill:#FFEAEA,stroke:#D73A49,stroke-width:2px,color:#7B1923
classDef reporting fill:#FBE9FF,stroke:#B44AC0,stroke-width:2px,color:#692273

class ACT,CUST,LEAD,SUPP,BPM crm
class CEC,SC,SCON,SB service
class OPP,PRIC,SQ,SO,DN,ARI,INP sales
class PR,PQ,PO,GRPO,API,OUTP purchasing
class BOM,MRP,SRC,PRO,ITP,RFP production
class IM,WM,DP inventory
class COA,GLA,GLAD,CA,JE,APAR,CM,REC finance
class BR,IAR,ABR,FR,PRR reporting

style CRM fill:#F8FCF9,stroke:#62B76E,stroke-width:2px
style CORE fill:#FFFFFF,stroke:#B8BEC4,stroke-width:1px
style SERVICE fill:#FFFDF4,stroke:#D6B600,stroke-width:2px
style INVENTORY fill:#F8F9FA,stroke:#7C858D,stroke-width:2px
style SALES fill:#FFF8F0,stroke:#F28C28,stroke-width:2px
style PURCHASING fill:#F3FAFF,stroke:#168AC1,stroke-width:2px
style PRODUCTION fill:#FBF6FE,stroke:#7A3D98,stroke-width:2px
style FINANCE fill:#FFF6F6,stroke:#D73A49,stroke-width:2px
style REPORTING fill:#FDF6FF,stroke:#B44AC0,stroke-width:2px
```

## Archivo fuente

El archivo fuente del diagrama se encuentra en [`diagrama_procesos.mmd`](./diagrama_procesos.mmd).
