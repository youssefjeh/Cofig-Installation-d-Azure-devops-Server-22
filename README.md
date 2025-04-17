# ⚙️ Configuration Azure DevOps Server 2022 – WIN_AD_SERVER

Ce projet documente l’installation et la configuration complète d’un serveur **Azure DevOps Server 2022** sur l’environnement **WIN_AD_SERVER**. Il comprend les paramétrages avancés, l'intégration avec SQL Server, la configuration d’IIS et les considérations de sécurité.

                    🔐 User (internes / externes)
                             |
                             | (HTTP / HTTPS)
                             v
                  🌐 Serveur IIS (WIN_AD_SERVER – Azure DevOps Server)
                ┌────────────────────────────────────────────┐
                │   - Windows Authentication activée         │
                │   - Certificat SSL (CA__ENT)              │
                │   - Site déplacé vers disque E:\           │
                │   - Ports : 80 / 443 / 22 (SSH)            │
                └────────────────────────────────────────────┘
                             |
                             | (SQL Queries)
                             v
                  🗄️ SQL Server (SQL_AD_SERVER – Instance dédiée)
                ┌────────────────────────────────────────────┐
                │   - Base de données Azure DevOps           │
                │   - Full-Text Search installé              │
                │   - Rôle sysadmin pour le compte de service│
                └────────────────────────────────────────────┘
                             |
                             | (Fichier Cache, Logs)
                             v
                    💾 Stockage local sur WIN_AD_SERVER
                ┌────────────────────────────────────────────┐
                │   - E:\zureDevOpsServerData\               │
                │   - _fileCache                              │
                └────────────────────────────────────────────┘

---

## 📘 Introduction

Ce guide couvre l’installation d’Azure DevOps Server 2022 sur **WIN_AD_SERVER**, avec configuration personnalisée (mode avancé), sécurité renforcée, et optimisation des services.

---

## ⚙️ Assistant de Configuration

Le **Centre de configuration** se lance automatiquement après l’installation. Il permet de :
- Gérer les nouvelles installations
- Effectuer des mises à niveau
- Configurer l’application

---

## 🛠️ Choix de la Configuration

🔧 **Mode choisi : Advanced**

Permet de :
- Spécifier le serveur SQL (ex. : `SQL_AD_SERVER`)
- Configurer IIS, le cache, les ports, les certificats SSL
- Garder le contrôle complet

---

## 🌐 Langue d’installation

- Langue : **English (US)**

---

## 🗄️ Configuration SQL Server

- Serveur SQL : `SQL_AD_SERVER`
- Compte de service avec :
  - 🔐 Droits administrateur local sur **WIN_AD_SERVER**
  - 🎯 Rôle `sysadmin` sur SQL Server

➡️ Problème résolu : accès SQL insuffisant, corrigé via les bons privilèges.


` TF255062: Failed to reach SQL instance. Verify that you have entered the correct name for the server and SQL instance, that the server and SQL instance are online, and that you have the required permissions. If the SQL instance is not on this computer, verify that it is configured to allow remote connections, that the TCP/IP protocol is enabled and configured, and that port 1433 is not blocked by Windows Firewall rules.`

---

## 👤 Compte de Service

- Utilisé : `NT AUTHORITY\NETWORK SERVICE` (compte système Windows par défaut)

---

## 🌍 Application Tier

- Protocoles : HTTP & HTTPS
- Certificat SSL : généré via **CA_ENT**
- SSH : Port `22`
- Cache fichiers : `E:\zureDevOpsServerData\ApplicationTier\_fileCache`

---

## 🔍 Composant de Recherche

- **Search** désactivé via l’assistant
- ✅ **Full-Text Search** installé manuellement (obligatoire)
- 📌 Erreur évitée : `F255149` (absence de Full-Text Search)

`F255149: The following server that is running SQL Server does not have the 
full-text search feature installed: KARCEL. This feature is required for 
Azure DevOps Server to operate correctly.`

---

## 📁 Project Collection

- Nom par défaut conservé : `DefaultCollection`

---

## 🧪 Vérification & Validation

- Revue des paramètres
- Bouton **Verify** pour validation
- ✅ En cas de succès → clic sur **Configure**
- ❌ En cas d’échec → corriger et relancer

---

## 🌐 Configuration IIS

- Chemin physique du site déplacé de `C:\…` vers `E:\…`
- ✅ **Windows Authentication** activée dans IIS

---

## 🚀 Accès au Serveur

- Accès local : [https://WIN_AD_SERVER.DN_ENT.com](https://WIN_AD_SERVER.DN_ENT.com)
- Accès externe : en attente de validation par l’équipe sécurité

---

## 📎 Notes

Ce projet est à usage interne, et documente une installation sur mesure adaptée aux contraintes réseau et sécurité de l’environnement **DN_ENT**.

---

