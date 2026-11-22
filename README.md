# Log Analysis & Threat Detection Tool

## 1. Présentation du projet

Outil Python qui prend en entrée des fichiers de logs SSH et Web (Apache/Nginx).

L'outil analyse et structure les événements présents dans ces fichiers, puis les compare à des règles pour identifier les activités suspectes et générer des alertes.

Une fonctionnalité personnelle sera la corrélation temporelle des échecs et des connexions SSH réussies, afin d'identifier le compte potentiellement compromis.

Projet à vocation pédagogique et défensive, limité à l'analyse de journaux provenant d'environnements autorisés.


## 2. Le flux de fonctionnement

```mermaid


flowchart TD
    subgraph INPUT["1. Sources de données"]
        SSH["Linux Authentication Logs<br/>auth.log / secure"]
        WEB["Web Server Logs<br/>Apache / Nginx"]
    end

    subgraph PROCESS["2. Traitement des journaux"]
        PARSE["Log Parsing<br/>Lecture et extraction des champs"]
        NORMALIZE["Normalization<br/>Conversion en événements structurés"]
        VALIDATE["Validation<br/>Gestion des lignes invalides"]
    end

    subgraph DETECTION["3. Moteur de détection"]
        RULES["Rule-Based Detection<br/>Échecs répétés, événements suspects"]
        CORRELATION["Temporal Correlation<br/>Échecs SSH suivis d'un succès"]
        ANALYSIS["Event Analysis<br/>IP source, compte, horodatage"]
    end

    subgraph OUTPUT["4. Résultats"]
        ALERT["Alert Generation<br/>Type, sévérité et justification"]
        REPORT["Analysis Report<br/>Événements, alertes et preuves"]
    end

    SSH --> PARSE
    WEB --> PARSE
    PARSE --> NORMALIZE
    NORMALIZE --> VALIDATE
    VALIDATE --> RULES
    VALIDATE --> CORRELATION
    RULES --> ANALYSIS
    CORRELATION --> ANALYSIS
    ANALYSIS --> ALERT
    ALERT --> REPORT

    classDef source fill:#dbeafe,stroke:#2563eb,color:#1e3a8a
    classDef process fill:#e0f2fe,stroke:#0284c7,color:#075985
    classDef detection fill:#fef3c7,stroke:#d97706,color:#78350f
    classDef output fill:#dcfce7,stroke:#16a34a,color:#166534

    class SSH,WEB source
    class PARSE,NORMALIZE,VALIDATE process
    class RULES,CORRELATION,ANALYSIS detection
    class ALERT,REPORT output

```
