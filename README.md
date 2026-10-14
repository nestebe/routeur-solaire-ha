# 🌞 Routeur solaire Home Assistant

**🇫🇷 Français** · [🇬🇧 English](README.en.md)

Chauffer le ballon d'eau chaude avec le surplus solaire, puissance modulée de 0 à 2200 W, pilotée par Home Assistant.

## Matériel

| Composant | Rôle |
|---|---|
| **LSA-H3P40YB** 40 A, version **sans « -F »** | Régulateur de puissance |
| **Shelly Dimmer 0/1-10V PM Gen3** | Commande 0-10 V du LSA, piloté en Wi-Fi par HA |
| Radiateur alu (LCTC H-110) + pâte thermique | Refroidissement du LSA |
| Coffret IP65, profondeur ≥ 150 mm, avec grilles d'aération | Protection |
| Fusible 2 A | Protection du Shelly |
| Mesure réseau (ZLinky TIC ou Shelly Pro EM) | Surplus vu par HA |
| Disjoncteur 20 A + différentiel 30 mA type A, câble 2,5 mm² | Circuit du ballon d'eau chaude |

⚠️ La version **LSA-H3P40YB-F** ne fonctionne pas avec une commande externe.

## Schéma

![Schéma de câblage](images/cablage-fr.svg)

![Bornier de commande](images/bornier-commande-fr.svg)

## Photos

<table>
  <tr>
    <td align="center"><img src="images/photo-prototype.jpg" alt="Montage d'essai" width="380"><br><em>Essai sur planche</em></td>
    <td align="center"><img src="images/photo-coffret.jpg" alt="Montage final" width="380"><br><em>Montage final</em></td>
  </tr>
</table>

## Réglages

- Shelly : mode **1-10V**, min brightness on toggle **0**, pas de remapping min/max.
- Régulation HA : toutes les 20 s, ajuster le Shelly pour garder ~200 W d'injection. Point de départ : [YaSolR de Mathieu Carbou](https://yasolr.carbou.me/blog/2024-07-01_shelly_solar_diverter).

## Calibrer le Dimmer

Le LSA ne chauffe pas sur toute la plage du Shelly. Il faut repérer à partir de quel pourcentage il commence à chauffer, et à partir duquel il est à fond.

Fais-le avec le ballon froid, sinon le thermostat coupe et tu ne verras rien. Et fais d'abord le test avec une ampoule.

1. Monte le Shelly par paliers : 10 %, 20 %, 25 %, 30 %, 35 %, 40 %, 50 %… jusqu'à 100 %. Attends une dizaine de secondes à chaque fois.
2. À chaque palier, note la puissance consommée par le ballon (sur ta mesure réseau ou avec une pince ampèremétrique).
3. Le premier pourcentage où le ballon se met à chauffer (environ 100 W), c'est ton minimum.
4. Le pourcentage à partir duquel la puissance ne monte plus, c'est ton maximum.

Chez moi, le ballon commence à chauffer vers 30 % (environ 100 W) et il est à fond vers 90 %. Entre les deux, chaque pourcent ajoute environ 38 W. Dans Home Assistant, la régulation reste toujours entre ces deux valeurs.

## Sécurité

- Travail hors tension. Thermostat du ballon d'eau chaude **toujours en série**, jamais shunté.
- Terre sur le ballon d'eau chaude et le radiateur du LSA.
- Le LSA n'a pas de protection thermique : radiateur et coffret ventilé obligatoires.
- Test d'abord avec une ampoule à filament 60 W.

## Contact

devestebe@gmail.com
