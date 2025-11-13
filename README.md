# MILA-Hackathon - Équipe 3

Hackathon santé numérique - 13-14 novembre 2025

## 📁 Structure du projet

```
MILA-Hackathon/
├── data/                    # Jeux de données
│   ├── CanPath_Student_Dataset_V2-20251113T130900Z-1-001/
│   └── MDClone-20251113T131252Z-1-001/
├── documentation/            # Documentation du hackathon (organisée)
│   ├── 01_Questions_de_recherche.md          # 10 questions de recherche suggérées
│   ├── 02_Projet_de_recherche.md              # Projet de recherche (version anglaise)
│   ├── 03_Notes_Hackathon.md                  # Notes générales du hackathon
│   ├── 04_Plan_Juan_Felipe.md                 # Plan de recherche et présentation
│   ├── 05_Presentation_MDClone.md             # Présentation MDClone (CUSM)
│   ├── 06_Presentation_CANPATH.md             # Présentation CANPATH
│   ├── 07_Presentation_POYM.md                # Présentation POYM (CHUS)
│   ├── 08_Article_MDClone_Validation.md       # Article validation données synthétiques
│   ├── 09_Idees_Projet_Agent_IA.md            # Idées concrètes pour le projet
│   └── Article_WSI_Agents_MultiAgent_System.pdf  # Article multi-agents (inspiration)
├── .gitignore                # Exclut les données sensibles (data/)
└── README.md
```

## 👥 Membres de l'équipe

- Julie-Anne Jardret
- Cathicia
- Juan Felipe Duran
- Mouni
- Rayyan
- PL_92

## 🎯 Axe thématique choisi

**Déterminants sociaux de la santé** (avec focus sur la santé mentale)

## 📊 Jeux de données utilisés

### Jeux de données principaux

#### CANPATH
- **Description** : Grande cohorte pancanadienne (santé, mode de vie, facteurs de risque)
- **Variables clés** :
  - Démographiques : `SDC_*` (âge, sexe, etc.)
  - Santé : `HS_*` (état de santé général)
  - Conditions médicales : `DIS_*` (maladies, troubles)
  - Comportements : `SLE_*` (sommeil), `ALC_*` (alcool), `SMK_*` (tabac), `NUT_*` (nutrition), `PA_*` (activité physique)
  - Environnement (CANUE) : pollution (PM2.5, NO2, SO2, O3), température, indice de défavorisation
- **Utilité** : Analyses populationnelles, associations santé-environnement, facteurs de risque

#### MDClone (CUSM)
- **Description** : Données synthétiques générées à partir de dossiers cliniques du CUSM
- **Tables disponibles** :
  - `DBT_type_2.csv` : Données sur diabète type 2
  - `ed_visit.csv` : Visites aux urgences
  - `HW.csv` : Vagues de chaleur
  - `Poll.csv` : Données de pollution
- **Utilité** : Prototypage rapide de pipelines cliniques, analyses de trajectoires de soins

#### POYM (CHUS) - Challenge
- **Description** : Données synthétiques d'admission hospitalière (123,646 patients, 248,485 hospitalisations)
- **Variables** : Démographiques, caractéristiques d'admission, diagnostics, comorbidités
- **Challenge** : Analyser la performance de 2 modèles RandomForest pré-entraînés
- **GitHub** : https://github.com/LaribiHakima/rsn_challenge
- **Dataset** : https://zenodo.org/records/12954673

### Jeux de données publics complémentaires
- [ ] Statistiques Canada - Health
- [ ] CIHI (Canadian Institute for Health Information)
- [ ] Données Québec - Health
- [ ] Canada Health Infobase

## 💡 Projet : Agent IA Multi-Expert pour Intervenants de Première Ligne en Santé Mentale

### Concept principal
Développer un système d'agents IA spécialisés pour outiller les intervenants de première ligne (infirmières scolaires, travailleurs sociaux, intervenants communautaires) dans la détection précoce, l'évaluation et l'orientation des personnes en détresse psychologique.

### Problématique
- **Manque d'accès aux ressources** : Les intervenants de première ligne manquent de ressources spécialisées et accessibles
- **Inégalités régionales** : Les ressources varient selon les régions (urbain vs rural)
- **Détection tardive** : Les problèmes de santé mentale détectés tôt sont plus faciles à traiter
- **Besoin d'expertise multidisciplinaire** : Les intervenants doivent faire des décisions informées sans avoir accès à tous les experts

### Solution proposée
Un système d'agents IA spécialisés (Model Zoo) qui agissent comme des experts virtuels :

1. **Red Flag Expert** : Détection de signaux d'alarme
2. **Coaching Expert** : Accompagnement et soutien
3. **Clinical Interview Expert** : Aide à l'entretien clinique
4. **De-escalation Expert** : Gestion de crises
5. **Stat Agent** : Statistiques régionales et contextuelles
6. **Global Impact Agent** : Analyse d'impact intersectoriel (ex: logement → coûts hospitaliers)

### Objectifs
- Outiller les intervenants de première ligne avec une expertise multidisciplinaire accessible
- Faciliter la détection précoce des problèmes de santé mentale
- Améliorer l'orientation vers les ressources appropriées
- Réduire les inégalités d'accès aux soins selon les régions
- Favoriser le dialogue et l'intelligence collective

## 📚 Documentation

Toute la documentation du hackathon est organisée dans le dossier `documentation/` :

- **`01_Questions_de_recherche.md`** : 10 questions de recherche suggérées pour MDClone
- **`02_Projet_de_recherche.md`** : Version anglaise des questions de recherche
- **`03_Notes_Hackathon.md`** : Notes générales sur le hackathon (objectifs, critères, ressources)
- **`04_Plan_Juan_Felipe.md`** : Plan détaillé du projet Agent IA avec architecture
- **`05_Presentation_MDClone.md`** : Présentation complète sur MDClone (CUSM)
- **`06_Presentation_CANPATH.md`** : Présentation complète sur CANPATH
- **`07_Presentation_POYM.md`** : Présentation complète sur le challenge POYM (CHUS)
- **`08_Article_MDClone_Validation.md`** : Résumé de l'article scientifique sur la validation des données synthétiques
- **`09_Idees_Projet_Agent_IA.md`** : Idées concrètes pour le projet Agent IA (basé sur le plan de Juan)
- **`Article_WSI_Agents_MultiAgent_System.pdf`** : Article sur systèmes multi-agents collaboratifs (inspiration architecture)

## 🔗 Ressources utiles

### Documentation externe
- [Déterminants sociaux de la santé - Canada.ca](https://www.canada.ca/fr/sante-publique/services/promotion-sante/sante-population/est-determine-sante.html)
- [Intégration de multiples déterminants sociaux de la santé - OTSTCFQ](https://www.otstcfq.org/article-dossier-special/lintegration-de-multiples-determinants-sociaux-de-la-sante/)
- [Accès aux services de santé mentale - CIHI](https://www.cihi.ca/fr/le-pouls-des-soins-de-sante-un-apercu-de-la-situation-au-canada-2023/lacces-aux-services-lies-a-la-sante-mentale-et-a-lutilisation-de-substances-demeure)

### Notes de l'équipe
- [Document de planification - Juan Felipe](https://docs.google.com/document/d/11K8uFI3NGsCDsLZmZa4qReuWgrEAxXWRbmFGeVaA_Mk/edit)

## 🚀 Développement

### Architecture proposée

#### Agents spécialisés (Model Zoo)
- **Trouble de l'humeur** : Dépression, anxiété
- **Trouble psychotique** : Schizophrénie, troubles délirants
- **Trouble d'usage de substance** : Dépendances
- **Nutritionniste** : Conseils nutritionnels
- **Travailleur social** : Ressources sociales
- **Intervenant communautaire** : Ressources communautaires
- **Psychiatre** : Évaluation psychiatrique
- **Psychologue** : Évaluation psychologique
- **Ergothérapeute** : Évaluation fonctionnelle
- **Infirmier** : Soins infirmiers

#### Sources de données pour l'entraînement
- Rapports de psychologues et ergothérapeutes
- Questionnaires complets d'évaluation
- Bases de données spécialisées par domaine/région
- Données CANPATH pour contextes régionaux

### Technologies suggérées
- Framework d'agents IA (ex: LangChain, AutoGen, CrewAI)
- LLM pour le traitement du langage naturel
- Base de données pour stocker les connaissances
- API pour l'intégration avec les systèmes existants

### Architecture Multi-Agents Collaboratifs (Inspirée de l'article WSI-Agents)
- **Agent Orchestrateur** : Coordonne et route les requêtes vers les agents spécialisés
- **Communication inter-agents** : Les agents se consultent entre eux pour des réponses plus complètes
- **Fusion multi-modale** : Combine texte (observations) + contexte régional + statistiques
- **Consensus entre agents** : Calcul d'accord entre plusieurs agents pour des décisions robustes

### Utilisation des Données Disponibles

#### CANPATH - Pour le Stat Agent
- **Variables santé mentale** : Sommeil (`SLE_*`), alcool (`ALC_*`), activité physique (`PA_*`), état de santé (`HS_*`)
- **Environnement** : Défavorisation (`MSD_*`), pollution (`PM25DAL_01`, `NO2LUR_02`), température
- **Utilisation** : Statistiques régionales, profils contextuels, associations santé-environnement

#### MDClone - Pour identifier des patterns
- **Visites aux urgences** (`ed_visit.csv`) : Patterns de crises de santé mentale
- **Vagues de chaleur** (`HW.csv`) : Association avec visites aux urgences
- **Pollution** (`Poll.csv`) : Impact sur santé mentale
- **Utilisation** : Trajectoires de soins, facteurs déclencheurs, patterns temporels

#### POYM - Pour facteurs de risque
- **Diagnostics** (`adm_*`, `dischargedx_*`) : Comorbidités psychiatriques
- **Utilisation** : Identification de patients à haut risque, facteurs de réadmission

### Prochaines étapes
1. Structurer le pitch (3 minutes)
2. Clarifier l'aspect scientifique et analytique (Juan)
3. Trouver exemples concrets avec CANPATH (PL)
4. Ajouter aspects cybersécurité et finance

## 📝 Notes

- Présentation finale : 3 minutes
- Focus sur l'impact et la captation de l'audience
