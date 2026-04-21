# Problème signalé

Après une réponse de l'assistant, le champ/prompt pour continuer la discussion disparaît, ce qui oblige à créer une nouvelle ligne de chat.

## Hypothèses probables
- Re-rendu complet du composant après réception de la réponse.
- Perte du focus sur l'input suite à un changement d'état global.
- Condition d'affichage de l'input liée à un état de streaming mal réinitialisé.

## Vérifications recommandées
1. Vérifier que le composant d'input reste monté pendant et après le streaming.
2. Forcer le focus après la fin de réponse (callback `onComplete`).
3. Confirmer que `isStreaming` (ou équivalent) revient bien à `false`.
4. Éviter les clés React instables sur le conteneur de conversation.

## Correctif UX minimal
- Garder l'input visible en permanence.
- Désactiver seulement le bouton d'envoi pendant la génération.
- Réactiver l'input et remettre le focus à la fin de génération.

