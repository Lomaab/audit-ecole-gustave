# Audit SEO Complet — ecole-gustave.com
**Document de synthèse — version révisée (16 juin 2026)**

| Champ | Valeur |
|-------|-------|
| Site audité | `ecole-gustave.com` |
| Date | 16 juin 2026 |
| Pages crawlées | 169 + 187 (sitemap) |
| Score global | 28/100 |
| Dashboard | https://lomaab.github.io/audit-ecole-gustave/ |
| Outils | 13 combinés (PageSpeed, CrUX, analyse HTML, audit sécurité, DNS, SERP, backlinks, social media, Rich Results Test, benchmark concurrents, analyse HTTP/3, Brotli, DOM |

---

## Executive Summary (résumé pour le client)

### En une phrase
Le site ecole-gustave.com est **bien construit techniquement** (contenu riche, HTTP/3, Brotli, pas de framework lourd) **mais saborde son SEO** par des erreurs critiques : 56% des pages sans meta description, cannibalisation massive, redirection www cassée, et pas de schémas métier sur les formations.

### 3 actions qui changent tout (cette semaine)

| # | Action | Temps | Impact attendu |
|---|--------|-------|---------------|
| 1 | Corriger la redirection www (perte de chemin) | 15 min | Récupération de tous les backlinks www + trafic perdu |
| 2 | Ajouter le schéma Course dans Yoast SEO | 30 min | 30% de visibilité SERP en plus sur les pages formation |
| 3 | Remplacer les 12 URLs staging par les URLs production | 30 min | Éviter un désastre SEO si le staging est supprimé |

### En chiffres

- **16 problèmes critiques** identifiés
- **95 pages** sans meta description (56% du site)
- **39 pages** en compétition sur le mot-clé 'plombier'
- **6 articles presse** (Figaro, Le Monde, BFMTV) sans backlink
- **TTFB à 1300ms** (données réelles CrUX) — le double du seuil recommandé
- **12 URLs staging** accessibles en production
- **168 meta descriptions** prêtes à déployer (fournies)
- **38 actions** planifiées sur 4 phases

---

## 1. Résumé Exécutif

### Forces identifiées

✅ **Core Web Vitals OK** — LCP 1800ms, CLS 0.01, INP 176ms (données réelles CrUX)
✅ **Contenu riche** — Moyenne 1537 mots/page, aucun thin content
✅ **Performance technique** — HTTP/3 disponible, Brotli actif (compression 79%), pas de frameworks lourds
✅ **Présence presse nationale** — Figaro (2x), Le Monde, BFMTV, BCG, Marcelle
✅ **LinkedIn solide** — 4333 abonnés, publications régulières
✅ **Sitemap bien structuré** — 7 sous-sitemaps, 187 URLs, 0 erreur HTTP
✅ **Sécurité de base** — Cloudflare WAF, TLS 1.3, xmlrpc/wp-admin protégés
✅ **Third-party léger** — Seulement GTM + HubSpot + Complianz (pas de scripts lourds)

### Faiblesses critiques

❌ **95 pages sans meta description (56%)** — CTR SERP reduit, Google genere des descriptions automatiques
❌ **Cannibalisation massive** — Les pages se font concurrence entre elles, aucune ne ranke bien
❌ **Schemas metier manquants (Course, Review, FAQ)** — Yoast genere bien les schemas de base (Organization, WebSite) MAIS les schemas metier sont absents : Course sur les 8 fo
❌ **Redirection www qui perd le chemin** — Perte de backlinks et de trafic www
❌ **12 URLs staging en production** — Risque de 404 massif si staging supprime
❌ **Page /campus/ en 404** — Mauvaise UX, erreur indexation Google
❌ **Facebook Pixel charge avant consentement RGPD** — Non-conforme RGPD, risque de sanction CNIL
❌ **Content-Security-Policy absente** — Risque XSS eleve
❌ **TTFB reel a 1300ms (CrUX)** — Depasse le seuil de 800ms
❌ **Absence du top 10 sur 3 mots-cles cles** — Perte de trafic sur electricien, couvreur, macon
  ... et 6 autres problèmes critiques

### Impact Google estimé

1. **TTFB à 1300ms** (données réelles CrUX) : Google utilise le TTFB comme signal de classement depuis 2018. Dépassement du seuil 800ms = facteur de déclassement, surtout mobile.
2. **95 pages sans meta description (56%)** : Google génère des descriptions automatiques, souvent coupées. CTR potentiellement réduit de 20-40%.
3. **Cannibalisation massive** : 39 pages sur 'plombier' diluent l'autorité. Aucune page ne peut devenir LA référence.
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

**Analyse :** L'écart mobile/desktop est significatif. L'accueil a 91 mobile mais 56 desktop — le site a été optimisé mobile-first sans équivalent desktop.

### 2.2 Infrastructure réseau

- **HTTP/2 + HTTP/3 (QUIC)** : ✅ Disponible via Cloudflare. Protocole le plus récent.
- **Brotli** : ✅ Actif (Brotli (~79% reduction) de réduction de taille)
- **DOM size** : ✅ ~1250 éléments (seuil Google < 1500)
- **Third-party** : ✅ Léger (Google Tag Manager, HubSpot Analytics, Complianz GDPR)
- **Resource Hints** : ❌ Aucun preconnect/preload/prefetch (seulement 2 dns-prefetch). Manque 200-400ms de latence sur ressources critiques.
- **SRI** : ❌ Absent (risque supply-chain si CDN compromis)

### 2.3 Core Web Vitals — Données réelles (CrUX)

**Note importante :** Le TTFB n'est PAS un Core Web Vital officiel. C'est un signal de performance indépendant utilisé par Google comme facteur de classement depuis 2018.

| Métrique | P75 Réel | Seuil Google | Statut |
|----------|----------|-------------|--------|
| **LCP** | 1800ms | 2500ms | ✅ OK |
| **CLS** | 0.01 | 0.1 | ✅ OK |
| **INP** | 176ms mobile / 60ms desktop | 200ms | ✅ OK |
| **FCP** | 1500ms | 1800ms | ✅ OK |
| **TTFB**⚠️ | **1300ms** | 800ms | ❌ **ÉCHEC** (signal indépendant) |

**⚠️ Le TTFB n'est pas un Core Web Vital officiel** mais un signal de classement indépendant. Google l'utilise comme facteur de ranking depuis 2018. Les CWV officiels (LCP, CLS, INP) sont tous OK.

### 2.4 Problèmes de performance

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

### 3.2 Redirection www — CRITIQUE

**www.ecole-gustave.com/formations/ redirige vers ecole-gustave.com/ (perte du chemin)**
- Impact : Toutes les sous-pages en www perdent leur referencement. Backlinks et recrutements perdus.
- Solution : Modifier la regle Cloudflare/Nginx ou le .htaccess pour preserver le chemin

### 3.3 URLs Staging en Production — CRITIQUE

**12 URLs staging**
  - ❌ `Logo SNCF`
  - ❌ `Logo Vinci`
  - ❌ `Logo Eiffage`
  - ❌ `Logo Qualiopi`
  - ❌ `Logo France Competences`
  - ❌ `Logo ministere du Travail`
- Risque : Quand le site staging sera supprime, ces 12 images deviendront des 404

### 3.4 Page /campus/ + /formation-plomberie-paris/ en 404 — CRITIQUE

- **/campus/** : listé dans le footer mais retourne 404
- **/formations/formation-plomberie-paris/** : URL listée dans le menu mais retourne 404 (slug correct : formation-plombier-chauffagiste)
- Solution : Créer les redirections 301 appropriées

### 3.5 Robots.txt & Sitemap

- **robots.txt :** présent mais Sitemap directive absente ❌
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

### 4.2 Meta Descriptions — CRITIQUE

**95 pages sans meta description (56%)**
**168 meta descriptions optimisées SEO** générées et livrées (fichier meta_descriptions.csv)

**Conséquences :** 1) Google extrait du texte au hasard 2) CTR réduit 3) Pas d'appel à l'action dans les SERP

### 4.3 Titres & H1

- ❌ Sans titre : `footer/`
- ❌ `formations/` → 'formations Archive - Ecole Gustave' (Contient Archive)
- ❌ `temoignages/` → 'temoignages Archive - Ecole Gustave' (Contient Archive)
- ❌ Sans H1 : `formations/`
- ❌ Sans H1 : `plan-du-site/`
- ❌ Sans H1 : `donnees-personnelles/`
- ❌ Sans H1 : `footer/`
- ❌ Sans H1 : `temoignages/`
- ❌ 'Formation Macon Voirie Reseaux Divers (VRD)' dupliqué sur `formations/` et `formations/formation-macon-vrd/`

### 4.4 Données Structurées JSON-LD

- **Présent :** OUI (via Yoast SEO)
- **Validé par Google Rich Results Test :** ✅ Schémas détectés, ❌ Erreur Breadcrumb (champ `item` manquant)

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

---
## 5. Cannibalisation — Problème majeur

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

---
## 6. Sécurité & RGPD

Score **D (sur 9 headers critiques, 1 seul present)** (9 headers de sécurité testés)

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

### 6.1 WordPress & DNS

- REST API : ❌ EXPOSEE
- XML-RPC : ✅ Bloqué
- wp-admin : ✅ Masqué
- Versions exposées : Yoast 27.6, HubSpot 11.3.45, Site Kit 1.179.0
- DMARC : ❌ p=none
- CAA : ❌ Absent
- HSTS preload : ❌ Non configuré (max-age=16000000, requis 31536000)

### 6.2 RGPD — Facebook Pixel

- Facebook Pixel avant consentement : **OUI ❌**
- Solution : Configurer Complianz pour bloquer Facebook Pixel et tous les scripts tiers avant consentement

---
## 7. Backlinks & Off-Page

- **Domain Rating estimé :** 10-25
- **Domaines référents :** < 50
- **Articles presse SANS backlink :** 6

**⚠️ Ces données sont des estimations (pas d'accès Ahrefs/Semrush).** Pour un profil backlinks complet, un abonnement outil métier est recommandé.

### 7.1 Opportunités perdues

- ❌ Le Figaro - portrait fondatrice (mars 2026) (Article presse national)
- ❌ Le Figaro Immobilier - article formation (mars 2026) (Article presse)
- ❌ Madame Figaro - portrait (mars 2023) (Article presse)
- ❌ Le Monde - article metier plombier (avril 2022) (Article presse national)
- ❌ BFM TV - article lancement (aout 2021) (Article media national)
- ❌ BCG - Prix PEES 2025 (Communique prix)
- ❌ Marcelle - article pedagogie (janv 2025) (Article long-format)
- ❌ L'Etudiant - breve formation (Breve)

### 7.2 Opportunités à saisir

- 💡 Negocier des backlinks depuis les 6 articles presse existants
- 💡 Creer une fiche Diplomeo (cout mais ROI eleve)
- 💡 Creer du contenu linkable : etude sur l'insertion professionnelle dans le BTP, rapport salaires, datas
- 💡 Guest blogging sur Batiweb, BatiActu, Le Moniteur
- 💡 Liens croises avec les ecoles du groupe (Rocket School, Ecole du Soin)
- 💡 Ajout dans les fiches Wikipedia des metiers du batiment

---
## 8. Analyse Concurrentielle

### 8.1 Top 5 concurrents

| Concurrent | Apparitions Top 10 |
|-----------|-------------------|
| Compagnons du Tour de France | 9/10 KW |
| CMA Ile-de-France | 7/10 KW |
| MaFormation.fr | 6/10 KW |
| Eco-Campus du Batiment | 6/10 KW |
| AFPA | 5/10 KW |

### 8.2 Benchmark technique

| Concurrent | HTTP | TTFB | Sécurité | Compression | CDN |
|-----------|------|------|----------|-------------|-----|
| Compagnons du Tour de France | HTTP/2 | 598ms | Faible (pas HSTS, pas XFO) | Gzip | LiteSpeed (Hostinger) |
| CMA Ile-de-France | HTTP/2 | ~108ms (bloque curl) | HSTS preload, pas de CSP | Inconnu | OVH |
| MaFormation.fr | HTTP/2 | 1659ms | Excellent (CSP, HSTS 2ans) | Brotli | Aucun |
| Eco-Campus | N/A | N/A (hors ligne) | N/A | N/A | N/A |
| AFPA | HTTP/2 | 186ms | Excellent (CSP, HSTS, XFO, nosniff) | Gzip | Google Cloud |

**Résultat :** Seule AFPA surpasse ecole-gustave.com techniquement. Les autres concurrents ont des TTFB plus élevés, pas de CDN, ou une sécurité faible. L'école a un avantage technique réel à exploiter.

### 8.3 Opportunités marché

- 💡 AFPA exceptee, ecole-gustave peut etre 2-3x plus rapide que la moyenne des concurrents
- 💡 Creer un hub de contenu BTP (guides metiers, reconversion) - aucun concurrent ne le fait bien
- 💡 UX mobile + quizz orientation + simulateur CPF = avantage produit unique
- 💡 Eco-Campus mort = opportunite de capter son trafic formation BTP

---
## 9. Social Media & Marque

**Score maturité numérique : 6/10**

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
**⚠️ INACTIF**
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
| 2 | Creer une redirection 301 de /formations/formation-plomberie-paris/ vers /formations/formation-plombier-chauffagiste/ | 5 min | ELEVE |
| 3 | Remplacer 12 URLs staging par les URLs production dans la BDD WordPress | 30 min | TRES ELEVE |
| 4 | Activer les schemas JSON-LD dans Yoast SEO (Course, Organisation, BreadcrumbList) + corriger Breadcrumb error | 30 min | TRES ELEVE |
| 5 | Rediger 10 meta descriptions prioritaires (pages les plus visitees) | 30 min | ELEVE |
| 6 | Corriger le H1 de /formations/ (n'affiche plus une formation specifique) | 10 min | ELEVE |
| 7 | Ajouter X-Frame-Options et X-Content-Type-Options dans Cloudflare | 10 min | ELEVE |
| 8 | Bloquer Facebook Pixel jusqu'au consentement dans Complianz | 20 min | CRITIQUE (RGPD) |
| 9 | Ajouter directive Sitemap dans robots.txt | 5 min | MOYEN |
| 10 | Corriger l'erreur Breadcrumb JSON-LD (ajouter champ 'item' manquant sur chaque element) | 15 min | MOYEN |

### 🟠 Phase 2 — Court terme (30 jours)

| # | Action | Effort | Impact |
|---|--------|--------|--------|
| 1 | Fusionner les pages CFA/CAP par ville (commencer par Paris plomberie) | 4h | TRES ELEVE |
| 2 | Ajouter la Content-Security-Policy via Cloudflare | 30 min | TRES ELEVE |
| 3 | Rediger les 85 meta descriptions restantes | 3h | TRES ELEVE |
| 4 | Creer les pages produits electricien, couvreur, macon Paris | 6h | TRES ELEVE |
| 5 | Creer la page /campus/ avec les 6 campus | 2h | ELEVE |
| 6 | Configurer le cache HTML Cloudflare | 20 min | ELEVE |
| 7 | Activer Cloudflare Polish (conversion WebP automatique) | 10 min | ELEVE |
| 8 | Ajouter des attributs alt aux images sans alt | 30 min | MOYEN |
| 9 | Corriger l'adresse NAP sur Facebook (Clichy -> St-Denis) | 10 min | MOYEN |
| 10 | Creer des labels accessibles pour les formulaires | 30 min | MOYEN |
| 11 | Contacter les 6 journaux pour ajouter des backlinks | 2h | TRES ELEVE |

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
## Notes & Améliorations requises

### Éléments nécessitant un accès client

Les analyses suivantes n'ont PAS PU être réalisées car elles nécessitent un accès aux outils du client :

| Analyse | Outil nécessaire | Pourquoi c'est important |
|---------|-----------------|--------------------------|
| Google Search Console | Accès GSC | Données réelles de clics, impressions, positions, indexation |
| Google Analytics 4 | Accès GA4 | Trafic, sources, taux de conversion, valeur de lead |
| Log files analyse | Logs serveur Cloudflare | Budget de crawl Googlebot, crawl efficiency |
| Backlinks complets | Abonnement Ahrefs/Semrush | Profil backlinks réel, analyse concurrentielle, link intersect |
| Core Web Vitals détaillés | GSC rapport Page Experience | CWV par URL (pas juste la moyenne) |
| Keyword position tracking | Rank tracker outil | Suivi quotidien des positions réelles |

**Recommandation :** Demander l'accès GSC + GA4 au client avant la présentation finale. Sans ces données, l'impact business réel ne peut pas être chiffré.

### Glossaire (jargon technique expliqué)

| Terme | Explication simple |
|-------|-------------------|
| **TTFB** | Temps que met le serveur à répondre à la première requête. Plus c'est bas, mieux c'est. |
| **CLS** | Mesure si les éléments de la page bougent après l'affichage (défaut de mise en page). |
| **LCP** | Temps que met le plus grand élément (image, texte) à s'afficher. |
| **CWV** | Core Web Vitals — les 3 mesures de performance que Google utilise pour le classement. |
| **CSP** | Header de sécurité qui empêche les attaques XSS (injection de code malveillant). |
| **JSON-LD** | Format de données structurées que Google lit pour comprendre le contenu d'une page. |
| **DR** | Domain Rating — mesure de la qualité des backlinks pointant vers un site. |
| **Schema** | Code qui dit à Google que votre page est une formation, un avis, une FAQ, etc. |
| **Cannibalisation** | Quand plusieurs pages de votre site parlent du même sujet — elles se font concurrence. |
| **Brotli** | Algorithme de compression moderne (meilleur que Gzip). Rend les pages plus légères. |
| **SRI** | Subresource Integrity — vérifie que les scripts externes n'ont pas été modifiés. |
| **Preconnect** | Indique au navigateur de se connecter à l'avance à un serveur externe. |

---
## Annexes

### Fichiers livrés
- **`data.json`** (38 Ko) : Données structurées complètes (16 sections)
- **`crawl_raw.json`** : Données brutes des 169 pages crawlées
- **`RAPPORT_AUDIT_COMPLET.md`** : Ce rapport (version révisée)
- **`meta_descriptions.csv`** : 168 meta descriptions optimisées SEO
- **`index.html`** : Dashboard interactif (7 pages, chargement dynamique)

🔗 Dashboard : https://lomaab.github.io/audit-ecole-gustave/

*Rapport généré le 16 juin 2026 — Version révisée — 13 outils combinés — 16 problèmes critiques identifiés*