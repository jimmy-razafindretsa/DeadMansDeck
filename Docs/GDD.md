# Dead Man's Deck : Le Pont du Revenant — GDD v1.0

> Version texte du [GDD PDF](../DeadMansDeck_GDD_FR.pdf). Les figures (concept art, plan du pont, maquette HUD) ne sont disponibles que dans le PDF.

**FPS Arcade de Défense d'Abordage sous Unreal Engine 5**

| | |
|---|---|
| Genre | FPS Wave Defense / Arcade Gunner |
| Moteur | Unreal Engine 5 (Chaos + Lumen) |
| Équipe | Développeur Solo |
| Échéance | Début Décembre 2026 |
| ESRB | T (Adolescents 13+) |

| Version | Auteur | Date | Commentaires et jalons |
|---|---|---|---|
| 0.10 | Développeur Solo | 01/11/2026 | Pitch initial : Concept 2 — Dead Man's Deck (Arcade Gunner / Boarding Defense). |
| 1.00 | Développeur Solo | 01/11/2026 | GDD complet en français : cadrage FPS, boucle Chaos, bestiaire Vital/Désiré, HUD/UX et planning Décembre. |

---

## Partie 1 : Concept général (High-Level Concept)

### 1.1 Titre provisoire
**Dead Man's Deck** (sous-titre francophone : *Le Pont du Revenant*). Le titre annonce immédiatement la thématique pirate surnaturelle (*Dead Man*) et la contrainte spatiale qui fait la force du projet (*Deck* : toute l'action se concentre sur le pont supérieur d'un galion maudit).

### 1.2 Énoncé du concept (le jeu en un tweet)
> « Dead Man's Deck est un FPS arcade de défense par vagues où vous incarnez un Capitaine Revenant défendant à lui seul le pont de son galion contre des hordes de squelettes d'abordage. Pulvérisez leurs radeaux à coups de canons lourds grâce à la physique Unreal Chaos, puis dégainez sabre et pistolet à silex lorsque leurs grappins fracassent vos rambardes ! »

### 1.3 Genre(s) et public cible
- **Genre(s) :** FPS Arcade de Défense par Vagues (First-Person Wave Defense / Artillery & Slasher). Combine le tir balistique lourd sur postes fixes (canons, pierriers, harpons) et l'escarmouche nerveuse au corps-à-corps (sabre et pistolet à silex) dans une arène close type *Call of Duty: Zombies* et *Vermintide*.
- **Public cible :** joueurs PC (16–35 ans) friands d'action arcade immédiate, de maîtrise mécanique (rechargement actif, priorisation de cibles à 360°) et d'univers Dark Fantasy maritime.
- **Classification ESRB :** T (Teen / 13+) pour violence fantastique contre des squelettes et créatures abyssales, sans gore humain.

### 1.4 Points distinctifs (USP)
- **Double échelle de combat fluide :** bascule instantanée entre l'artillerie lourde en mer (détruire les radeaux avant l'impact) et le duel nerveux au sabre/pistolet sur le pont.
- **Destruction Unreal Chaos à impact tactique réel :** les 8 segments de rambardes du galion servent de barricades physiques. Intactes, elles ralentissent l'escalade des squelettes ; pulvérisées par les radeaux ou grappins, elles ouvrent une brèche immédiate jusqu'à leur réparation.
- **Double jauge de survie (Le Pacte du Revenant) :** le joueur perd si ses PV tombent à 0 **ou** si l'intégrité de la coque atteint 0 %, forçant des arbitrages constants entre sa propre survie et celle du navire.
- **Architecture « Scope-Smart » :** NavMesh restreint au seul pont du galion, garantissant zéro temps mort et une réalisation réaliste d'ici début décembre.

---

## Partie 2 : Conception du produit (Product Design)

### 2.1 Expérience du joueur, POV et fiction
**Point de vue :** première personne (FPS). Le joueur incarne le **Capitaine Revenant**, un pirate trahi dont l'âme est scellée dans l'**Autel des Âmes** au centre de son galion, ***L'Écorché***. Tandis que le navire traverse lentement la **Mer des Épaves** vers la **Brèche de l'Aube**, son ancien équipage de squelettes surgit de la brume pour couler le vaisseau et entraîner son âme dans les abysses.

### 2.2 Style visuel et sonore
- **Direction artistique :** Dark Cartoon Stylisé (croisement entre *Sea of Thieves* pour la lisibilité des silhouettes/proportions et *Dredge* pour l'atmosphère abyssale).
- **Palette :** contraste fort sous Lumen entre la brume volumétrique froide turquoise (`#14B8A6`) et la lueur chaude ambrée des lanternes de pont (`#F59E0B`) qui signale les postes de tir.
- **Références :** *Sea of Thieves* (lueur spectrale, lisibilité nocturne) · *Dredge* (brouillard oppressant, signaux rouges) · *Vermintide 2* (cadrage FPS viscéral face à une horde).
- **Design sonore 3D critique :** le son renseigne sur les menaces hors-champ : sifflement métallique d'un grappin à bâbord/tribord, craquement de charpente lors d'une brèche Chaos, clic-clac mécanique distinct du Rechargement Actif.

### 2.3 Monétisation, plateforme, technologie et échéancier
- **Monétisation :** achat unique Premium Indie PC (Steam / Itch.io) à 12,99 $ CAD (9,99 $ USD), sans microtransactions Pay-to-Win. Extensions par chapitres thématiques à 4,99 $ (nouveaux navires et bestiaires).
- **Technologie :** PC (Windows/Mac), Unreal Engine 5 (First-Person Template, Chaos Destruction, NavMesh local sur le pont).

| Jalon | Date cible | Livrables |
|---|---|---|
| M1 — Engine & Greybox | 8 nov. 2026 | Greybox du galion, contrôleur FPS, prise en main et tir balistique des canons de bordée. |
| M2 — First Playable | 15 nov. 2026 | Approche radeau sur spline, destruction Chaos radeau/rambarde, NavMesh + 1 squelette et combat sabre/pistolet. |
| M3 — Core Loop Complete | 22 nov. 2026 | Directeur de vagues, PV Coque + Joueur, réparation des rambardes, Rechargement Actif et Autel des Âmes. |
| M4 — Alpha (Look & Feel) | 29 nov. 2026 | Habillage Dark Cartoon, brouillard Lumen, audio 3D spatialisé, HUD complet et vague finale. |
| M5 — Gold Master | Début déc. 2026 | Équilibrage des vagues 1 à 8+, optimisation 60 FPS, menus de victoire/défaite et build packagé. |

---

## Partie 3 : Conception détaillée et systèmes de jeu

### 3.1 Boucle de jeu principale (Core Loop)
1. **Repérer (360°)** — identifier les radeaux dans la brume et les grappins à l'oreille.
2. **Artillerie** — tirer au canon / pierrier + Rechargement Actif.
3. **Impact Chaos** — radeau pulvérisé en mer **ou** rambarde fracassée.
4. **Escarmouche** — sabre et pistolet à silex pour nettoyer le pont.
5. **Accalmie** — réparer les brèches et s'améliorer à l'Autel des Âmes.

### 3.2 Objectifs, progression et session type
Une traversée complète dure **15 à 20 minutes (8 à 10 vagues)**, séparées par des accalmies de **25 secondes**.

**Exemple :** à la Vague 1, le joueur entend la cloche et repère un radeau à tribord. Il empoigne le canon (**E**), ajuste sa hausse et tire (**Clic Gauche**). Le boulet fracasse le radeau en une douzaine de planches physiques (Chaos). Pendant son Rechargement Actif (**R** dans la fenêtre dorée), un second radeau percute bâbord (**-5 % Coque**) et brise la rambarde. Trois squelettes grimpent par la brèche : le joueur lâche le canon, abat le premier au pistolet (**Clic Droit**) et tranche les deux autres au sabre (**Clic Gauche**). En fin de vague, il récolte les **Éclats d'Âmes**, reconstruit la rambarde (**F**) et active l'Autel des Âmes pour débloquer le pierrier à mitraille.

### 3.3 Systèmes de jeu et inventaire de production (style DOOM Bible)
Priorités : **V = Vital** (indispensable au build final), **D = Désiré** (si avance en semaine 4), **N = Non-Vital** (bonus).

| Catégorie | Priorité | Élément / comportement |
|---|---|---|
| Ennemi / Physique | **VITAL** | **Radeau d'abordage** (Chaos Geometry Collection) : avance sur spline vers le galion, explose en éclats sous un boulet de canon. |
| Ennemi (Base) | **VITAL** | **Squelette Épéiste** : escalade la rambarde (lent si intacte, immédiat si brisée) et attaque le joueur ou la coque sur le NavMesh. |
| Ennemi (Prioritaire) | **VITAL** | **Squelette Sapeur** (baril de poudre) : aura rouge ; inflige -15 % à la coque au contact, mais explose en chaîne si tiré à distance. |
| Ennemi / Boss | DÉSIRÉ | **Sirène des Abysses** (distance), **Brute à Ancre** et **Tentacules du Léviathan d'Os** (boss de la vague finale). |
| Armes & Pont | **VITAL** | 4 canons lourds de bordée, sabre d'abordage + pistolet à silex FPS, 8 rambardes Chaos réparables, Autel des Âmes. |
| Armes de Pont+ | DÉSIRÉ | Pierrier à mitraille (x2) et harpon pivotant de proue (x1) déblocables via l'Autel des Âmes. |

### 3.4 Architecture du pont et interface (UX / HUD)
- **Plan du pont de *L'Écorché* :** NavMesh central, 4 canons de bordée, harpons, rambardes destructibles et Autel au centre (voir Figure 3 du PDF).
- **HUD FPS :** jauge de Coque du galion et état des rambardes en haut, Rechargement Actif au centre, PV / Âmes en bas à gauche, alertes d'abordage rouges sur les bords (voir Figure 4 du PDF).

#### Contrôles

| Action | Clavier / Souris | Manette | Description |
|---|---|---|---|
| Déplacement / Visée | WASD + Souris | Sticks G / D | Déplacement FPS rapide sur le pont ; oriente le fût lorsqu'un canon est empoigné. |
| Sabre / Tir canon | Clic Gauche | RT / R2 | Combo de sabre (maintenir = estoc repoussant par-dessus bord) ; tire au canon en mode artillerie. |
| Pistolet à silex | Clic Droit | LT / L2 | Tir rapide de la main gauche pour éliminer un sapeur ou finir une cible à moyenne portée. |
| Rechargement Actif | R | X / Carré | Appuyer une 2e fois dans la zone dorée : recharge 50 % plus vite + bonus de dégâts. |
| Artillerie / Réparer | E / F (maintenir) | Y / B | E : prendre/quitter un canon. F : réparer une rambarde brisée ou ouvrir l'Autel des Âmes. |
