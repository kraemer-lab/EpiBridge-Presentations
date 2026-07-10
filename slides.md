<style>
.slidev-layout p {
  opacity: 1 !important;
  color: inherit !important;
}
</style>

# EpiBridge
## Supporting collaborative research on sensitive datasets

**Kraemer Lab, University of Oxford**

---

# The Problem

<span />

Your research group holds sensitive data.

Your need collaborators to work with it — but you cannot simply send them the data

How do you enable analysis while maintaining control?

---

# How Research Happens Today

<span />

Large institutions provision **Trusted Research Environments (TREs)**: secure facilities where researchers access data through remote desktops and notebooks

TREs provide strong governance but require substantial infrastructure

Many labs and smaller institutions hold governed data but lack large research computing facilities

---

# EpiBridge: Locally Deployable

```mermaid
%%{init: {'theme': 'neutral', 'themeVariables': { 'lineColor': '#888888', 'primaryTextColor': '#555' }}}%%
flowchart LR
  R([Your computer]) --> B[Analysis package]
  B --> E[Institutional execution]
  E --> O[Governed output]
```

EpiBridge is a deployable platform that runs on a single machine — no data centre required.

Institutions install it locally and immediately gain a governed execution pipeline for sensitive data.

---

# What This Means

<span />

**For researchers:**
- Prepare analyses in your usual environment
- Submit analyses
- Receive results

**For institutions:**
- Governed data stays in your control
- Every execution is audited
- Outputs are reviewed before release

---

# Who Is It For

<span />

Any institution with sensitive data

Labs collaborating across sites

Organisations wanting governance without large infrastructure

EpiBridge can run on a single computer

---

<div style="max-width:60%;margin:auto">

```mermaid
%%{init:{
  "theme":"base",
  "flowchart":{
    "curve":"basis",
    "nodeSpacing":65,
    "rankSpacing":80,
    "padding":20,
    "htmlLabels":true
  },
  "themeVariables":{

    "background":"#ffffff",
    "mainBkg":"#ffffff",

    "fontFamily":"Inter, Helvetica, Arial",
    "fontSize":"18px",

    "primaryColor":"#ffffff",
    "primaryBorderColor":"#475569",
    "primaryTextColor":"#1e293b",

    "secondaryColor":"#ffffff",
    "secondaryBorderColor":"#475569",
    "secondaryTextColor":"#1e293b",

    "tertiaryColor":"#ffffff",
    "tertiaryBorderColor":"#475569",
    "tertiaryTextColor":"#1e293b",

    "clusterBkg":"#f8fafc",
    "clusterBorder":"#94a3b8",

    "lineColor":"#64748b",
    "defaultLinkColor":"#64748b",

    "edgeLabelBackground":"#ffffff"
  }
}}%%

flowchart TB

subgraph User["Researcher"]
Rd[Develop Analysis]
Ra[Analysis Bundle]
Rx[Results]
Rd --> Ra
end

subgraph mod["Moderator"]
M1[Approve Analysis]
M2[Review Outputs]
M1 --- M2
end

subgraph Host["Host"]

Hd["Institutional Datasets"]

subgraph VM["Virtual Machine"]

Ed[EpiBridge Portal]

Er[Analysis Approval]
Ec[Execution Environment]

Cc[Build Execution Image]
Cx[Execution]

Or[Output Review]
Ox[Approved Outputs]

Cc --> Cx
M1 -...-> Er
Er --> Cc
Ec --> Cc

Cx --> Or
M2 -...-> Or
Or --> Ox
Ox --> Rx

Ed --> Er

end

Hd -...-> Cx
Ra --> Ed

end

```

</div>

---

# From the Researcher's Side

- Inspect the institution's data schema, sample datasets and execution environment
- Write your analysis in R, Python, Stata — your usual tools
- Specify environment execution requirements
- Package and submit as an Analysis Bundle
- Wait for institutional approval / execution
- Download results when released

You never access the governed data directly

---

# From the Moderator's Side

- Review incoming Analysis Bundles
- Approve or reject submissions
- Monitor execution
- Review output results
- Release approved outputs

The institution governs every step

---

# Analysis Bundle

<span />

An Analysis Bundle is an **immutable description of an analysis**.

Typical contents for a Python-based analysis:

```text
analysis.zip
├── run.py
├── requirements.txt
└── README.md
```

Typical contents for a Conda-based analysis:
```text
analysis.zip
├── run.sh
├── environment.yml
└── README.md
```

---

# Building the Execution Image

<div style="width: 65%; margin:auto;">

```mermaid
%%{init:{
  "theme":"base",
  "flowchart":{
    "curve":"basis",
    "nodeSpacing":65,
    "rankSpacing":80,
    "padding":20,
    "htmlLabels":true
  },
  "themeVariables":{

    "background":"#ffffff",
    "mainBkg":"#ffffff",

    "fontFamily":"Inter, Helvetica, Arial",
    "fontSize":"18px",

    "primaryColor":"#ffffff",
    "primaryBorderColor":"#475569",
    "primaryTextColor":"#1e293b",

    "secondaryColor":"#ffffff",
    "secondaryBorderColor":"#475569",
    "secondaryTextColor":"#1e293b",

    "tertiaryColor":"#ffffff",
    "tertiaryBorderColor":"#475569",
    "tertiaryTextColor":"#1e293b",

    "clusterBkg":"#f8fafc",
    "clusterBorder":"#94a3b8",

    "lineColor":"#64748b",
    "defaultLinkColor":"#64748b",

    "edgeLabelBackground":"#ffffff"
  }
}}%%
flowchart LR

Bundle["Analysis Bundle"]

Req["requirements.txt"]

Environment["Execution Environment"]

Image["Execution Image"]

Bundle --> Req

Environment -.->|Institutional base| Image

Req --> Image
```

</div>

### Institutional Build

The platform uses a curated builder template.

```
FROM ${BASE_IMAGE}

COPY requirements.txt .

RUN pip install ...
```

Only the dependency specification influences the image

Once built, the environment can be reused

---

# Why this matters

<span />

Researchers describe:

- **what** should be executed
- **which** dependencies are required
- optionally **how** the image should be extended

The institution remains responsible for:

- the execution environment
- execution
- governance
- release

This separation preserves reproducibility while allowing controlled flexibility

---

# EpiBridge

<span />

**Project Repository**

<https://github.com/kraemer-lab/EpiBridge>

Source code, documentation, and issue tracking.
