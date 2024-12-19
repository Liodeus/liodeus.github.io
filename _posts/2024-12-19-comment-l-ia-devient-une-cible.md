---
layout: post
title: Comment l’IA devient une cible - Le point de vue d’un pentester
tags: [AI, Security, LLM, RAG]
description: "Comment l’IA devient une cible - Le point de vue d’un pentester"
---

Cet article est une adaptation d'une présentation interne réalisée au sein de mon entreprise sur la sécurité des systèmes d'intelligence artificielle. D'où la présence d'illustrations à chaque section, initialement conçues pour accompagner la présentation orale et conservées ici pour faciliter la compréhension des concepts abordés.

- [Introduction](#introduction)
- [Concepts de base](#concepts-de-base)
- [Menaces principales et risques](#menaces-principales-et-risques)
- [Processus de Red Teaming](#processus-de-red-teaming)
- [Conclusion](#conclusion)
- [Sources](#sources)
- [Lexique](#lexique)

---

# Comment l’IA devient une cible - Le point de vue d’un pentester
## Introduction
### Contexte et objectifs
Depuis ces dernières années, l'IA et plus particulièrement les LLM (Large Language Models) se sont largement démocratisés, s'intégrant progressivement dans nos systèmes et infrastructures d'entreprise. Ce retour d'expérience explore la sécurité des systèmes d'IA du point de vue d'un pentester, en se concentrant sur les méthodologies d'évaluation, les risques spécifiques et les stratégies de test essentielles pour garantir leur robustesse.

### Avertissement
Avant de plonger dans le sujet, il est important de rappeler certains points pour mieux contextualiser ce qui va suivre :

1. **Recherche personnelle** : Cette présentation repose sur mes expériences et recherches personnelles.
2. **Vérité non absolue** : Les méthodologies et techniques évoquées ici ne sont pas immuables. La sécurité de l'IA évolue constamment et exige une adaptation continue.
3. **Méthodologies alternatives** : Les approches présentées ne sont qu'une partie des possibilités existantes. Il existe d'autres méthodologies et outils pour tester la sécurité de l'IA.

<p align="center" width="100%">
    <img src="https://raw.githubusercontent.com/Liodeus/liodeus.github.io/refs/heads/master/assets/imgs/AI/warning.svg"> 
</p>

---

## Concepts de base
### Équilibrer les approches de sécurité
Dans le domaine de la cybersécurité, il est crucial d'adopter une approche équilibrée pour protéger efficacement les systèmes contre les diverses menaces. Deux méthodes complémentaires se distinguent : le Red Teaming et le Pentesting. Chacune de ces approches joue un rôle essentiel dans la sécurisation des infrastructures, notamment celles intégrant l'intelligence artificielle (IA).

#### L'importance de l'équilibre
Pour garantir une sécurité optimale, il est crucial de combiner ces deux approches. Le Red Teaming permet de se préparer aux attaques sophistiquées et spécifiques à l'IA, tandis que le Pentesting assure la protection contre les vulnérabilités traditionnelles. En équilibrant ces méthodes, les organisations peuvent construire des défenses plus robustes et mieux protéger leurs systèmes contre une large gamme de menaces.

<p align="center" width="100%">
    <img src="https://raw.githubusercontent.com/Liodeus/liodeus.github.io/refs/heads/master/assets/imgs/AI/redteam_vs_pentest.svg"> 
</p>

### Les LLM ne se limitent pas qu’au texte
Les modèles de langage, ne se limitent pas à la génération de texte. Ils s'appliquent à des domaines variés tels que le traitement du langage naturel (NLP), la vision par ordinateur (computer vision) pour les images, et l'audio pour les voix. Ils acceptent également d'autres formats d'entrée de données, formant ainsi des modèles multimodaux capables de traiter et croiser différents types d'informations. Cette diversité élargit considérablement leur surface d'attaque.

<p align="center" width="100%">
    <img src="https://raw.githubusercontent.com/Liodeus/liodeus.github.io/refs/heads/master/assets/imgs/AI/multimodales.svg"> 
</p>

---

## Menaces principales et risques
### Papiers de recherche
De nombreuses recherches sortent chaque mois, dévoilant de nouvelles attaques spécifiques à l'IA. Parmi mes principales sources d'information figure [arxiv.org](arxiv.org), où des papiers récents explorent des attaques novatrices. En voici quelques-unes pour l'exemple :

- **LoBAM** : Ajout d'une backdoor lors de la fusion de modèles. [Lien PDF](https://arxiv.org/pdf/2411.16746)
- **"Moralized" Multi-Step Jailbreak Prompts** : Contournement des mécanismes de sécurité via des prompts multi-étapes. [Lien PDF](https://arxiv.org/pdf/2411.16730)
- **Memory Backdoor Attacks** : Extraction de données d'entraînement confidentielles. [Lien PDF](https://arxiv.org/pdf/2411.14516)
- **AnywhereDoor** : Backdoor flexible pour contrôler les modèles de détection d'objets. [Lien PDF](https://arxiv.org/pdf/2411.14243)

Cette veille continue est essentielle pour anticiper les menaces et adapter des stratégies de sécurité en conséquence.

<p align="center" width="100%">
    <img src="https://raw.githubusercontent.com/Liodeus/liodeus.github.io/refs/heads/master/assets/imgs/AI/research_papers.svg"> 
</p>

### Risques spécifiques aux LLM
Le premier jet du Top 10 OWASP dédié aux vulnérabilités des LLM date de 2023. Cependant, avec les avancées rapides et les nombreuses recherches sur le sujet, le Top 10 a dû être mis à jour et celui de 2025 a évolué pour s'adapter aux nouvelles menaces et découvertes. Celui-ci comprend :

- **LLM01:2025 Prompt Injection** : Manipulation des entrées pour influencer les réponses.
- **LLM02:2025 Sensitive Information Disclosure** : Divulgation involontaire d'informations sensibles.
- **LLM03:2025 Supply Chain** : Vulnérabilités introduites via les dépendances de la chaîne d'approvisionnement.
- **LLM04:2025 Data and Model Poisoning** : Corruption des données ou du modèle d'entraînement.
- **LLM05:2025 Improper Output Handling** : Gestion inadéquate des sorties générées.
- **LLM06:2025 Excessive Agency** : Autorisations excessives menant à des actions imprévues.
- **LLM07:2025 System Prompt Leakage** : Fuite de prompts systèmes sensibles.
- **LLM08:2025 Vector and Embedding Weaknesses** : Faiblesses dans les vecteurs ou les embeddings exploités.
- **LLM09:2025 Misinformation** : Génération de fausses informations.
- **LLM10:2025 Unbounded Consumption** : Consommation excessive de ressources.

L'OWASP met en lumière les principales menaces auxquelles les LLM sont exposés, et il est essentiel, de comprendre comment ces vulnérabilités peuvent être exploitées pour causer des dommages.

<p align="center" width="100%">
    <img src="https://raw.githubusercontent.com/Liodeus/liodeus.github.io/refs/heads/master/assets/imgs/AI/volcano.svg"> 
</p>

### Exemples concrets
#### Freysa
[Freysa](https://www.freysa.ai/) est une plateforme innovante où les utilisateurs peuvent participer à des défis visant, entre autres, à convaincre un agent IA de transférer des fonds d'une cagnotte. Par exemple, dans un défi récent, un utilisateur a réussi à convaincre l'IA Freysa de transférer plus de **47 000 dollars** en utilisant une stratégie de prompt injection astucieuse. L'utilisateur a réussi à contourner les directives de l'IA en lui faisant croire qu'une demande de transfert était légitime, malgré les protections mises en place.

#### JailbreakMe
[JailbreakMe](https://jailbreakme.xyz/), quant à elle, est une plateforme décentralisée où les organisations peuvent tester leurs modèles d'IA en organisant des tournois où les utilisateurs gagnent des récompenses pour trouver des failles et "jailbreak" les agents IA. Par exemple, dans un tournoi récent, un agent IA appelé Zynx a été mis au défi de protéger un secret. Les participants ont tenté de le convaincre de révéler ce secret en utilisant des dialogues et des prompts spécialement conçus pour contourner les protections de l'IA.

Ces exemples montrent à quel point les systèmes d'IA peuvent être vulnérables si les prompts ne sont pas correctement filtrés ou si les directives de l'IA ne sont pas suffisamment robustes. Ils démontrent également que les attaques par prompt injection peuvent être très efficaces, même contre des modèles d'IA conçus pour être sécurisés. Cela souligne l'importance de tester régulièrement les modèles d'IA pour identifier et corriger ces vulnérabilités avant leur déploiement en production.

---

## Processus de Red Teaming
### Étapes clés
Le Red Teaming suit un processus structuré comprenant plusieurs étapes essentielles :
- **Planification et préparation** : Définition du périmètre et planification du Red Teaming pour le système d'IA cible.
- **Cartographie des risques** : Analyse des risques et développement de scénarios de risques et d'attaques.
- **Réalisation des scénarios d'attaque** : Exécution des scénarios et prise de notes détaillées.
- **Rapport** : Analyse des résultats et rédaction d'un rapport avec des recommandations claires.

<p align="center" width="100%">
    <img src="https://raw.githubusercontent.com/Liodeus/liodeus.github.io/refs/heads/master/assets/imgs/AI/etapes_clés.svg"> 
</p>

### Modèles de LLM
Définir le type de modèles utilisés par le client est essentiel pour adapter les tests de sécurité. Parmi les catégories courantes :
- **LLM développés en interne** : modèles créés et entraînés spécifiquement par l'organisation.
- **LLM pré-entraînés avec fine-tuning par d'autres organisations** : modèles ajustés pour des besoins spécifiques après un pré-entraînement initial.
- **LLM open source** : modèles accessibles publiquement sans modifications supplémentaires.
- **LLM open source avec fine-tuning** : modèles open source adaptés pour des tâches spécifiques.
- **LLM accessibles via API externe** : solutions hébergées fournies par des tiers et utilisées à distance.

Une bonne compréhension de ces catégories permet de poser les bases pour des tests efficaces.

<p align="center" width="100%">
    <img src="https://raw.githubusercontent.com/Liodeus/liodeus.github.io/refs/heads/master/assets/imgs/AI/configurations_client.svg"> 
</p>

### Quel type de tests conduire ?
Les tests doivent inclure des scénarios réalistes adaptés au niveau de connaissance disponible :
- **Black-box** : Utilisé sans aucune information préalable sur le système, garantissant un test impartial.
- **Gray-box** : Combine des informations partielles pour trouver un équilibre entre précision et flexibilité.
- **White-box** : Exploite une connaissance complète pour mener des tests approfondis et exhaustifs.

<p align="center" width="100%">
    <img src="https://raw.githubusercontent.com/Liodeus/liodeus.github.io/refs/heads/master/assets/imgs/AI/type_of_redteam.svg"> 
</p>

### Quel environnement ?
Il est essentiel de choisir l'environnement de tests avec soin :
- **Environnement de production** : Idéal pour l'application réelle, mais plus risqué en raison de l'impact potentiel sur les systèmes en direct.
- **Environnement de développement** : Adapté aux premières étapes de développement, mais peut manquer de réalisme.
- **Environnement de pré-production** : Offre un équilibre entre réalisme et sécurité, permettant des tests dans des conditions similaires à la production.

<p align="center" width="100%">
    <img src="https://raw.githubusercontent.com/Liodeus/liodeus.github.io/refs/heads/master/assets/imgs/AI/environments.png"> 
</p>

### Scénarios de risques et d’attaques
Avant d'entreprendre des tests de sécurité approfondis, il est essentiel de structurer les étapes préparatoires 
- **Compréhension du système d'IA** : Collecte d'informations sur les modèles utilisés, les données d'entraînement et les interactions prévues avec l'environnement.
- **Identification des éléments clés** : Déterminer les fonctionnalités critiques et les zones à haut risque pour concentrer les efforts.
- **Réflexion sur des scénarios d'attaque** : Élaborer des scénarios réalistes exploitant les vulnérabilités potentielles, comme des attaques par empoisonnement ou des exfiltrations de données.
- **Mise en œuvre des scénarios** : Définir clairement les objectifs, méthodes et ressources nécessaires pour exécuter les tests de manière efficace et exploitable.

<p align="center" width="100%">
    <img src="https://raw.githubusercontent.com/Liodeus/liodeus.github.io/refs/heads/master/assets/imgs/AI/scenarios.svg"> 
</p>

### Quelle méthode utiliser pour exécuter les attaques ?
Pour conduire des tests d'attaque efficaces, il existe plusieurs approches complémentaires :
- **Outils automatisés** : Ils permettent de couvrir rapidement de larges surfaces d'attaque, bien qu'ils manquent souvent de flexibilité pour s'adapter à des scénarios complexes.
- **Red Teaming manuel** : Une méthode réaliste et hautement adaptable qui reproduit au mieux les comportements d'attaquants humains. Toutefois, elle demande beaucoup de temps et de ressources.
- **Agents IA** : Offrent un compromis entre automatisation et adaptabilité, mais nécessitent une configuration et une supervision experte.

L'approche idéale combine ces trois méthodes pour tirer parti de leurs avantages respectifs.

<p align="center" width="100%">
    <img src="https://raw.githubusercontent.com/Liodeus/liodeus.github.io/refs/heads/master/assets/imgs/AI/method_to_use.svg"> 
</p>

### Analyse des résultats et rapport
Après tous les préparatifs, les tests se déroulent avec plusieurs étapes clés :
- **Prise de notes** : Documenter avec précision toutes les activités réalisées tout au long des tests.
- **Rapport** : Synthétiser les résultats obtenus et analyser la gravité des vulnérabilités identifiées.
- **Compte-rendu client** : Présenter un résumé clair des découvertes et répondre aux questions ou préoccupations soulevées par le client.

<p align="center" width="100%">
    <img src="https://raw.githubusercontent.com/Liodeus/liodeus.github.io/refs/heads/master/assets/imgs/AI/resultats.svg"> 
</p>

---

## Conclusion
Tester la sécurité des systèmes d'intelligence artificielle constitue un défi majeur et crucial à l'ère de l'IA omniprésente. Ce processus exige une compréhension approfondie des modèles, des risques et des scénarios d'attaque pertinents, tout en adaptant les approches aux spécificités de chaque système. En combinant rigueur méthodologique et innovation, il est possible de mieux protéger ces technologies avancées contre les menaces actuelles et futures. Il est essentiel de maintenir une vigilance constante et de favoriser la collaboration pour assurer la sécurité et la fiabilité de l'IA, et ainsi bâtir un avenir où l'intelligence artificielle peut être utilisée de manière sûre et bénéfique pour tous.

---

## Sources

* [AI Safety Guidelines](https://aisi.go.jp/assets/pdf/ai_safety_RT_v1.00_en.pdf)
* [Advancing Red Teaming with People and AI](https://openai.com/index/advancing-red-teaming-with-people-and-ai)
* [OWASP Top 10 for LLM](https://genai.owasp.org/llm-top-10/)
* [Schémas - Napkin.ai](https://app.napkin.ai/)

---

## Lexique
- **IA (Intelligence Artificielle)** : Branche de l'informatique qui se concentre sur la création de machines capables de simuler l'intelligence humaine.
- **LLM (Large Language Model)** : Modèle de langage articificiel conçu pour générer du texte ressemblant à celui produit par un être humain.
- **RAG (Retrieval-Augmented Generation)** : Méthode qui améliore les modèles de langage en leur permettant de récupérer des informations à partir de sources externes.
- **Red Teaming** : Pratique de cyber sécurité où une équipe mime des attaquants réels pour identifier les faiblesses d'un système.
- **Pentesting (Test d'Intrusion)** : Procédure structurée pour identifier les vulnérabilités dans un système en simulant des attaques.
- **OWASP (Open Web Application Security Project)** : Organisme qui publie des directives et des listes de vulnérabilités pour les applications web, y compris l'IA.
