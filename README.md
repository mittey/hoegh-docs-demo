# Hoegh SSCS Docs

## Table of Contents

- [Hoegh SSCS Docs](#hoegh-sscs-docs)
    - [Table of Contents](#table-of-contents)
    - [Basic SSCS Workflow](#basic-sscs-workflow)
        - [SSCS entities creation process diagram](#sscs-entities-creation-process-diagram)

## Basic SSCS Workflow

The SSCS business-process cosists of three main entities:

- Nomination
- Case Study
- STS

The creating process on these entities is described on the diagram below:

### SSCS entities creation process diagram

<pre>
          +
          |
          | Create new Nomination
          |
+---------v----------+
|                    |
|     Nomination     |
|                    |
+---------+----------+
          |
          | Approve Nomiantion
          |
+---------v----------+
|                    |
|     Case Data      |
|                    |
+---------+----------+
          |
          | Approve Case Data
          |
+---------v----------+
|                    |
|        STS         |
|                    |
+--------------------+
 </pre>
