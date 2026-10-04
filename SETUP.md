


# Remettre une clé USB bootable Linux en clé USB normale

> **À lire avant de commencer**
>
> - Cette procédure fonctionne sous **Windows**.
> - Elle **efface toutes les données** présentes sur la clé USB.
> - Repère bien la taille de ta clé USB avec `list disk` pour ne pas te tromper de disque.
> - Si tu sélectionnes le mauvais disque, tu risques d’effacer ton disque principal.
> - Ici, la clé sera formatée en **exFAT**, compatible avec Windows et macOS.
> - Si tu veux une compatibilité maximale avec d’anciens appareils, tu peux utiliser `fat32` à la place de `exfat`.

---

## 1. Ouvrir PowerShell en administrateur

Cherche **PowerShell** ou **Terminal**, puis ouvre-le en tant qu’administrateur.

---

## 2. Lancer DiskPart

Écris :

```powershell
diskpart
```

---

## 3. Lister les disques

Dans DiskPart, écris :

```diskpart
list disk
```

Repère ta clé USB grâce à sa taille.

Exemple :

```text
Disque 0   512 Go
Disque 1   256 Go
Disque 2    29 Go
```

Ici, si ta clé USB fait environ 32 Go, elle correspond probablement au `Disque 2`.

---

## 4. Sélectionner la clé USB

Remplace `X` par le numéro de ta clé USB.

```diskpart
select disk X
```

Exemple :

```diskpart
select disk 2
```

---

## 5. Nettoyer, formater et rendre la clé utilisable

Copie-colle les commandes suivantes une par une dans DiskPart :

```diskpart
clean
```

```diskpart
create partition primary
```

```diskpart
format fs=exfat label="MaCleUSB" quick
```

```diskpart
assign
```

```diskpart
exit
```

Tu peux remplacer `"MaCleUSB"` par le nom que tu veux donner à ta clé.

---

## Résultat

Ta clé USB est maintenant redevenue une clé USB normale, vide et utilisable.
