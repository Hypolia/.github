<img height="50" src="https://github.com/Hypolia/.github/blob/main/icon.png" alt="Hypolia" />

![Rust](https://img.shields.io/badge/Rust-000000?style=for-the-badge&logo=rust&logoColor=white)
![Minecraft](https://img.shields.io/badge/Minecraft-62B47A?style=for-the-badge&logo=minecraft&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![Argo CD](https://img.shields.io/badge/Argo%20CD-EF7B4D?style=for-the-badge&logo=argo&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![Astro](https://img.shields.io/badge/Astro-BC52EE?style=for-the-badge&logo=astro&logoColor=white)

![Hypolia Banner](https://github.com/Hypolia/.github/blob/main/Croquis.png)

Hypolia est un serveur Minecraft de mini-jeux. Tout le réseau est écrit en Rust, tourne sur
[rspigot](https://github.com/ferrislabs/rspigot) et se déploie sur Kubernetes.

## Les dépôts

| Dépôt | Rôle |
|---|---|
| [`sdk`](https://github.com/hypolia/sdk) | Contrats partagés : protocole lobby / jeux / orchestrateur, domaine de la progression joueur |
| [`platform`](https://github.com/hypolia/platform) | Orchestrateur (files d'attente, matchmaking, flotte de serveurs), plugin proxy, chart Helm du réseau |
| [`lobby`](https://github.com/hypolia/lobby) | Hub : spawn, PNJ, menus, profil, collectibles, comptes |
| [`sheepwars`](https://github.com/hypolia/sheepwars) | Mini-jeu SheepWars |
| [`towerwars`](https://github.com/hypolia/towerwars) | Mini-jeu TowerWars, modes Solo et Duo |
| [`hypolia.fr`](https://github.com/hypolia/hypolia.fr) | Site, blog et documentation |
| `infra` (privé) | Déploiement GitOps du réseau |

## Architecture

- **Proxy** : `rspigot-proxy` avec le plugin Hypolia. Il route les joueurs vers les lobbies et les parties.
- **Orchestrateur** : service Rust (axum, kube-rs). Il gère les files, lance les pods de jeu à la demande et suit leur heartbeat.
- **Serveurs de jeu** : un serveur rspigot par partie, avec le plugin du jeu en sidecar.
- **Données** : PostgreSQL (CloudNativePG) pour la progression et le lobby, RustFS (S3) pour les maps.
- **Déploiement** : images sur `ghcr.io/hypolia`, chart Helm, Argo CD sur un cluster k3s.

## Le site

`hypolia.fr` est un monorepo pnpm + Turborepo avec trois apps Astro (site, blog, docs),
React 19 et Tailwind CSS 4.
