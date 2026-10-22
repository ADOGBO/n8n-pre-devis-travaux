# Pré-devis travaux automatisé (n8n + IA)

Workflow n8n qui transforme une demande de chantier en pré-devis,
avec validation humaine avant envoi.

## Cas d'usage
Un commercial ou un client décrit un chantier dans un formulaire.
Le workflow produit un pré-devis chiffré, soumis à un responsable
avant tout envoi.

## Structure
```text
n8n-pre-devis-travaux/
├── workflow.json
├── README.md
└── docs/
    ├── bareme.png (capture d'écran du barème fictif)
    └── canevas.png   (capture d'écran du workflow complet)

```


## Fonctionnement
1. Formulaire de demande (n8n Form Trigger)
2. Extraction des postes de travaux par un LLM (API Groq, modèle Qwen)
3. Contrôle du JSON renvoyé + alerte email en cas d'échec
4. Application d'un barème de prix avec Google Sheet
5. Calcul HT / TVA / TTC et génération du devis HTML
6. Validation humaine (nœud Wait)
7. Envoi du devis par Gmail

## Robustesse
- Sortie IA invalide : alerte email, aucun devis envoyé
- API indisponible : erreur capturée, même alerte
- Aucun envoi sans approbation d'un responsable
- Barème intégré  dans Google Sheet modifiable
  par les équipes

## Limites et évolutions
- Pas de PDF : le devis part en HTML dans l'email
- Données fictives uniquement
- Piste : interroger un RAG (historique de devis) avant le chiffrage

## Installation
1. `npx n8n` puis ouvrir http://localhost:5678
2. Importer `workflow.json` (menu ⋯ → Import from file)
3. Créer les credentials : Header Auth (clé Groq) et Gmail OAuth2
