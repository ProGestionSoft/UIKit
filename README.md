# 🧩 PGS UI Kit

**PGS UI Kit** est une bibliothèque de composants Vue 3 conçue pour les projets PRO GESTION SOFT et leurs partenaires.

Elle centralise des composants réutilisables, stylés avec Tailwind CSS et intégrés à l’écosystème Nuxt/Vue.

---

## 🚀 Installation

### Depuis NPM

```bash
npm install @progestionsoft/pgs-ui-kit
```

### Depuis GitHub Packages

```bash
npm install @progestionsoft/pgs-ui-kit --registry=https://npm.pkg.github.com
```

## 🔧 Utilisation

``` vue
<script setup>
import { ErrorPage } from '@progestionsoft/pgs-ui-kit'
</script>

<template>
  <ErrorPage :localConfig="configLocal" :configUrl="configUrl" />
</template>
```

## 🧠 Composants disponibles

- ErrorPage – Page d’erreur personnalisable
- D'autres composants sont en cours d'intégration...


## ⚙️ Configuration
``` js
const configLocal = {
  logoLight: '/img/logo.png',
  logoDark: '/img/logoDark.png',
  copyright: '© 2025 Nom de la page. Tous droits réservés.'
};

const configUrl = 'https://raw.githubusercontent.com/ProGestionSoft/Files/main/General/templates/ErrorConfig.json';
```

## 🌐 Dépendances
- Vue 3
- Tailwind CSS
- @tabler/icons-vue

## 🤝 Contribution
Les contributions sont les bienvenues !

Forkez ce dépôt, créez une branche et ouvrez une Pull Request.

## 🛡️ Licence
Ce projet est sous licence MIT.

## 📦 Publication
Ce package est disponible sur :
- npmjs.com
- GitHub Packages

## 🧑‍💻 Mainteneur
Développé et maintenu par l’équipe **PRO GESTION SOFT**.
