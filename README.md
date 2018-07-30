# Hoegh SSCS Docs

## Table of Contents

- [Hoegh SSCS Docs](#hoegh-sscs-docs)
    - [Table of Contents](#table-of-contents)
    - [Conventions](#conventions)
    - [Basic SSCS Workflow](#basic-sscs-workflow)
        - [Description](#description)
        - [SSCS entities creation process diagram](#sscs-entities-creation-process-diagram)
    - [Nomination workflow](#nomination-workflow)
        - [Description](#description)
        - [Creating a new Nomination](#creating-a-new-nomination)
            - [Fetching existing LNGC data and Refreshment Type by IMO](#fetching-existing-lngc-data-and-refreshment-type-by-imo)
            - [Fetching Company names](#fetching-company-names)
            - [Fetching company contacts](#fetching-company-contacts)
        - [Create Nomination diagram](#create-nomination-diagram)

## Conventions

- [something] - an entity;
- {something} - an action;
- #something# - bool expression;

## Basic SSCS Workflow

### Description

The SSCS business-process cosists of three main entities:

- Nomination;
- Case Study;
- STS;

The creating process on these entities is described on the diagram below:

### SSCS entities creation process diagram

<pre>
        Start
          +
          |
          | {Create new Nomination}
          |
+---------v----------+
|                    |
|    [Nomination]    |
|                    |
+---------+----------+
          |
          | {Approve Nomination}
          |
+---------v----------+
|                    |
|    [Case Data]     |
|                    |
+---------+----------+
          |
          | {Approve Case Data}
          |
+---------v----------+
|                    |
|       [STS]        |
|                    |
+--------------------+
 </pre>

## Nomination workflow

### Description

The Nomination is the first entity created during the SSCS business-process. It describes the base data in the LNGC - FSRU relations.

### Creating a new Nomination

To create a new nomination, this data is required:

- Terminal company Id (the Company that is creating the Nomination);
- FSRU Id (this is the FSRU for which the Nomiantion is being created);
- IMO (the IMO of the LNGC for this Nomination);
- Ship name (the name of the LNGC for this Nomination);
- Loading date period;
- Scheduled arriving date;
- Requesting company name, details and contacts;
- Ship owner name, details and contacts;
- Ship operator name, details and contacts;

Before the Nomiantion entity is created, Company and Contact enities are created or fetched from the database to be linked to the created Nomiantion.

#### Fetching existing LNGC data and Refreshment Type by IMO

There is a backend endpoint, that provides an ability to fetch exising LNGC data by an IMO. Also, there is an endpoint, that returns Refreshment Type info by IMO and FSRU. A Nomintion will have a Refreshment Type, if there is a completed STS for a LNGC (IMO) - FSRU pair.

#### Fetching Company names

There is a backend endpoint, which can return a collection of existing companies by a string, that contains a Company name (or part of the name).

#### Fetching company contacts

There is a backend endpoint, which can return a collection of existing contacts by a string, that compaing a E-Mail (or part of the E-Mail).

### Create Nomination diagram

<pre>
                      +------------------------------------------------+
                      |                                                |
                      |  {Request to endpoint with [Nomination] data}  |
                      |                                                |
                      +-------------------------+-+--------------------+
                                                | |
                                                | +-------------------------------------------+
                                                |                                             |
                      +-------------------------v----------------------+                      |
                      |                                                |                      |
                      |           #Do the [Companies] exist?#          |                      |
                      |                                                |                      |
                      +---------+----------------------------+---------+                      |
                                |                            |                                |
                                | No                         | Yes                            |
                                |                            |                                |
        +-----------------------v---------+        +---------v----------------------------+   |
        |                                 |        |                                      |   |
        | {Create new [Company] entities} |        | {Fetch existing [Company] entities}  |   |
        |                                 |        |                                      |   |
        +-----------------+---------------+        +----------------+---------------------+   |
                          |                                         |                         |
+-------------------------+-----------------------------------------+                         |
|                                                                                             |
|                                               +---------------------------------------------+
|                                               |
|                     +-------------------------v----------------------+
|                     |                                                |
|                     |           #Do the [Contacts] exist?#           |
|                     |                                                |
|                     +---------+----------------------------+---------+
|                               |                            |
|                               | No                         | Yes
|                               |                            |
|       +-----------------------v---------+        +---------v----------------------------+
|       |                                 |        |                                      |
|       | {Create new [Contact] entities} |        | {Fetch existing [Contact] entities}  |
|       |                                 |        |                                      |
|       +--------------------------+------+        +--------------------+-----------------+
|                                  |                                    |
|                                  |                                    |
+----------------------------------+----+-------------------------------+
                                        |
                                        |
                            +-----------v------------------------+
                            |                                    |
                            | {Create a new [Nomiantion] entity} |
                            |                                    |
                            +------------------------------------+
</pre>
