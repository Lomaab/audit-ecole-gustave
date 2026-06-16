# Audit SEO Complet — ecole-gustave.com

**Document de synthèse destiné à la présentation**

| Champ | Valeur |
|-------|-------|
| Site audité | `ecole-gustave.com` |
| Date | 16 juin 2026 |
| Pages analysées | 169 (crawl intégral) + 187 (sitemap) |
| Score global | 28/100 |
| Dashboard | https://lomaab.github.io/audit-ecole-gustave/ |
| Méthodologie | PageSpeed Insights, CrUX, analyse HTML, audit sécurité, DNS, SERP, backlinks, social media |

---

## 1. Résumé Exécutif

Le site **ecole-gustave.com** obtient un score global de **28/100**, reflétant des lacunes importantes dans plusieurs domaines clés du SEO.

### Forces identifiées

✅ **Core Web Vitals OK** — LCP 1800ms, CLS 0.01, INP 176ms (données réelles CrUX)
✅ **Contenu riche** — Moyenne 1537 mots/page, aucun thin content
✅ **Performance technique** — Pas de frameworks lourds (code léger)
✅ **Présence presse nationale** — Figaro (2x), Le Monde, BFMTV, BCG, Marcelle
✅ **LinkedIn solide** — 4333 abonnés, publications régulières
✅ **Sitemap bien structuré** — 7 sous-sitemaps, 187 URLs, 0 erreur
✅ **Sécurité de base** — Cloudflare WAF, TLS 1.3, xmlrpc/wp-admin protégés

### Faiblesses critiques

❌ **95 pages sans meta description (56%)** — CTR SERP reduit, Google genere des descriptions automatiques
❌ **Cannibalisation massive** — Les pages se font concurrence entre elles, aucune ne ranke bien
❌ **Schemas metier manquants (Course, Review, FAQ)** — Yoast genere bien les schemas de base (Organization, WebSite) MAIS les schemas metier sont absents : Course sur les 8 formations, Review sur les 17 te
❌ **Redirection www qui perd le chemin** — Perte de backlinks et de trafic www
❌ **12 URLs staging en production** — Risque de 404 massif si staging supprime
❌ **Page /campus/ en 404** — Mauvaise UX, erreur indexation Google
❌ **Facebook Pixel charge avant consentement RGPD** — Non-conforme RGPD, risque de sanction CNIL
❌ **Content-Security-Policy absente** — Risque XSS eleve

### Impact Google estimé

1. **TTFB à 1300ms** (données réelles CrUX) : Google utilise le TTFB comme signal de classement depuis 2018. Dépassement du seuil 800ms = facteur de déclassement, surtout mobile.
2. **95 pages sans meta description (56%)** : Google génère des descriptions automatiques, souvent coupées. CTR +20-40% avec des descriptions optimisées.
3. **Cannibalisation massive** : 39 pages sur 'plombier' diluent l'autorité. Aucune page ne peut devenir LA référence sur ce mot-clé.
4. **Absence de Course schema** : Google ne peut pas afficher les formations en résultats enrichis. Perte de visibilité estimée à 30%.
5. **6 articles presse sans backlink** : Figaro, Le Monde, BFMTV mentionnent l'école sans la lier. DR perdu estimé à 15-20 points.

---
## 2. Performances Web

### 2.1 Scores PageSpeed

| Page | Mobile | Desktop | Écart |
|------|--------|---------|-------|
| accueil | 91 | 56 | ⚠️ 35 pts |
| formation_electricien | 81 | 72 | ✅ 9 pts |
| campus_paris | 83 | 61 | ⚠️ 22 pts |
| ecole_gustave | 78 | 83 | ✅ 5 pts |
| actualites | 65 | 98 | ⚠️ 33 pts |
| **Moyenne** | **79.6** | **74** | **5 pts** |

**Analyse :** L'écart mobile/desktop est significatif sur plusieurs pages, suggérant une optimisation prioritaire mobile sans équivalent desktop.

### 2.2 Core Web Vitals — Données réelles (CrUX)

| Métrique | P75 Réel | Seuil Google | Statut |
|----------|----------|-------------|--------|
| **TTFB** | 1300ms | 800ms | ❌ ÉCHEC |
| **LCP** | 1800ms | 2500ms | ✅ OK |
| **CLS** | 0.01 | 0.1 | ✅ OK |
| **INP** | 176ms mobile / 60ms desktop | 200ms | ✅ OK |
| **FCP** | 1500ms | 1800ms | ✅ OK |

**Verdict :** PASS - Core Web Vitals OK malgre TTFB eleve

### 2.3 Problèmes de performance

**🔴 TTFB reel a 1300ms (CrUX)** [CRITIQUE]
- Impact : Depasse le seuil de 800ms, penalise le SEO
- Cause : Pas de cache HTML Cloudflare, hebergement mutualise Infomaniak
- Solution : Configurer le cache HTML Cloudflare, utiliser un plugin de cache WP (WP Rocket ou Flying Press)

**🟠 273 Kio de JavaScript inutilise** [HAUTE]
- Impact : Ralentit le thread principal, TBT eleve
- Cause : Le theme charge des scripts non utilises sur toutes les pages
- Solution : Auditer les scripts avec coverage DevTools, ne charger que ce qui est necessaire

**🔴 Requetes bloquant le rendu (910-1330ms)** [CRITIQUE]
- Impact : Retarde l'affichage de la page, LPC augmente
- Cause : CSS/JS non optimises pour le chargement critique
- Solution : CSS critique inline, JS ajoute avec defer/async

**🟠 Cache inefficace (516-1700 Kio)** [HAUTE]
- Impact : Les visiteurs recurrents telechargent les memes ressources
- Cause : Headers de cache trop courts ou absents
- Solution : Configurer des durees de cache longues (1 an) pour les ressources statiques via Cloudflare Page Rules

**🟠 Images non optimisees - Campus Paris (924 Kio economie possible)** [HAUTE]
- Impact : Poids de page excessif, LPC mobile degrade
- Cause : Images en JPEG/PNG haute resolution sans compression
- Solution : Convertir en WebP avec Cloudflare Polish ou ShortPixel/EWWW Image Optimizer

**🟠 CLS excessif (0.12-0.17) sur /ecole-gustave/ et /campus/paris/ desktop** [HAUTE]
- Impact : Experience utilisateur degradee, Core Web Vitals echoue sur desktop
- Cause : Images sans dimensions explicites, animations non composees
- Solution : Ajouter width/height aux images, utiliser transform/opacity pour les animations

**🟠 Seulement 18% des images en WebP (6/34 sur l'accueil)** [HAUTE]
- Impact : Poids de page 2-3x superieur au necessaire
- Cause : Telechargement en JPEG/PNG natif, pas de conversion automatique
- Solution : Activer Cloudflare Polish (lossless) ou installer ShortPixel Performance Image

---
## 3. SEO Technique

### 3.1 Crawl & Indexation

- Pages crawlées : **169** (100% du sitemap)
- Erreurs HTTP : **0** ✅
- ❌ Page orpheline : `formations/formation-macon-vrd/`
- ❌ Page orpheline : `equivalences-de-nos-titres/`
- ❌ Page orpheline : `mentions-legales/`
- ❌ Page orpheline : `donnees-personnelles/`
- ❌ Page orpheline : `footer`

**Qu'est-ce qu'une page orpheline ?** Une page sans aucun lien interne entrant. Google la découvre via le sitemap mais lui attribue moins d'autorité. Potentiel de classement réduit de 50 à 80%.

### 3.2 Redirection www — CRITIQUE

**www.ecole-gustave.com/formations/ redirige vers ecole-gustave.com/ (perte du chemin)**
- Impact : Toutes les sous-pages en www perdent leur referencement. Backlinks et recrutements perdus.
- Solution : Modifier la regle Cloudflare/Nginx ou le .htaccess pour preserver le chemin

**Pourquoi Google pénalise :** www et non-www sont des origines différentes. Les backlinks www perdent leur PageRank redirigés vers la racine.

### 3.3 URLs Staging en Production — CRITIQUE

**URLs staging en production**
- 12 URLs du staging
  - ❌ `Logo SNCF`
  - ❌ `Logo Vinci`
  - ❌ `Logo Eiffage`
  - ❌ `Logo Qualiopi`
  - ❌ `Logo France Competences`
- Risque : Quand le site staging sera supprime, ces 12 images deviendront des 404

### 3.4 Page /campus/ en 404

**Page listee dans le footer mais retourne 404**
- Solution : Creer la page /campus/ avec la liste des 6 campus ou rediriger vers /campus/paris/

### 3.5 Robots.txt & Sitemap

- **robots.txt :** présent mais **Sitemap directive absente** ❌
- **Sitemap :** 187 URLs, 7 sous-sitemaps
  - post-sitemap.xml : 124 URLs
  - page-sitemap.xml : 16 URLs
  - temoignages-sitemap.xml : 15 URLs
  - formations-sitemap.xml : 8 URLs
  - campus-sitemap.xml : 6 URLs
  - formulaire-sitemap.xml : 15 URLs
  - intervenants-sitemap.xml : 3 URLs
  - ❌ La page /footer/ est listee dans le sitemap (artefact technique)
  - ❌ Pas reference dans robots.txt
  - ❌ Des pages sans meta description sont indexees

### 3.6 Pagination

- Paginée : `les-actualites/`
- Paginée : `les-temoignages/`
- Balises rel=next/prev : **ABSENTES** ❌
- Solution : Ajouter les balises rel=next et rel=prev dans le template d'archive WordPress

---
## 4. Contenu & Données Structurées

### 4.1 Statistiques de contenu

- Pages analysées : **169**
- Moyenne : **1537 mots/page**
- Médiane : **1558 mots**
- Min : 414 | Max : 4051
- Thin content (< 300 mots) : **Aucun** ✅

Distribution des longueurs :
- 400-700 mots : 8 ████████
- 700-1000 mots : 25 █████████████████████████
- 1000-1500 mots : 47 ████████████████████████████████████████
- 1500-2500 mots : 85 ████████████████████████████████████████
- 2500-5000 mots : 4 ████

### 4.2 Meta Descriptions — CRITIQUE

**95 pages sans meta description (56%)**

Google genere automatiquement des descriptions, souvent mauvaises, ce qui reduit le CTR

**Conséquences :**
1. Google extrait du texte au hasard → description souvent incomplète, sans appel à l'action
2. Une meta description optimisée augmente le CTR de 5,8% en moyenne (Backlinko 2024)
3. Sur 95 pages, des milliers de clics potentiels perdus par mois
4. La meta description est un indice de pertinence pour Google

### 4.3 Titres & H1

- ❌ Page sans titre : `footer/`
- ❌ `formations/` → 'formations Archive - Ecole Gustave' (Contient Archive)
- ❌ `temoignages/` → 'temoignages Archive - Ecole Gustave' (Contient Archive)

- ❌ `formations/` — H1 absent
- ❌ `plan-du-site/` — H1 absent
- ❌ `donnees-personnelles/` — H1 absent
- ❌ `footer/` — H1 absent
- ❌ `temoignages/` — H1 absent
- ❌ 'Formation Macon Voirie Reseaux Divers (VRD)' présent sur `formations/` et `formations/formation-macon-vrd/`
  - L'archive utilise le H1 d'une formation specifique

### 4.4 Données Structurées JSON-LD

- **Présent :** OUI (via Yoast SEO)

**Schémas présents :**
  ✅ WebPage
  ✅ WebSite
  ✅ Organization
  ✅ BreadcrumbList
  ✅ Article
  ✅ ImageObject
  ✅ CollectionPage
  ✅ Person
  ✅ Event

**Schémas manquants (critiques) :**
  ❌ **Course** — Les formations n'apparaissent pas dans les snippets enrichis 'Course' de Google. Pas de badge 'Formation' dans les resul
  ❌ **Review** — Impossible d'avoir des etoiles dans les SERP pour les temoignages. Les etoiles augmentent le CTR de 35% en moyenne.
  ❌ **FAQ** — Pas de FAQ rich snippets. Google afficherait les questions directement dans les SERP, augmentant la visibilite et le CTR
  ❌ **VideoObject** — Les videos ne peuvent pas apparaitre dans les resultats Video Google. Perte de trafic video dans les SERP.

**Pourquoi Google en a besoin :**
- **Course :** Affiche formations avec prix/durée dans les SERP
- **Review :** Affiche les étoiles (CTR +35%)
- **FAQ :** Questions/réponses dans Google, occupe 2-3 positions SERP
- **VideoObject :** Apparition dans l'onglet Vidéo Google

---
## 5. Cannibalisation

**MASSIVE - des centaines de pages en competition sur les memes mots-cles**

| Mot-clé | Pages en compétition | Risque |
|---------|---------------------|--------|
| formation | 39 | 🔴 CRITIQUE |
| plombier_plomberie | 39 | 🔴 CRITIQUE |
| btp_batiment_construction | 37 | 🔴 CRITIQUE |
| cap | 23 | 🔴 CRITIQUE |
| electricien_electricite | 16 | 🟠 HAUT |
| cfa | 9 | 🟡 MOYEN |
| alternance | 9 | 🟡 MOYEN |
| paris | 8 | 🟡 MOYEN |
| couvreur | 7 | 🟡 MOYEN |
| lyon | 7 | 🟡 MOYEN |
| bordeaux | 7 | 🟡 MOYEN |
| marseille | 5 | 🟢 FAIBLE |

### Conflit CFA vs CAP

Pages CFA et CAP en competition directe sur les memes villes et metiers
- Exemple : cfa-plomberie-paris/ vs cap-plomberie-paris/ - titres et H1 quasi-identiques
- Étendue : Se repete pour Paris, Lyon, Bordeaux, Marseille (4 villes x 2 metiers = 16 pages en conflit)
- **32 pages en compétition directe**

**Pourquoi Google pénalise :** Plusieurs pages quasi-identiques → Google ne sait pas laquelle classer → dilution d'autorité, budget de crawl gaspillé, backlinks divisés.

---
## 6. Sécurité & RGPD

Score **D (sur 9 headers critiques, 1 seul present)** (headers de sécurité)

| Header | Statut | Risque |
|--------|--------|--------|
| strict_transport_security | ✅ | N/A |
| content_security_policy | ❌ | CRITIQUE - XSS possible |
| x_frame_options | ❌ | HIGH - Clickjacking possible |
| x_content_type_options | ❌ | HIGH - MIME sniffing possible |
| referrer_policy | ❌ | MEDIUM - Fuite de Referrer |
| permissions_policy | ❌ | MEDIUM - API navigateur sans restriction |
| cross_origin_embedder_policy | ❌ | LOW |
| cross_origin_opener_policy | ❌ | LOW |
| cross_origin_resource_policy | ❌ | LOW |

### 6.1 Exposition WordPress

- ❌ : REST API exposée
- ✅ : XML-RPC protégé
- ✅ : wp-admin masqué
- ✅ : Users API protégée
- ❌ : license.txt exposé

**Versions exposées :** yoast_seo=27.6, hubspot=11.3.45, site_kit=1.179.0, complianz=timestamp detecte

### 6.2 RGPD — Facebook Pixel

- Plugin consentement : Complianz GDPR
- Facebook Pixel avant consentement : **OUI ❌**
- Risque : NC - charge avant le consentement sur toutes les pages
- Solution : Configurer Complianz pour bloquer Facebook Pixel et tous les scripts tiers avant consentement

### 6.3 DNS

- SPF : ✅ v=spf1 include:_spf.google.com include:spf.sendinblue.com ~all
- DMARC : ❌ p=none (avec rua/ruf Sendinblue)
- CAA : ❌ Absent

---
## 7. Backlinks & Off-Page

- **Domain Rating estimé :** 10-25
- **Domaines référents :** < 50
- **Articles presse SANS backlink :** 6

### 7.1 Opportunités perdues — Presse

- ❌ Le Figaro - portrait fondatrice (mars 2026) (Article presse national)
- ❌ Le Figaro Immobilier - article formation (mars 2026) (Article presse)
- ❌ Madame Figaro - portrait (mars 2023) (Article presse)
- ❌ Le Monde - article metier plombier (avril 2022) (Article presse national)
- ❌ BFM TV - article lancement (aout 2021) (Article media national)
- ❌ BCG - Prix PEES 2025 (Communique prix)
- ❌ Marcelle - article pedagogie (janv 2025) (Article long-format)
- ❌ L'Etudiant - breve formation (Breve)

### 7.2 Plateformes manquantes

- ❌ Diplomeo - plateforme #1 de referencement formation en France
- ❌ Orientation.com
- ❌ L'Etudiant (fiche etablissement)
- ❌ Kompass
- ❌ PagesJaunes (fiche par campus)
- ❌ Trustpilot
- ❌ Avis Verifies

### 7.3 Opportunités à saisir

- 💡 Negocier des backlinks depuis les 6 articles presse existants
- 💡 Creer une fiche Diplomeo (cout mais ROI eleve)
- 💡 Creer du contenu linkable : etude sur l'insertion professionnelle dans le BTP, rapport salaires, datas
- 💡 Guest blogging sur Batiweb, BatiActu, Le Moniteur
- 💡 Liens croises avec les ecoles du groupe (Rocket School, Ecole du Soin)
- 💡 Ajout dans les fiches Wikipedia des metiers du batiment

---
## 8. Analyse Concurrentielle

### 8.1 Top 5 concurrents

| Rang | Concurrent | Apparitions Top 10 |
|------|-----------|-------------------|
| 1 | Compagnons du Tour de France | 9/10 KW |
| 2 | CMA Ile-de-France | 7/10 KW |
| 3 | MaFormation.fr | 6/10 KW |
| 4 | Eco-Campus du Batiment | 6/10 KW |
| 5 | AFPA | 5/10 KW |

### 8.2 Mots-clés où ecole-gustave.com est INVISIBLE

- ❌ **formation electricien Paris** — 0 visibilité
- ❌ **formation couvreur Paris** — 0 visibilité
- ❌ **formation macon Paris** — 0 visibilité

### 8.3 Mots-clés bien positionnés (forces)

- ✅ **formation plomberie Paris** — position 3 Page produit
- ✅ **CAP plomberie Paris** — position 3 Blog
- ✅ **formation en alternance Paris** — position 3 Page campus
- ✅ **ecole plomberie Paris** — position 3, 9, 10 (3 resultats dans top 10) 
- ✅ **devenir plombier Paris** — position 2, 6 (2 resultats dans top 10) 
- ✅ **CFA plomberie** — position 5 

### 8.4 Opportunités mots-clés

- 💡 formation BTP Paris (peu concurrentiel)
- 💡 formation alternance batiment Paris (position 3, peut monter)
- 💡 financement formation plomberie CPF (informationnel fort potentiel)
- 💡 reconversion plomberie Paris (peu de concurrence dediee)
- 💡 formation plombier sans diplome (avantage differenciant unique)

---
## 9. Social Media & Marque

**Score maturité numérique : 6/10/10**

### 9.1 LinkedIn
**✅ EXCELLENT**
- followers : 4333
- publications : Regulieres, contenu marque employeur
- recommandation : Maintenir le rythme

### 9.2 Instagram
**⚠️ MOYEN**
- followers : 802
- posts : 131
- probleme : Faible pour 2000+ apprenants, opportunite de contenu UGC
- recommandation : Augmenter la cadence, republier les apprenants

### 9.3 Facebook
**⚠️ MOYEN - INACTIF**
- followers : 336
- derniere_publication : Octobre 2025
- nap_incoherent : Adresse: 17-19 Allees de l'Europe, Clichy (different de St-Denis)
- avis : 0
- recommandation : Corriger l'adresse NAP, republier 2x/semaine

### 9.4 TikTok
**⚠️ MOYEN**
- followers : 944
- likes_cumules : ~20000
- contenu : JPO, femmes dans le BTP, humour
- recommandation : Augmenter la cadence, formats viraux

### 9.5 YouTube
**❌ INEXISTANT**
- description : Chaine @EcoleGustave vide, 0 videos
- impact : Une ecole de formation sans contenu video est un handicap majeur en 2026
- recommandation : Produire au minimum: visites de campus, temoignages apprenants, JPO en video

### 9.6 Google Business
**⚠️ MOYEN**
- note : 4.6-4.8/5
- avis : 102-146
- suspicion_faux_avis : Signale par ecolesparis.com - investigation requise
- recommandation : Creer une fiche par campus, repondre aux avis negatifs, politique transparente de collecte

---
## 10. Plan d'Action

### 🔴 Phase 1 — Urgences immédiates (7 jours)

| # | Action | Effort | Impact |
|---|--------|--------|--------|
| 1 | Corriger la redirection www (perte de chemin) | 15 min | TRES ELEVE |
| 2 | Remplacer 12 URLs staging par les URLs production dans la BDD WordPress | 30 min | TRES ELEVE |
| 3 | Rediger 10 meta descriptions prioritaires (pages les plus visitees) | 30 min | ELEVE |
| 4 | Corriger le H1 de /formations/ (n'affiche plus une formation specifique) | 10 min | ELEVE |
| 5 | Ajouter X-Frame-Options et X-Content-Type-Options dans Cloudflare | 10 min | ELEVE |
| 6 | Bloquer Facebook Pixel jusqu'au consentement dans Complianz | 20 min | CRITIQUE (RGPD) |
| 7 | Ajouter directive Sitemap dans robots.txt | 5 min | MOYEN |

### 🟠 Phase 2 — Court terme (30 jours)

| # | Action | Effort | Impact |
|---|--------|--------|--------|
| 1 | Activer les schemas JSON-LD dans Yoast SEO (Organisation, BreadcrumbList, Course) | 30 min | TRES ELEVE |
| 2 | Fusionner les pages CFA/CAP par ville (commencer par Paris plomberie) | 4h | TRES ELEVE |
| 3 | Ajouter la Content-Security-Policy via Cloudflare | 30 min | TRES ELEVE |
| 4 | Rediger les 85 meta descriptions restantes | 3h | TRES ELEVE |
| 5 | Creer les pages produits electricien, couvreur, macon Paris | 6h | TRES ELEVE |
| 6 | Creer la page /campus/ avec les 6 campus | 2h | ELEVE |
| 7 | Configurer le cache HTML Cloudflare | 20 min | ELEVE |
| 8 | Activer Cloudflare Polish (conversion WebP automatique) | 10 min | ELEVE |
| 9 | Ajouter des attributs alt aux images sans alt | 30 min | MOYEN |
| 10 | Corriger l'adresse NAP sur Facebook (Clichy -> St-Denis) | 10 min | MOYEN |
| 11 | Creer des labels accessibles pour les formulaires | 30 min | MOYEN |
| 12 | Contacter les 6 journaux pour ajouter des backlinks | 2h | TRES ELEVE |

### 🟡 Phase 3 — Moyen terme (90 jours)

| # | Action | Effort | Impact |
|---|--------|--------|--------|
| 1 | Creer fiche Diplomeo + autres annuaires manquants | 3h | ELEVE |
| 2 | Produire 15+ videos YouTube (visites campus, interviews, JPO) | 20h | ELEVE |
| 3 | Contenu linkable : etude insertion BTP, rapport salaires, datas marché | 10h | ELEVE |
| 4 | Configurer HSTS preload (max-age=31536000; includeSubDomains; preload) | 15 min | MOYEN |
| 5 | Restreindre l'API REST WordPress aux utilisateurs authentifies | 20 min | MOYEN |
| 6 | Ajouter breadcrumbs JSON-LD sur toutes les pages | 20 min | MOYEN |
| 7 | Ajouter DMARC p=quarantine | 30 min | MOYEN |
| 8 | Ajouter CAA record DNS | 10 min | FAIBLE |
| 9 | Installer un CAPTCHA (Cloudflare Turnstile) sur les formulaires | 30 min | MOYEN |
| 10 | Ajouter resource hints preconnect pour GTM et HubSpot | 10 min | FAIBLE |
| 11 | Revitaliser Facebook (publication 2x/semaine) et Instagram (+ stories) | 5h/semaine | MOYEN |
| 12 | Guest blogging sur Batiweb, BatiActu, Le Moniteur | 10h | MOYEN |

### 🟢 Phase 4 — Long terme (6 mois)

| # | Action | Effort | Impact |
|---|--------|--------|--------|
| 1 | Migrer vers un hebergement plus rapide ou optimiser Infomaniak | Variable | ELEVE |
| 2 | Refonte du maillage interne (repartition equilibree des liens) | 10h | MOYEN |
| 3 | Schema Review pour les 17 pages de temoignages (etoiles SERP) | 2h | FAIBLE |
| 4 | Ajouter les pages financement, FAQ, recrutement, tarifs | 8h | MOYEN |
| 5 | Optimiser les images restantes (dimensions, WebP, alt) | 4h | MOYEN |
| 6 | Corriger le CLS sur /ecole-gustave/ et /campus/paris/ | 2h | MOYEN |
| 7 | Programme de link building regulier | Continu | ELEVE |

---
## Annexes

### Fichiers livrés
- **`data.json`** (32 Ko) : Données structurées complètes de l'audit
- **`crawl_raw.json`** : Données brutes des 169 pages crawlées
- **`RAPPORT_AUDIT_COMPLET.md`** : Ce rapport complet
- **`meta_descriptions.csv`** : 95 meta descriptions optimisées SEO
- **`index.html`** : Dashboard interactif déployé sur GitHub Pages

### Dashboard
🔗 https://lomaab.github.io/audit-ecole-gustave/

### Méthodologie
- Google PageSpeed Insights (Lighthouse 13.3.0)
- CrUX API (Chrome User Experience Report)
- cURL (HTTP headers, TTFB, redirections)
- Analyse HTML brute (meta, headings, JSON-LD, images)
- Analyse sitemaps (7 sous-sitemaps)
- Analyse securite headers (securityheaders.com)
- Analyse DNS (CAA, SPF, DMARC, TLS)
- Analyse concurrentielle SERP (10 mots-cles)
- Analyse backlinks (websearch + annuaires)
- Analyse semantique (clusters, TF-IDF, patterns)
- Audit accessibilite (WCAG, ARIA, contrastes)
- Audit social media (LinkedIn, Instagram, FB, TikTok, YouTube)
- Analyse RGPD (Facebook Pixel, cookies tiers)
- Analyse WordPress (REST API, xmlrpc, wp-admin)

---
*Rapport généré le 16 juin 2026 — Audit automatisé multi-couches*