# Structure du Pitch Final - CareCircle

## ⏱️ Durée & Format

- **3 minutes** de présentation + **2 minutes** de questions (jury)
- **1-2 orateur·rices**
- **5-6 diapositives max** (hors annexes)
- **Plan B démo** : Préparer des captures statiques si besoin

## ⚠️ Clarifications Importantes (Feedback Mentor)

### Ce qui N'EST PAS attendu
- ❌ **Pas besoin d'un prototype complet** en 48h
- ❌ **Pas besoin d'un MVP fonctionnel** nécessairement
- ❌ **Pas besoin d'une démo technique** complète

### Ce qui EST attendu
- ✅ **Démontrer l'idée** : Expliquer clairement le concept
- ✅ **Montrer comment on la ferait** : Architecture, approche technique
- ✅ **Défendre l'idée** : Preuves concrètes de la nécessité
- ✅ **Valider avec utilisateurs potentiels** : Feedback de professionnels en santé mentale
- ✅ **Preuves concrètes** : Données, statistiques, témoignages

### Stratégie de Validation
- **Idée de Mouni** : Demander à des collègues en santé mentale leur avis
- **Impact** : Montrer qu'on a validé avec des professionnels du domaine
- **Argument fort** : "Nous avons consulté X professionnels qui confirment le besoin"

---

## 📊 Structure Suggerée (5-6 slides)

### Slide 1 : Accroche & Problème
**Pour qui, quoi, pourquoi maintenant ?**

**Accroche (phrase/citation/statistique catchy)** : À trouver - pour marquer les gens dès le début

**Image d'impact au début** : Un jeune avec la jambe cassée et on demande quel est son problème ? Puis un jeune sans rien de particulier et on demande quel est son problème ? Les problèmes de santé mentale ne sont pas faciles à déceler, encore moins à accompagner !

**Problème** : 
- Les problèmes de santé mentales cachent souvent : Troubles alimentaires, Troubles émotionnels, anxiété, dépression, des troubles du comportement, automutilation, consommations, isolement (mettre des photos qui suscite l'émotion)

**Contexte** :
- Dans nos secondaires, plus d'1 jeune sur 10 souffre d'une santé mentale languissante. Ce taux a pratiquement doublé entre 2016 et 2022. (mettre un graphique).
- Lorsque les troubles mentaux ne sont pas pris en charge à l'adolescence, les conséquences se font sentir jusqu'à l'âge adulte! Importance ++ du dépistage et de l'intervention précoce (a bcp d'impact sur le pronostic)
- Baisse d'intervenants sociaux pour soutenir les jeunes (entre 2016 et 2022).
- Nécessité de connaissances transversales dans la prise en charge de la santé mentale.
- Les intervenants de première ligne scolaires non formés à la prise en charge en santé mentale se retrouvent démunis face à un besoin croissant.
- Les intervenants décrivent un besoin de plus de connaissances pour appuyer leur pratique.
- Existence d'inégalités au sein des intervenants de première ligne à accéder à des expertises en lien avec la santé mentale (pour des raisons géographiques par exemple).

**Exemple concret émotionnel** : 
  > "Marie, infirmière scolaire à Rouyn-Noranda, remarque qu'un élève de 14 ans semble déprimé. Elle veut l'aider mais ne sait pas comment évaluer la situation. Les ressources spécialisées sont à 200km. Elle se sent dépassée."

**Durée** : 30-40 secondes

---

### Slide 2 : Données & Approche
**Sources, variables clés, pipeline simple**

**Contenu suggéré :**
- **Données utilisées** :
  - CANPATH : Statistiques régionales, santé mentale, environnement
  - MDClone : Patterns de visites aux urgences, vagues de chaleur
  - POYM : Facteurs de risque, comorbidités psychiatriques
- **Variables clés** :
  - CANPATH : Sommeil (`SLE_*`), alcool (`ALC_*`), défavorisation (`MSD_*`), pollution
  - MDClone : Visites aux urgences, diagnostics, trajectoires de soins
  - POYM : Diagnostics psychiatriques, comorbidités
- **Pipeline simple** :
  ```
  Observations → Agents Spécialisés → Collaboration → Consensus → Réponse
  ```

**Durée** : 30-40 secondes

---

### Slide 3 : Solution & Approche Technique
**1-2 figures lisibles + comment on la ferait**

**Solution (proposition de valeur)** :
- Offrir un accompagnement aux intervenants de première ligne grâce à une solution basée sur l'IA qui permettrait d'augmenter l'accessibilité à des connaissances d'expertise, plus rapidement et adaptées à la réalité du terrain afin d'augmenter la capacité d'agir des intervenants.

**Présentation de AgentCareAI** :
- Un agent principal avec qui communiquer (un canal unique pour faciliter l'utilisation)
- Des agents d'expertise (gérés par l'agent principal)
- 6 agents spécialisés :
  1. **Red Flag Agent** : Aide déterminer si l'intervenant devrait faire recours à une autorité de santé supérieure
  2. **Coaching Agent** : Aide l'intervenant traiter le patient (anxiété, nutrition, relations, exercice)
  3. **Clinical Interview Agent** : Aide l'intervenant qui ne sait pas quoi demander au patient
  4. **De-escalation Agent** : Gère les crises (attaques de panique)
  5. **Stat Agent** : Fournit stats régionales rapides
  6. **Global Impact Agent** : Outil qui sauvegarde interactions pour analyse régionale

**Model Zoo (Spécialistes)** : Les agents font appel à des sous-modèles spécialisés :
- Troubles (humeur, psychotique, substance, personnalité, anxieux, TOC, dépressifs)
- Professionnels (Nutritionniste, Travailleur social, Intervenant communautaire, Psychiatre, Psychologue, Ergothérapeute, Infirmier)

**Figure 1** : Diagramme de collaboration entre agents (architecture)
**Figure 2** : Exemple visuel de réponse consolidée (mockup/diagramme)
**Stack technique** : CrewAI, Groq API, Chroma, React

**Interprétation** : "Un collègue expert virtuel disponible 24/7 qui combine l'expertise de plusieurs spécialistes en temps réel"

**Note** : Pas besoin de démo fonctionnelle, juste montrer l'architecture et le concept

**Durée** : 45-60 secondes

---

### Slide 4 : Limites & Éthique/EDI
**Biais, qualité des données, ce que ça ne dit pas**

**Contenu suggéré :**
- **Limites** :
  - Données synthétiques (pas de données réelles confidentielles)
  - Prototype pour hackathon (validation avec experts nécessaire)
  - Pas de remplacement des professionnels, outil d'aide à la décision
  - Études existantes (ex: MH-TIPS) ont des limites de généralisation
  - Recherche future nécessaire pour évaluer faisabilité et acceptabilité
- **Éthique** :
  - Pas de stockage de données personnelles
  - Transparence sur le fonctionnement des agents
  - Respect de la confidentialité
- **Biais potentiels** :
  - Données CANPATH peuvent avoir des biais régionaux
  - Modèles LLM peuvent avoir des biais culturels/linguistiques
  - Nécessite validation avec experts diversifiés
- **Positionnement** :
  - Solution complémentaire (pas remplacement de formation continue)
  - CareCircle n'existe pas encore, offre alternative innovante

**Durée** : 30-40 secondes

---

### Slide 5 : Métriques d'Évaluation & Impact
**Preuves concrètes + qui s'en sert demain**

**Métriques d'évaluation** : Comment démontrer concrètement que la solution est efficace
- **Analyse statistique** : Inclure des éléments comme la p-value pour montrer la rigueur
- **Indicateurs de succès** :
  - Au niveau des jeunes : augmenter le soutien perçu des intervenants → indicateurs « soutien social à l'école » qui mesure entre autres : les services de prévention et d'intervention précoce des intervenants en milieu scolaire
  - Indicateurs de bien-être des intervenants de première ligne en santé mentale (confiance en ses compétences, impression de soutien)
  - À plus long terme : diminution des hospitalisations de jeunes dans la région pour des problématiques de santé mentale (car on les prend en charge avant qu'ils ne soient décompensés et qu'ils doivent être hospitalisés)

**Impact** :
- **Court terme** → réduction du stress décisionnel
- **Intermédiaire** → amélioration de la santé mentale
- **Long terme** → génération de données anonymisées

**Validation avec utilisateurs potentiels** :
  - ✅ Consultation avec X professionnels en santé mentale
  - ✅ Feedback confirmant le besoin et la pertinence
  - ✅ "Nous avons validé avec des intervenants de première ligne qui confirment la nécessité"

**Preuves concrètes** :
  - Données CANPATH/MDClone montrant les inégalités
  - Statistiques sur le manque de ressources en région
  - Témoignages de professionnels consultés

**Durée** : 40-50 secondes

---

### Slide 6 : Financement, Timeline & Call to Action
**Vision et impact final**

**Financement** : Institutions ou organisations potentielles pour soutenir le projet
- FRQS, CIHR, MSSS
- Partenaires : Ordres professionnels, CISSS/CIUSSS, Centres de santé communautaire
- Incubateurs : ÉlanTech, Millenium Québecor, Experience Ventures

**Sensibilisation et diffusion** : Idées pour encourager l'adoption
- Podcast, outreach, événements
- Conférences RSN, congrès de santé publique
- Publications dans revues de santé publique
- Partenariats avec ordres professionnels

**Timeline** : Plan de déploiement sur 3 à 5 ans
- Année 1 : Développement prototype, validation avec experts
- Année 2 : Tests pilotes dans 2-3 régions
- Année 3 : Déploiement progressif
- Années 4-5 : Expansion et amélioration continue

**Slide de fin** :
> AgentCareAI vise à redonner du pouvoir, du soutien, et du temps aux intervenants de premières lignes :
> 
> Pour qu'un jeune qui souffre en silence ne passe plus inaperçu.
> 
> Pour que l'expertise soit accessible, partout, tout le temps.
> 
> Pour qu'ensemble, nous changions durablement le parcours de santé mentale des jeunes.

**Durée** : 30-40 secondes

---

## 🎯 Points Clés à Retenir

### Pour le Jury
1. **Impact et pertinence** : Problème réel, 50,000+ personnes visées, **validé avec professionnels**
2. **Originalité** : Système multi-agents collaboratifs (pas juste un chatbot)
3. **Faisabilité** : Stack technique confirmé, architecture claire
4. **Validation** : **Preuve concrète** qu'on a consulté des utilisateurs potentiels

### Pour la Présentation
- **Parler avec passion** : Le problème est réel et émotionnel
- **Montrer la validation** : "Nous avons consulté X professionnels qui confirment..."
- **Montrer l'architecture** : Diagramme de collaboration entre agents (pas besoin de démo)
- **Preuves concrètes** : Données, statistiques, témoignages de professionnels
- **Être transparent** : Mentionner les limites et l'éthique
- **Défendre l'idée** : Pourquoi c'est nécessaire, pas juste comment ça marche

---

## 📝 Checklist Avant le Pitch

- [ ] Slides créées (5-6 max)
- [ ] Timing testé (3 minutes exactement)
- [ ] Exemples concrets préparés
- [ ] Figures/diagrammes clairs et lisibles
- [ ] Plan B : Captures d'écran statiques si démo échoue
- [ ] Questions anticipées préparées
- [ ] Répétition avec l'équipe

---

## 💡 Conseils

1. **Démarrer fort** : Exemple émotionnel pour captiver l'audience
2. **Visualiser** : Diagrammes de collaboration entre agents
3. **Être honnête** : Mentionner les limites et l'éthique
4. **Avoir une vision claire** : Prochaines étapes réalistes
5. **Pratiquer** : Répéter plusieurs fois pour être à l'aise

---

## 📚 Références

- **Template fourni par Tess** : `Hackathon_RSN_Pitch_Template (1).pdf` (dans ce dossier)
- **Documentation complète** : `documentation/09_Idees_Projet_Agent_IA.md`
- **Design dashboard** : `documentation/13_Dashboard_Design_UI.md`

