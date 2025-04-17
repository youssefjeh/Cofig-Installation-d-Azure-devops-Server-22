# ⚙️ Configuration Azure DevOps Server 2022 – Serveur WIN_AZ_DEVOPS

Ce projet documente l’installation et la configuration complète d’un serveur **Azure DevOps Server 2022** sur l’environnement **WIN_AZ_DEVOPS**. Il comprend les paramétrages avancés, l'intégration avec SQL Server, la configuration d’IIS et les considérations de sécurité.

## 🧩 Sommaire

1. [Introduction](#introduction)
2. [Assistant de Configuration](#assistant-de-configuration)
3. [Choix de la Configuration](#choix-de-la-configuration)
4. [Langue d’Installation](#langue-dinstallation)
5. [Configuration SQL Server](#configuration-sql-server)
6. [Compte de Service](#compte-de-service)
7. [Application Tier](#application-tier)
8. [Composant de Recherche](#composant-de-recherche)
9. [Project Collection](#project-collection)
10. [Vérification & Validation](#vérification--validation)
11. [Configuration IIS](#configuration-iis)
12. [Accès au Serveur](#accès-au-serveur)

---

## 📘 Introduction

Ce guide couvre l’installation d’Azure DevOps Server 2022 sur **WIN_AZ_DEVOPS**, avec configuration personnalisée (mode avancé), sécurité renforcée, et optimisation des services.

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
  - 🔐 Droits administrateur local sur **WIN_AZ_DEVOPS**
  - 🎯 Rôle `sysadmin` sur SQL Server

➡️ Problème résolu : accès SQL insuffisant, corrigé via les bons privilèges.


---

## 👤 Compte de Service

- Utilisé : `NT AUTHORITY\NETWORK SERVICE` (compte système Windows par défaut)

---

## 🌍 Application Tier

- Protocoles : HTTP & HTTPS
- Certificat SSL : généré via **CA MASSA**
- SSH : Port `22`
- Cache fichiers : `E:\zureDevOpsServerData\ApplicationTier\_fileCache`

---

## 🔍 Composant de Recherche

- **Search** désactivé via l’assistant
- ✅ **Full-Text Search** installé manuellement (obligatoire)
- 📌 Erreur évitée : `F255149` (absence de Full-Text Search)

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

- Accès local : [https://WIN_AZ_DEVOPS.DN_ENT.com](https://WIN_AZ_DEVOPS.DN_ENT.com)
- Accès externe : en attente de validation par l’équipe sécurité

---

## 📎 Notes

Ce projet est à usage interne, et documente une installation sur mesure adaptée aux contraintes réseau et sécurité de l’environnement **DN_ENT**.

---

