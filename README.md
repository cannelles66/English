# English Coach — application Cloudflare

Application web progressive (PWA) pour apprendre l'anglais, prête à être déployée sur **Cloudflare Pages**.

## Fonctionnalités incluses
- 5 niveaux : A1, A2, B1, B2 et C1/C2
- Vocabulaire avec traduction, exemples, recherche et prononciation
- Leçons de grammaire progressives
- Tableau de 25 verbes irréguliers
- Quiz de 10 questions avec correction et score
- Assistant de conversation IA via Cloudflare Pages Function
- Sauvegarde locale de la progression (localStorage)
- Installation sur mobile et cache hors ligne de l'interface (PWA)

## Déploiement rapide sur Cloudflare Pages

1. Décompresse `english_coach_cloudflare.zip`.
2. Dans Cloudflare, ouvre **Workers & Pages → Create → Pages → Upload assets** (ou Direct Upload).
3. Donne un nom au projet, par exemple `english-coach`.
4. Téléverse le contenu du dossier décompressé (le fichier `index.html` doit être à la racine).
5. Pour activer l'assistant IA, le projet doit exécuter les Pages Functions. Le plus simple est de connecter le dossier à un dépôt Git et de déployer avec Cloudflare Pages, en conservant le dossier `functions/` à la racine et en utilisant `.` comme répertoire de sortie. Selon le mode de déploiement, le téléversement statique direct peut ne pas publier les Functions.

### Activer l'assistant IA

Dans **Workers & Pages → ton projet → Settings → Variables and Secrets**, ajoute :

- `OPENAI_API_KEY` : ta clé API OpenAI, enregistrée comme **secret**.
- `OPENAI_MODEL` (facultatif) : par exemple `gpt-4o-mini`.

Redéploie ensuite le projet. La clé reste côté serveur et n'est jamais exposée dans le navigateur.

> L'utilisation de l'API OpenAI peut entraîner une facturation séparée. Une clé ChatGPT Plus/Free n'est pas une clé API.

## Déploiement avec Wrangler (optionnel)

Avec Node.js et Wrangler installés :
```bash
npm install -g wrangler
wrangler pages deploy . --project-name english-coach
```
Pour un déploiement Pages Functions fiable, utilise de préférence l'intégration Git décrite ci-dessus et vérifie que `functions/api/chat.js` est bien détecté comme route `/api/chat`.

## Personnalisation
- Les listes de vocabulaire, grammaire, verbes et questions se trouvent au début de `app.js`.
- Les couleurs et styles se trouvent dans `styles.css`.
- La progression est stockée dans le navigateur de l'utilisateur. Elle n'est pas synchronisée entre appareils.

## Limites de cette première version
- Le contenu pédagogique fourni est une base de démarrage, pas un programme exhaustif.
- Les statistiques sont locales au navigateur.
- La conversation IA nécessite une clé API et le déploiement de la Function Cloudflare.
- La prononciation utilise la synthèse vocale du navigateur.
