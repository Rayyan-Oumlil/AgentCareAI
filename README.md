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
│   ├── 13_Dashboard_Design_UI.md              # Design et interface utilisateur
│   ├── 15_Limites_Etudes_References.md        # Limites des études de référence
│   ├── 16_Resume_Analyses_PL.md              # Résumé analyses PL (variables sélectionnées)
│   └── Article_WSI_Agents_MultiAgent_System.pdf  # Article multi-agents (inspiration)
├── presentation/             # Présentation finale du hackathon
│   ├── Structure_Pitch.md    # Structure détaillée du pitch (5-6 slides)
│   ├── Validation_Utilisateurs.md  # Guide validation avec professionnels
│   ├── Hackathon_RSN_Pitch_Template (1).pdf  # Template officiel (Tess)
│   └── README.md             # Guide de la présentation
├── analyse_rayyan/           # Analyses CANPATH (Rayyan)
│   ├── analyse_depression_canpath.ipynb  # Modèle régression logistique - Facteurs risque dépression
│   └── Taches_Rayyan.md     # Liste des tâches et projets à implémenter
├── Chapitre_16 - Santé mentale et troubles mentaux.xlsx  # Données adolescents (Julie-Anne)
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

## 💡 Projet : AgentCareAI - Système Multi-Agents pour Intervenants de Première Ligne en Santé Mentale

### Concept principal

**AgentCareAI** : Un système d'agents IA spécialisés qui outille les intervenants de première ligne (infirmières scolaires, travailleurs sociaux, intervenants communautaires) travaillant avec les **jeunes du secondaire** dans la détection précoce, l'évaluation et l'orientation des personnes en détresse psychologique.

**Niveau d'intervention** : Services de prévention et d'intervention précoce en milieu scolaire (niveau 2)

**Vision** : Outiller l'intervenante de première ligne et l'amener à interagir avec l'expertise de plusieurs professionnels pour faire des décisions informées grâce à l'intelligence artificielle.

### Problématique

- **Manque d'accès aux ressources** : Les intervenants de première ligne manquent de ressources spécialisées et accessibles
- **Inégalités régionales** : Les ressources varient selon les régions (urbain vs rural)
- **Détection tardive** : Les problèmes de santé mentale détectés tôt sont plus faciles à traiter
- **Besoin d'expertise multidisciplinaire** : Les intervenants doivent faire des décisions informées sans avoir accès à tous les experts

### Solution proposée

Un système d'agents IA spécialisés qui agissent comme un **assistant de ressources** pour les intervenants de première ligne travaillant avec les jeunes du secondaire (niveau 2 : prévention et intervention précoce en milieu scolaire).

#### Agents spécialisés

Les agents sont entraînés pour détecter le besoin de l'intervenant et faire appel aux sous-modèles qu'ils auront besoin pour compléter leur tâche.

1. **Red Flag Agent** : Aide déterminer si l'intervenant devrait faire recours à une autorité de santé supérieure. C'est comme un diagnostic agent, mais on ne peut pas légalement diagnostiquer. En fait, il aide déterminer si l'intervenante devrait faire recours à une autorité de santé supérieur car le patient a un trouble plus sérieux.

2. **Coaching Agent** : C'est comme un treatment agent, il aide l'intervenant traiter le patient. Par exemple, si le patient a de l'anxiété, il faut le guider en lui donnant des avis, respecter la pyramide de Maslow, comment bien manger, comment garder des amis ou avoir des bonnes relations, exercice. Donc c'est coaching mais en pratique c'est traiter le problème mental.

3. **Clinical Interview Agent** : C'est lorsque l'intervenante ne sait PAS ce qu'il devrait demander au patient pour l'aider. Donc une entrée serait : "le patient a les symptômes A et B, qu'est-ce que je peux lui demander maintenant pour améliorer mon analyse et mon enquête". C'est comme un outil HANDY.

4. **De-escalation Agent** : Oui gérer les crises, comme attaque de panique par exemple.

5. **Stat Agent** : Fournit stats régionales rapides au besoin.

6. **Global Impact Agent** : C'est pas un agent, c'est juste un outil. L'idée est que on sauvegarde chaque interaction de l'intervenant et du modèle pour voir quelles genres de problèmes et de questions arrivent le plus souvent selon la région. Comme ça c'est comme un sondage qui nous permet de prendre action au niveau politique mais aussi pour savoir comment déployer nos ressources de santé.

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
- **`13_Dashboard_Design_UI.md`** : Design et interface utilisateur du dashboard
- **`Article_WSI_Agents_MultiAgent_System.pdf`** : Article sur systèmes multi-agents collaboratifs (inspiration architecture)

## 🔗 Ressources utiles

### Documentation externe

- [Déterminants sociaux de la santé - Canada.ca](https://www.canada.ca/fr/sante-publique/services/promotion-sante/sante-population/est-determine-sante.html)
- [Intégration de multiples déterminants sociaux de la santé - OTSTCFQ](https://www.otstcfq.org/article-dossier-special/lintegration-de-multiples-determinants-sociaux-de-la-sante/)
- [Accès aux services de santé mentale - CIHI](https://www.cihi.ca/fr/le-pouls-des-soins-de-sante-un-apercu-de-la-situation-au-canada-2023/lacces-aux-services-lies-a-la-sante-mentale-et-a-lutilisation-de-substances-demeure)

### Notes de l'équipe

- [Document de planification - Juan Felipe](https://docs.google.com/document/d/11K8uFI3NGsCDsLZmZa4qReuWgrEAxXWRbmFGeVaA_Mk/edit)

### Ressources pour justifier la pertinence (Julie-Anne)

**Articles sur besoins des intervenants** :

- [The Mental Health Training Intervention for School Nurses](https://pmc.ncbi.nlm.nih.gov/articles/PMC7036278/)
- [School Nurses&#39; Experiences in Dealing with Adolescents Having Mental Health Problems](https://pmc.ncbi.nlm.nih.gov/articles/PMC9449503/)
- [Review on school nurses&#39; training needs for mental health](https://escholarship.org/content/qt1r79h16s/qt1r79h16s.pdf)
- [Rôles des infirmières scolaires - Minnesota](https://www.health.state.mn.us/people/childrenyouth/schoolhealth/hco/mentalhlth.html)

**Note sur MH-TIPS** : Cette méthode existe mais favorise la formation continue. Notre solution (CareCircle) n'existe pas encore et offre une alternative complémentaire avec agents IA spécialisés.

**Données adolescents** :

- [Enquête québécoise sur la santé des jeunes du secondaire 2022-2023](https://statistique.quebec.ca/fr/document/sante-jeunes-secondaire-2022-2023)
- [Méthodologie](https://statistique.quebec.ca/fr/fichier/enquete-quebecoise-sante-jeunes-secondaire-2022-2023-methodologie.pdf)

## 🚀 Développement

### Architecture proposée

#### Model Zoo (Spécialistes) - Sous-modèles auxquels les agents ont accès

Les agents intermédiaires (Red Flag, Coaching, Clinical Interview, De-escalation, Stat) font appel à ces spécialistes selon les besoins :

- **Trouble de l'humeur** : Dépression, anxiété
- **Trouble psychotique** : Schizophrénie, troubles délirants
- **Trouble d'usage de substance** : Dépendances
- **Troubles de la personnalité** : BPD, narcissisme, etc.
- **Troubles anxieux** : Anxiété généralisée, phobies, panique
- **Troubles obsessionnels-compulsifs** : TOC
- **Troubles dépressifs** : Dépression majeure, dysthymie
- **Nutritionniste** : Conseils nutritionnels adaptés à la santé mentale
- **Travailleur social** : Ressources sociales, logement, bénéfices
- **Intervenant communautaire** : Ressources communautaires, intégration sociale
- **Psychiatre** : Évaluation psychiatrique, médication
- **Psychologue** : Évaluation psychologique, thérapie
- **Ergothérapeute** : Évaluation fonctionnelle, routines, activités de la vie quotidienne
- **Infirmier** : Soins infirmiers, suivi médical

**Note** : Entraînés avec rapports de psychologue et ergothérapeute, façon d'agir, évaluation, questionnaire complet d'un psychologue.

#### Sources de données pour l'entraînement

**Bases de données identifiées (Juan)** :

🧠 **Counseling & Dialogue Datasets** :

- MentalChat16K, HuggingFace Mental Health Counseling Datasets, PsyDial, CounseLLMe, MedDialog, NutriBench

🧪 **Synthetic & Augmented Data** :

- GPT-generated therapist–patient dialogs, Synthetic Q&A and clinical vignettes, Synthetic ADL coaching scenarios, Public therapist Q&A, Psychoeducation guides rewritten as Q&A/dialog, Recovery support dialogs

📖 **Manuals & Professional Guides** :

- CBT guides/worksheets, DBT training materials, ERP manuals, Psychiatric emergency guidelines, Psychiatric treatment guidelines (APA), Nutrition counseling and psychoeducation, Government/NGO resource guides

📚 **Expert-Curated & Case-Based Sources** :

- Case studies (psychology, psychiatry, OT), Online psychiatrist Q&A (ChatPsychiatrist-style), Therapist/clinician session transcripts, Dietitian FAQs and session transcripts, Community health worker case studies, Real psychotherapy and emotional support transcripts

**Note** : Ces bases de données sont pour montrer COMMENT on entraînerait les modèles, pas pour un MVP fonctionnel.

### Technologies confirmées

- **Framework d'agents** : CrewAI (collaboration multi-agents, consensus)
- **LLM** : Groq API (rapide, free tier) ou Ollama (local)
- **Vector DB** : Chroma (local, gratuit)
- **Frontend** : React + Tailwind CSS
- **Innovation** : Agents qui interagissent entre eux pour réponse fact-checked et consensus

### Architecture Multi-Agents Collaboratifs (Inspirée de l'article WSI-Agents)

- **Agent Orchestrateur** : Coordonne et route les requêtes vers les agents spécialisés
- **Communication inter-agents** : Les agents se consultent entre eux pour des réponses plus complètes
- **Fusion multi-modale** : Combine texte (observations) + contexte régional + statistiques
- **Consensus entre agents** : Calcul d'accord entre plusieurs agents pour des décisions robustes

### Attentes du Hackathon (Mise à jour)

**Niveau d'attente** : Les bases de données sont fournies à titre indicatif. On ne s'attend pas à des analyses poussées — si vous en êtes capables, tant mieux.

**Objectif principal** : Réfléchir ensemble à un problème et à une solution potentielle. Co-créer une solution ou innovation en santé répondant aux critères du RSN.

**Évaluation** : Votre projet sera évalué, mais aussi votre capacité à le présenter et à le défendre.

**Avancement requis** : Il n'est pas obligatoire d'être très avancé dans les analyses. Il n'est même pas nécessaire de travailler sur une base de données spécifique.

### Prochaines étapes

1. ✅ Structurer le pitch (3 minutes) - En cours
2. ✅ Clarifier l'aspect scientifique et analytique (Juan) - Fait
3. ✅ Trouver exemples concrets avec CANPATH (PL) - Fait avec statistiques Québec
4. Ajouter aspects cybersécurité et finance (Cathicia, PL)
5. Trouver une phrase/citation/statistique catchy comme 1re slide
6. Choisir un nom final (AgentCareAI - à valider)
7. Penser au timeline (3-5 ans)

## 📝 Notes

- Présentation finale : 3 minutes
- Focus sur l'impact et la captation de l'audience
- **Nom du projet** : AgentCareAI (à valider)
- **Approche** : Présenter le projet comme une solution que nous développerons réellement après le hackathon et qui aura un impact concret dans la vie des gens

## 🎯 Éléments Essentiels de la Présentation

1. **Problème** : Définition claire
2. **Exemple concret** : Toucher (créer émotion) l'audience avec une situation réelle illustrant le problème
3. **Solution** : Résumé rapide et clair
4. **Modèle** : Description du modèle, de l'architecture et de la méthode
5. **Métriques d'évaluation** : Comment démontrer concrètement que la solution est efficace
6. **Analyse statistique** : Inclure des éléments comme la p-value pour montrer la rigueur
7. **Financement** : Institutions ou organisations potentielles pour soutenir le projet
8. **Sensibilisation et diffusion** : Idées pour encourager l'adoption (podcast, outreach, événements, etc.)
9. **Timeline** : Plan de déploiement sur 3 à 5 ans

## 📚 Documentation Détaillée

- **Structure du pitch** : `presentation/Structure_Pitch.md`
- **Détails d'entraînement des modèles** : `documentation/10_Entrainement_Modeles_Agents.md` (à créer)
- **Tâches Rayyan** : `analyse_rayyan/Taches_Rayyan.md`
