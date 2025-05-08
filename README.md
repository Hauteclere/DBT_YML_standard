# DBT_YML_standard

> [!CAUTION]  
> This document is in DRAFT

---

## Contents
- [1 - Standard](#1---standard)
- [2 - Example Change](#2---example-change)

---

## 1 - Standard  

```yml
    sources:
      - name:                             # Use the name of the application in the application catalogue
        description:                      # Use the description of the application from the application catalogue 
        schema:                           # Specify the schema name
        loader:                           # Specify the specific integration that loads the data, by its canonical name in the integration catalogue
        loaded_at_field: "{{ var('loaded_at_expression') }}"
        freshness:
          warn_after: { count: 365, period: day }
        tables:
          - name:                         # Use a clear, concise logical name for the table entity
            description:                  # Use the canonical description from the data catalogue
            identifier:                   # Specify the precise table name
            config:
              meta:
                infosec:                  # Specify the Security level of the table, as listed in the data catalogue
                logical_data_entities: [] # List the logical data entities that are associated with this table, as listed in the data catalogue
            columns: []                   # At present it is not necessary to document columns in the data source.
```

> [!IMPORTANT]  
> The above specification removes the following fields from the `.yml` format:
> - `ida`: This should be specified against the integration in the integration catalogue instead.

---

## 2 - Example Change

```diff
    sources:
-     - name: rm
+     - name: ResearchMaster (RM)
        description: |
-         Research Master is a legacy system but the tables were loaded in EDIE DW.
+         A research administration tool that allows users to manage scholarships, postgraduates, grants, publications, ethics/biosafety and intellectual property/commercial development.
        schema: SRC
-       loader: Azure Data Factory
+       loader: # Unknown!!
        loaded_at_field: "{{ var('loaded_at_expression') }}"
        freshness:
          warn_after: { count: 365, period: day }
        tables:
-         - name: rm4sacc
+         - name: fin_account_codes
-           description: FIN Account Codes
+           description: # unknown!!
            identifier: RM_RM4SERV_RM4SACC
+           config:
+             meta:
+               infosec: Official
+               logical_data_entities: # Unknown!!
            columns: []
```
