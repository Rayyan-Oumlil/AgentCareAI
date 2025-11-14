# Détails d'Entraînement des Modèles Spécialisés - AgentCareAI

## 🎯 Vue d'Ensemble

Ce document décrit en détail comment chaque modèle spécialisé du **Model Zoo** sera entraîné pour AgentCareAI. Les agents intermédiaires (Red Flag, Coaching, Clinical Interview, De-escalation, Stat) font appel à ces spécialistes selon les besoins.

## 🏗️ Architecture d'Entraînement

### Rôle de l'Agent Principal (Front Man Agent)

1. **Input triage (sentiment classification)** : Choisit quel agent intermédiaire devrait gérer le cas
2. **Délègue la requête** : Passe la demande à l'agent approprié (ex: Red Flag, Coaching)
3. **Collecte la sortie** :
   - Agent intermédiaire
   - Modèle(s) spécialiste(s)
4. **Résume la réponse finale** : Produit un rapport ou message de guidance clair et convivial pour l'intervenant de première ligne

### Rôle des Agents Intermédiaires

Les agents intermédiaires adressent des besoins spécifiques de la personne menant une intervention.

**Stratégie simple (conceptuelle)** : Chaque agent suit ce processus interne en 3 étapes :

1. **Comprendre la Situation** : Regarde les informations entrantes et détermine "Quel type de problème est-ce ?"
2. **Faire correspondre aux Types de Problèmes** : A une petite carte interne (comme une liste de règles ou un mini-classifieur) qui dit :
   - "Pour l'anxiété, consulter le Psychologue et le Nutritionniste"
   - "Pour panique aiguë, consulter le Crisis Worker et le Community Worker"
3. **Appeler les Bons Modèles** : Envoie la situation aux modèles choisis (experts du zoo) et collecte leurs réponses

### Exemples de Routage

| Input de l'utilisateur (intervenant) | Agent | Expert Cible |
|--------------------------------------|-------|--------------|
| "Le patient dit qu'il veut disparaître pour toujours…" | Red Flag Agent | Psychiatre |
| "Elle hyperventile, que puis-je dire pour la calmer ?" | De-escalation Agent | Modèle de dé-escalation |
| "Je ne sais pas quoi d'autre lui demander…" | Clinical Interview Agent | Modèle de guide d'entretien |
| "Elle est stressée et dort mal — que peut-elle faire ?" | Coaching Agent | Coach sommeil ou Nutritionniste |
| "Combien de cas de dépression ont été rapportés à Laval ?" | Stat Agent | Base de données statistiques régionales |

---

## 🧠 Modèles Spécialisés - Détails d'Entraînement

### 1. Mood Disorders Expert (Troubles de l'Humeur)

**Modèle** : LLaMA-2 7B (finetuned with QLoRA)

**Données** :
- Mental Health Counseling Conversations (conversations liées à la dépression)
- MentalChat16K (dialogs dépression + deuil)
- Extraits de guides CBT + matériaux de support bipolaire réécrits comme dialogue/Q&A

**Entraînement** :
- Supervised fine-tuning sur tous les dialogs liés à l'humeur
- Enseigner : empathie, stratégies d'adaptation, activation comportementale, gestion de routine
- Enseigner questions de suivi (durée, fréquence, déclencheurs)
- **Jamais diagnostiquer** ; seulement soutenir et guider
- Évaluation sur scénarios synthétiques de dépression/bipolaire pour vérifier sécurité + qualité

---

### 2. Psychotic Disorders Expert (Troubles Psychotiques)

**Modèle** : LLaMA-2 7B (finetuned with QLoRA)

**Données** :
- Dialogs synthétiques thérapeute-patient psychose (générés depuis un modèle plus fort, comme GPT-4, suivant prompts contrôlés)
- Scripts de counseling synthétiques style MentalChat pour hallucinations, délires, paranoïa
- Textes de psychoéducation sur gestion hallucinations, grounding, signes d'avertissement de rechute (réécrits comme Q&A/dialog)
- Guidelines d'urgence psychiatrique (étapes de sécurité psychose aiguë)
- Optionnel : extraits anonymisés d'études de cas + Q&A psychiatre en ligne sur psychose

**Entraînement** :
- Supervised fine-tuning sur Q&A synthétiques + curés
- Enseigner réponses calmes, grounding, validation, reality-testing doux, non-confrontation
- **Pas de diagnostic** ; seulement soutien + guidance sécurité
- Enseigner détection red-flag (hallucinations de commande, délires dangereux → déclencher Red Flag agent)
- Étape de raffinement optionnelle : RL depuis feedback IA/humain pour renforcer empathie + sécurité
- Évaluation sur scénarios synthétiques de psychose pour s'assurer ton correct, grounding, comportement d'escalade

---

### 3. Substance Use Disorders Expert (Troubles d'Usage de Substance)

**Modèle** : LLaMA-2 7B with QLoRA finetuning

**Données** :
- Dialogs de Support de Récupération Générés (~1100 conversations de counseling d'addiction alignées MI ; étapes de changement, cravings, déclencheurs, rechute)
- Optionnel : transcripts anonymisés de counseling d'addiction, extraits narratifs AA/NA réécrits comme dialog, Q&A santé publique (effets substances, recherche traitement)

**Entraînement** :
- Supervised finetuning sur dialogs style MI (empathie, non-jugement, écoute réflexive, affirmations, exploration ambivalence)
- Enseigner compétences : "rolling with resistance," évoquer raisons propres de l'utilisateur pour changement, soutenir auto-efficacité, suggestions compétences d'adaptation, étapes prévention rechute
- **Pas de jugement, pas de confrontation** ; ton strictement motivationnel
- Évaluation sur scénarios d'addiction non vus ; raffiner avec RLHF si nécessaire (récompenser réponses supportives, cohérentes MI)
- Sortie doit rester sûre : encourager groupes de soutien, ressources traitement, stratégies d'adaptation ; jamais fournir guidance illégale ou nuisible

---

### 4. Personality Disorders Expert (Troubles de la Personnalité)

**Modèle** : LLaMA-2 7B with QLoRA finetuning

**Données** :
- Transcripts d'entraînement DBT / role-plays (régulation émotion, tolérance détresse, efficacité interpersonnelle)
- Datasets de counseling généraux filtrés pour thèmes comme peur abandon, colère, relations instables, problèmes identité
- Dialogs synthétiques simulant crises style BPD, sensibilité narcissique, impulsivité, etc., générés avec règles (validation + compétences, pas d'étiquetage)
- Q&A réécrits depuis guides psychoéducationnels (compétences DBT, bases thérapie schémas, gestion relations)
- Résumés d'études de cas convertis en dialog décrivant interactions typiques

**Entraînement** :
- Supervised finetuning sur réponses validation-first et coaching compétences (mindfulness DBT, grounding, tolérance détresse, remise en question pensées CBT)
- Enseigner patterns :
  - "Je t'entends…" validation
  - Coping de crise avant analyse
  - Désescalade émotion intense
  - **Pas de diagnostic, pas de stigmatisation**
- Inclure scénarios pour comportements multiples liés PD : impulsivité, épisodes rage, vide, instabilité relationnelle, guidance prise perspective
- Tester sur vignettes cliniques ; raffiner si ton devient jugeant
- RLHF optionnel : récompenser réponses calmes, validantes, cohérentes DBT ; pénaliser étiquetage ou confrontation

---

### 5. Anxiety Disorders Expert (Troubles Anxieux)

**Modèle** : LLaMA-2 7B + QLoRA adapters

**Données** :
- MentalChat16K dialogs anxiété + stress counseling
- Scripts intervention attaque panique (respiration guidée, grounding, désescalade menée thérapeute)
- Q&A thérapeute public sur inquiétude, panique, phobies (converti en dialog)
- Textes CBT/self-help réécrits comme Q&A (cycles inquiétude, distorsions cognitives, étapes exposition)
- Scénarios anxiété multi-tours synthétiques (épisodes panique, anxiété anticipatoire, inquiétude nocturne)

**Entraînement** :
- Supervised fine-tuning sur tous dialogs liés anxiété
- Enseigner techniques soulagement aigu : respiration rythmée, grounding (5-4-3-2-1), relaxation musculaire
- Enseigner compétences CBT long terme : reframing cognitif, questionnement socratique, étapes exposition, planification inquiétude
- Entraînement ton : calme, stable, rassurant, structuré
- Curriculum : commencer avec QA sur symptômes/coping, puis entraîner sur séquences panique multi-tours
- Règles sécurité : pas de claims médicaux, pas de diagnostic ; coaching seulement
- Évaluation sur épisodes panique simulés — s'assurer désescalade étape-par-étape correcte et gestion inquiétude style CBT correcte ; raffiner avec exemples ciblés si nécessaire

---

### 6. OCD Expert (Troubles Obsessionnels-Compulsifs)

**Modèle** : LLaMA-2 7B + QLoRA adapters

**Données** :
- Manuels ERP (Exposure & Response Prevention) convertis en forme dialog (coach → client)
- Dialogs TOC synthétiques (contamination, vérification, pensées intrusives, symétrie, obsessions de mal)
- Datasets counseling filtrés contenant conversations pensées obsessionnelles
- FAQs psychoéducationnels (explications style International OCD Foundation de TOC, ERP, tolérance incertitude)
- Prompts style étude de cas réécrits comme Q&A montrant étapes ERP et réponses non-rassurantes

**Entraînement** :
- Supervised fine-tuning sur tous dialogs focalisés ERP
- Enseigner :
  - Validation non-jugeante pensées intrusives
  - Règle zéro-rassurance (pas de rassurance compulsive)
  - Coaching exposition graduée (retarder, réduire, résister compulsions)
  - Tolérance détresse pendant exposition (surfer vague anxiété)
- Entraîner utilisant format role-play : utilisateur exprime obsession/urge → modèle fournit coaching cohérent ERP
- Règles sécurité : jamais encourager compulsions ; pas de diagnostic ; reality-testing doux seulement
- RL optionnel (récompense basée règles) : réponses alignées étapes ERP obtiennent signal positif
- Évaluation sur scénarios TOC synthétiques (contamination, vérification, pensées intrusives de mal) pour s'assurer comportements style ERP corrects ; raffiner si nécessaire

---

### 7. Depression Expert (Troubles Dépressifs)

**Modèle** : LLaMA-2 7B + QLoRA adapters

**Données** :
- MentalChat16K dialogs spécifiques dépression (empathie, désespoir, faible motivation, deuil)
- Dialogs counseling réels (datasets HuggingFace mental-health counseling) filtrés pour thèmes dépression
- Q&A spécifiques dépression depuis sources psychoéducationnelles ("sortir du lit," "perte motivation," "self-care")
- Guides Activation Comportementale réécrits comme dialog/extraits
- Prompts risque suicide : questions C-SSRS réécrites conversationnellement + templates réponses sûres (PAS diagnostic, OUI escalade)

**Entraînement** :
- Supervised fine-tuning sur tous dialogs focalisés dépression
- Enseigner compétences core :
  - Empathie profonde + validation
  - Activation comportementale petits pas (micro-tâches)
  - Reframing cognitif doux
  - Poser questions de suivi sur durée, intensité, altération (style entretien)
- Comportement suicide-safe : modèle entraîné répondre avec grounding, safety-checking, compassion, et déclencheurs escalade immédiate (handoff à Red Flag agent)
- Pondération coût-sensible : récompenser réponses sûres, supportives ; pénaliser sorties dismissives ou nuisibles
- Évaluation : scénarios dépression non vus (faible motivation, désespoir, SI passif, SI actif) pour confirmer empathie, sécurité, logique escalade correcte

---

### 8. Nutritionist Expert (Nutritionniste)

**Modèle** : LLaMA-2 7B + QLoRA adapters

**Données** :
- NutriBench (descriptions repas + info nutriments) → supporte connaissance factuelle (macros, calories, ingrédients)
- Q&A counseling nutrition depuis sources réputables (FAQs diététiste, "combien protéine?", "collations saines?", "prise poids médications")
- Transcripts sessions diététiste (si disponible) pour style dialog
- Dialogs synthétiques construits depuis guidelines officiels (planification repas, cuisine basse énergie, tips alimentation émotionnelle)

**Entraînement** :
- Supervised fine-tuning sur tous Q&A nutrition et dialogs style counseling
- Enseigner comportements core :
  - Recommandations basées preuves (repas équilibrés, hydratation, micronutriments)
  - Contexte santé mentale (énergie, perte appétit, changements poids liés médications)
  - Suggestions repas/collations très simples ; étape-par-étape, bas effort
  - Ton motivational interviewing (encourageant, non-jugeant, "petits pas")
- Entraînement limites : escalader problèmes sérieux (trouble alimentaire possible, malnutrition sévère)
- Optionnel : CoT finetuning sur tâches estimation nutriments
- Évaluation : problèmes nutrition non vus (faible appétit, repas budget, alimentation supportant humeur) vérifiés contre guidelines nutritionnels standards

---

### 9. Social Worker Expert (Travailleur Social)

**Modèle** : LLaMA-2 7B + QLoRA adapters

**Données** :
- Dataset Q&A construit depuis scénarios services sociaux réels (perte logement, chômage, insécurité alimentaire, conflit familial, bénéfices, refuges, voies aide légale)
- Transcripts counseling / role-plays domain public depuis entraînement travail social (écoute active, empowerment)
- Guides ressources gouvernement/NGO (assistance logement, soutien revenu, programmes communautaires), réécrits comme dialog
- Exemples multi-région pour enseigner patterns généralisables (ex: "contacter municipalité/centre communautaire local")

**Entraînement** :
- Supervised fine-tuning sur dialogs résolution problèmes étape-par-étape
- Enseigner comportements core :
  - Mix empathie + actions concrètes (bénéfices, refuges, banques alimentaires, programmes communautaires)
  - Limites claires (pas conseil légal → recommander aide légale ; pas conseil médical → différer)
  - Style empowerment (identifier forces, options, prochaines étapes)
- Entraîner produire guidance agnostique région, avec option pour Stat Agent injecter données locales plus tard
- Mises à jour périodiques dataset (ressources sociales changent)
- Évaluation sur scénarios non vus (crise logement, difficulté financière, navigation services) pour s'assurer guidance pratique, sûre, et compassionnelle

---

### 10. Community Worker Expert (Intervenant Communautaire)

**Modèle** : LLaMA-2 7B + QLoRA

**Données** :
- Chevauchement avec dataset Travailleur Social (logement, bénéfices, ressources soutien)
- Scénarios spécifiques communautaires : groupes soutien, outreach jeunesse, solitude, stigmatisation culturelle/communautaire, navigation soutien par pairs
- Répertoires ressources communautaires réécrits comme dialog (bibliothèques, centres communautaires, clubs, événements locaux, groupes religieux)
- Études de cas travailleurs santé communautaires (engagement grassroots, conversations outreach)

**Entraînement** :
- Supervised fine-tuning sur conversations proactives, orientées ressources
- Enseigner comportements core :
  - Encourager intégration communautaire (clubs, événements, groupes pairs)
  - Offrir aider trouver ressources, pas juste les lister
  - Utiliser langage compétent culturellement et conscience normes communautaires
- Maintenir chevauchement avec modèle Travailleur Social mais accordé vers appartenance communautaire, soutien par pairs, et connexion sociale
- Évaluation sur cas non vus (solitude, barrières culturelles, réintégration communautaire)
- Mises à jour périodiques utilisant logs interactions réelles pour raffiner besoins communautaires communs

---

### 11. Psychiatrist Expert (Psychiatre)

**Modèle** : LLaMA-2 7B + QLoRA adapters

**Données** :
- MedDialog (anglais, ~257k dialogs docteur-patient) → filtrer vers psychiatrie, questions médication, discussions symptômes
- Guidelines psychiatriques & FAQs (résumés traitement APA dépression/schizophrénie, psychoéducation sur médications)
- Q&A style ChatPsychiatrist (Q&A consultation psychiatrique publique, explications médications)
- Q&A spécifiques médication : SSRIs, SNRIs, antipsychotiques, effets secondaires, timelines, risques, interactions

**Entraînement** :
- Supervised fine-tuning sur MedDialog filtré + Q&A psychiatrique curés
- Enseigner comportement :
  - Expliquer médications (ce qu'elles font, combien temps prennent, effets secondaires communs)
  - Fournir guidance mais pas diagnostic ou prescriptions
  - Suggérer quand évaluation psychiatrique en personne nécessaire
  - Reconnaître red flags (hallucinations de commande, manie sévère, intent suicidaire → escalader)
  - Maintenir ton autoritaire mais empathique
- Inclure exemples où psychiatre diffère vers thérapie/soutien social quand approprié
- RLHF optionnel pour renforcer sécurité, clarté, phrasé non-prescriptif
- Évaluation sur questions médication non vues et scénarios symptômes sévères ; mettre à jour périodiquement avec guidance médicale la plus récente

---

### 12. Psychologist Expert (Psychologue)

**Modèle** : LLaMA-2 13B + QLoRA adapters (besoin nuance + empathie long format)

**Données** :
- Transcripts thérapie (sessions psychothérapie réelles : réflexions, traitement émotionnel, interactions CBT/DBT)
- Q&A counseling santé mentale (dataset HuggingFace mental-health-counseling → réponses thérapeute baseline)
- Sets counseling simulés (PsyDial, CounseLLMe → scénarios divers, cas émotionnels multilingues)
- Scripts techniques (exercices pleine conscience, scripts grounding, prompts compétences CBT, prompts compétences DBT)

**Entraînement** :
- SFT (supervised fine-tuning) sur dialogs style thérapeute :
  - Questions ouvertes
  - Réflexion émotion
  - Validation + normalisation
  - Compétences coping collaboratives
- Fine-tuning deux étapes :
  1. Datasets counseling larges → style thérapeute global
  2. Données focalisées CBT/DBT/pleine conscience → techniques ciblées
- Enseigner limites : soutien émotionnel seulement ; rediriger problèmes pratiques/médicaux vers autres spécialistes
- Inclure exemples où thérapeute passe la main ("Un travailleur social peut aider avec la partie financière pendant que je te soutiens émotionnellement")
- RLHF optionnel : cliniciens notent empathie, écoute, rythme → raffiner ton + profondeur
- Évaluation sur métriques thérapie (empathie, validation, rythme conversationnel). Objectif : thérapeute virtuel stable, chaleureux, réfléchi pour traitement émotionnel général

---

### 13. Occupational Therapist (OT) Expert (Ergothérapeute)

**Modèle** : LLaMA-2 7B ou 13B + QLoRA adapters

**Données** :
- Guides OT + études de cas réécrits en dialog/Q&A (routines matin, coaching AVQ, activités grounding, décomposition tâches)
- Scénarios AVQ synthétiques (nettoyage, soins personnels, luttes fonction exécutive, conservation énergie, accommodements travail/école)
- Dialogs réadaptation/réadaptation professionnelle (ex: planificateurs, gestion temps, réadaptation cognitive pour clients santé mentale)

**Entraînement** :
- SFT sur dialogs style OT construits : coaching tâches étape-par-étape, structurer routines, petits objectifs, timers, encouragement doux
- Enseigner patterns résolution problèmes OT : décomposer tâches en micro-étapes, planifier activités, utiliser stratégies sensorielles/grounding (modèle PEOP)
- Entraîner gestion limites : pas conseil médical, pas réadaptation blessure physique → rediriger vers infirmier/psychiatre/OT physique quand nécessaire
- Inclure exemples ton collaboratif ("Choisissons ensemble une toute petite étape…")
- Évaluation sur tâches AVQ, scénarios construction routine, cas faible motivation, planification hygiène sommeil. Le modèle réussit quand il donne guidance quotidienne concrète, faisable, motivationnelle de manière cohérente

---

### 14. Nurse Expert (Infirmier)

**Modèle** : LLaMA-2 7B/13B + QLoRA adapters

**Données** :
- MedDialog (filtré vers conseils simples, suivis, vérifications symptômes)
- FAQs infirmières + brochures éducation patient (effets secondaires SSRIs, hygiène sommeil, bénéfices exercice, guides self-care)
- Protocoles triage réécrits en dialog (symptômes légers vs urgents, quand escalader)
- Scénarios vérification symptômes synthétiques ("1 semaine sur antidépresseur + vertiges", "nouvel effet secondaire", "problèmes sommeil")

**Entraînement** :
- SFT sur dialogs style infirmière : ton chaleureux, rassurant + instructions claires, sûres
- Enseigner patterns :
  - Expliquer effets secondaires communs
  - Suggérer self-care basique
  - Avertir symptômes sérieux → référer docteur/urgence
- Inclure coaching promotion santé (hygiène sommeil, hydratation, exercice, routine)
- Renforcer limites : pas prescrire ; encourager contacter docteur/pharmacien quand nécessaire
- Optionnel : retrieval grounding pour faits médication
- Évaluation sur triage symptômes et questions effets secondaires pour s'assurer précision + sécurité

---

## 🔍 Agents de Validation

### Logic Agent (Agent de Logique)

**But** : Vérifie si les réponses spécialistes font sens au niveau raisonnement (pas de contradiction, étapes suivent logiquement)

**Utilisation** : S'assure que le plan d'entretien ou étapes coaching suivent un flux cohérent

### Fact Agent (Agent de Faits)

**But** : Vérifie précision factuelle utilisant bases de données externes ou références médicales

**Utilisation** : Confirme que toute suggestion médicale ou référence est basée sur faits cliniques de confiance

### Consensus Agent (Agent de Consensus)

**But** : Compare réponses à travers plusieurs spécialistes pour trouver accord commun ou désaccords

**Utilisation** : Résume ce sur quoi la plupart des experts sont d'accord (ex: "3 modèles recommandent thérapie par la parole, 2 mentionnent médication — probablement thérapie est primaire")

---

## 📊 Stratégie d'Entraînement Globale

### Approche par Étapes

1. **Entraînement individuel** : Chaque modèle spécialisé entraîné séparément sur son domaine
2. **Validation experte** : Validation avec humains (experts validation)
3. **Retour au terrain** : Demander feedback des utilisateurs réels
4. **Amélioration continue** : Mises à jour périodiques basées sur logs interactions

### Sources de Données Principales

- **Datasets publics** : MentalChat16K, MedDialog, NutriBench, HuggingFace datasets
- **Données synthétiques** : Générées avec GPT-4 ou modèles similaires suivant prompts contrôlés
- **Manuels professionnels** : CBT, DBT, ERP, guidelines psychiatriques convertis en format dialog
- **Rapports professionnels** : Rapports psychologues et ergothérapeutes, questionnaires complets

### Fédération et Confidentialité

- **Federated learning** : Entraînement distribué pour préserver confidentialité
- **Dataset public pour entraînement** : Utilisation datasets publics pour entraînement initial
- **Anonymisation** : Toutes données personnelles anonymisées avant entraînement

---

## ⚠️ Limitations et Considérations

1. **Pas de diagnostic légal** : Les modèles ne diagnostiquent pas, ils guident seulement
2. **Validation humaine nécessaire** : Toutes suggestions doivent être validées par professionnels
3. **Biais potentiels** : Les modèles peuvent avoir des biais culturels/linguistiques nécessitant validation avec experts diversifiés
4. **Mises à jour continues** : Les guidelines médicales changent, nécessitant mises à jour périodiques
5. **Conformité réglementaire** : Respect des normes de santé et protection des données

---

## 📚 Références

- **Article inspiration** : `Article_WSI_Agents_MultiAgent_System.pdf`
- **Plan détaillé** : `documentation/04_Plan_Juan_Felipe.md`
- **Idées projet** : `documentation/09_Idees_Projet_Agent_IA.md`

