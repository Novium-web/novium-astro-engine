# Novium Astro Engine

![Astro](https://img.shields.io/badge/Astro-FF7A59?style=flat&logo=astro&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind%20CSS-38B2AC?style=flat&logo=tailwind-css&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-%3E%3D22.12-339933?style=flat&logo=nodedotjs&logoColor=white)
![CLI](https://img.shields.io/badge/CLI-Custom%20Scaffolding-black?style=flat)
![Lighthouse](https://img.shields.io/badge/Lighthouse-100%2F100-00CC66?style=flat&logo=lighthouse&logoColor=white)
![Core Web Vitals](https://img.shields.io/badge/Core_Web_Vitals-Optimal-4285F4?style=flat&logo=google&logoColor=white)
![SEO](https://img.shields.io/badge/SEO-Cheerio%20Audit-blueviolet?style=flat)
![Zod](https://img.shields.io/badge/Validation-Zod-3068B7?style=flat&logo=zod&logoColor=white)
![Cloudflare](https://img.shields.io/badge/Cloudflare_Pages-Ready-F38020?style=flat&logo=cloudflare&logoColor=white)
![Decap CMS](https://img.shields.io/badge/Decap%20CMS-Integrated-FF7828?style=flat)
![Status](https://img.shields.io/badge/Status-In%20Production-success?style=flat)
![License](https://img.shields.io/badge/License-Proprietary-red?style=flat)

Moteur Web que j'ai conçu et développé pour ma micro-entreprise **Novium**, dédié à la génération, au déploiement et à la gestion de sites vitrines professionnels ultra-rapides et optimisés pour le référencement local.

---

## 💡 Pourquoi j'ai créé ce projet ?

Dans le cadre de mon activité avec **Novium**, j'accompagne des artisans, commerces de proximité et indépendants dans leur présence en ligne. Face aux limites récurrentes des CMS traditionnels (lourdeurs, failles de sécurité, maintenance chronophage et performances mobiles dégradées), j'ai choisi de concevoir **mon propre moteur sur-mesure**.

Mon objectif était double :
1. **Délivrer une expérience utilisateur irréprochable** : des temps de chargement quasi-instantanés, un score Lighthouse parfait (100/100) et une ergonomie mobile pensée pour maximiser la conversion (appels d'urgence, itinéraires GPS, avis vérifiés).
2. **Automatiser la rigueur technique** : garantir un référencement naturel (SEO) optimal et sans faille dès la compilation grâce à une suite de tests d'audit intégrée au build.

---

## 📊 Benchmark & Métriques Clés

Comparatif moyen mesuré entre un site déployé avec **Novium Astro Engine** et un site vitrine standard sous CMS dynamique traditionnel (ex: WordPress + Page Builder) :

| Métrique | CMS Traditionnel | Novium Astro Engine | Gain / Impact |
|---|:---:|:---:|---|
| **Score Google Lighthouse Mobile** | 50 - 75 / 100 | **100 / 100** | Expérience fluide & meilleur ranking SEO |
| **First Contentful Paint (FCP)** | 1.8s - 3.2s | **< 0.6s** | Affichage quasi-instantané |
| **Poids moyen d'une page** | 2.5 Mo - 6 Mo | **< 160 Ko** | Économie de bande passante & écoconception |
| **JavaScript bloquant exécuté** | 400 Ko - 1.2 Mo | **0 Ko** | Zéro saccade au défilement |
| **Temps de compilation complet** | N/A (Serveur PHP/SQL) | **~ 1.4s** | Déploiements et itérations ultra-rapides |

---

## 🧠 Décisions d'Architecture & Arbitrages Techniques

Pour concevoir un moteur pérenne, scalable et facilement maintenable, j'ai fait plusieurs choix structurants :

### 1. Astro plutôt qu'une SPA ou un CMS dynamique
- **Pourquoi pas une SPA (Next.js / React) ?** Un site vitrine n'a pas besoin de transporter un runtime JavaScript complet sur le smartphone du visiteur. L'approche d'Astro permet de compiler du pur HTML statique pré-rendu tout en gardant une logique de composants moderne.
- **Islands Architecture :** Le JavaScript n'est chargé que de manière ciblée et différée si une interaction l'exige. Résultat : zéro blocage du thread principal.

### 2. Typage et intégrité des données avec Zod
- Chaque donnée saisie (coordonnées d'artisan, numéros d'urgence, avis clients, prestations, liens sociaux) passe par une validation de schéma **Zod** stricte.
- Si un champ obligatoire est manquant, mal formaté ou invalide, l'erreur est détectée dès la compilation, éliminant tout bug en production.

### 3. Design Tokens & Presets découplés
- Le code HTML et les composants sont **100 % agnostiques du métier et du style**.
- L'univers visuel (typographies, arrondis, ombres, bordures) et les réglages sectoriels (ordre des sections, libellés, données Schema.org) sont pilotés par des tokens configurables. Cela me permet de décliner un site pour un serrurier, un restaurant ou une boutique sans retoucher le balisage des composants.

### 4. Audit SEO automatisé post-build (Cheerio)
- Le référencement naturel étant crucial pour mes clients locaux, j'ai développé une suite de vérification programmatique avec **Cheerio**.
- À chaque `npm run build`, le script inspecte directement le HTML compilé pour vérifier :
  - L'unicité absolue de la balise `<h1>`.
  - La présence et la longueur minimale de `<title>` et `<meta name="description">`.
  - La validité de `<link rel="canonical">` et des balises OpenGraph.
  - La conformité du schéma JSON-LD (présence de `@type`, nom et téléphone).
  - La cohérence de la balise `robots` (interdiction d'indexer un site en mode brouillon).
- **Si un seul critère échoue, le build est interrompu avec un code d'erreur non nul.**

---

## 🚀 Workflow CI/CD & Déploiement

Le cycle de production repose sur un pipeline moderne, automatisé et sécurisé :

```
[Modification Contenu / Code]
           │
           ▼
     git push origin
           │
           ▼
   Build Astro & SSG
           │
           ▼
 Tests SEO Bloquants (Cheerio) ──❌── Échec (Build rejeté si régression SEO)
           │
          ✅ Succès
            ▼
 Déploiement Edge CDN (Cloudflare Pages)
```

- **Hébergement Edge mondial (Cloudflare Pages)** : distribution des fichiers HTML au plus proche des visiteurs avec mise en cache automatique et certificats SSL gérés nativement.
- **Sécurité maximale** : sans base de données SQL ni serveur dynamique exposé en ligne, le risque d'injection ou d'intrusion est nul.
- **Zéro maintenance infrastructure** : aucun plugin à patcher, aucun serveur à redémarrer, réduisant le coût de maintenance à son strict minimum.

---

## 🛠️ Ce que j'ai implémenté côté fonctionnalités

- **Scaffolding CLI interactif (Node.js natif)** : j'ai développé un outil en ligne de commande sans dépendance externe (`scripts/new-client.mjs`) qui guide la création d'un nouveau site client (identité, contact, Google Place ID, métadonnées SEO) en moins de 60 secondes.
- **Mobile-First calibré pour la conversion** : bouton d'appel sticky positionné dans la zone naturelle du pouce, intégration directe des itinéraires GPS Google Maps et affichage dynamique des avis Google certifiés.
- **Autonomie client avec Decap CMS** : espace d'administration épuré sous `/admin` permettant à mes clients de modifier leurs horaires, textes et photos en toute autonomie sans toucher au code.
- **Formulaire de contact sécurisé** : traitement léger avec honeypot anti-spam natif et mode simulation en environnement de test.
- **Pages locales dynamiques** : génération automatique de landing pages géociblées (`/zone/[ville]`) pour couvrir les secteurs d'intervention des professionnels.

---

## 🧰 Stack Technique

| Technologie | Rôle & Usage |
|---|---|
| **Astro** | Générateur de site statique haute performance (SSG) |
| **Tailwind CSS (v4)** | Système de design fluide basé sur des tokens modulaires |
| **TypeScript** | Typage statique de bout en bout |
| **Zod** | Validation stricte des données et contenus |
| **Decap CMS** | Interface d'administration Git-based pour les clients |
| **Cheerio** | Moteur de parsing HTML pour les assertions SEO automatisées |
| **Node.js (CLI)** | Script d'initialisation et de scaffolding interactif sans dépendance externe |
| **Cloudflare Pages** | Hébergement statique distribué sur réseau CDN Edge |

---

## 🔒 Confidentialité & Propriété

Ce moteur constitue la propriété intellectuelle et la base technique exclusive de mes prestations au sein de **Novium**. 
Le code source complet et les modules internes demeurent privés. Ce dépôt public sert de vitrine technique pour illustrer mes compétences en développement web moderne, architecture logicielle et automatisation.
