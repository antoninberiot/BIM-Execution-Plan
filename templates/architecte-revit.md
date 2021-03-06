{% extends "/templates/softwares/revit.md" %}
{% set categorie_logiciel = "Revit 2017.4" %}

{# Donne un exemple de découpage pour le lot #}
{% block lot_decoupage %}Votre modèle peut ainsi être séparé en 2 modèles, Façades et Intérieur.{% endblock %}

{# Donne des recommendation de modélisaiton générales propre au lot#}
{% block lot_specifique_generalites %}

De manière générale, dans les modèles Architecte les éléments de structure (dalles, poteaux, poutres, voiles ...) devront être modélisées sur un sous-projet à part de manière à pouvoir les isoler facilement.
Dans le cas où des intervenants spécifiques pour les lots façade et décoration soient soient présents dans l'équipe, de principe devra s'appliquer également pour les éléments de façade et de décoration.

{% endblock %}

{# Ajoute la table des matières pour le lot#}
{% block specific_toc %}* [Plans de surface](#surface)
* [Pièces](#piece)
* [Logements](#logements)
* [Places de parking](#parking)
* [Modélisation des murs](#murs)
* [Placards](#placards){% endblock %}

{# Décrit les recommendations de modélisation spécifiques au lot et au logiciel #}
{% block lot_specifique_content %}

### Modélisation des plans de surfaces{#surface}

Les Surface Hors Œuvre Brut \(SHOB\), Surface Hors Œuvre Nette \(SHON\) et Surface de Plancher \(SDP\) sont calculées en additionnant les différents types de surfaces du projet. De plus, la représentation des surfaces de parkings extérieurs est attendue.

#### Modélisation

L’ensemble de ces surfaces SHOB/SHON/SDP est représenté à l’aide d’un unique plan de surface par niveau :

![Plan de surface](/02_Modelisation/02_architecte/images/SURFACE_01.PNG)

Les surfaces modélisées doivent couvrir l'ensemble de l'emprise du projet, à tout les niveaux. Le niveau N00 (Rez-De-Chaussé) doit également contenir les surfaces extérieures au bâtiment lui-même (VRD, parking extérieur, ...).

Chaque surface dessinée dans ces plans doit avoir les propriétés suivantes :

| Propriété | Valeurs possibles | Explication |
| :--- | :--- | :--- |
| Nom | Voir [« Noms des surfaces »](#nom_surface) ci-dessous | Cette propriété indique le type de surface, suivant la décomposition décrite ci-dessus. |
| Commentaire | Voir [« Types de surfaces »](#types_surface) ci-dessous| Cette propriété indique la destination des surfaces réalisées. |

Si un même niveau contient des surfaces ayant des usages différents (par exemple, surface de plancher de commerce et de logement), chaque usage doit être réprésenté par une surface distincte.

#### Exemples

##### Niveau de parking

![Niveau de parking](/02_Modelisation/02_architecte/images/Surfaces_ExempleNiveauParking.png)

##### Niveau courant

![Niveau courant](/02_Modelisation/02_architecte/images/Surfaces_ExempleNiveauCourant.png)

#### Noms des surfaces{#nom_surface}

{% include "/00_Referentiel/NomDesSurfaces.md"  %}

#### Types de surface{#types_surface}

{% include "/00_Referentiel/NomDesProduits.md"  %}

### Modélisation des pièces{#piece}

Les {% if book.bu == "logement" %}Surfaces Habitables (S.H.A.B.){% else %}Surfaces Utiles Brutes Locatives \(SUBL\), Surfaces Utiles Brutes Bureaux \(SUBB\), Surfaces Utiles Nettes \(SUN\) et Surfaces Nettes Bureaux \(SNB\){% endif %} sont calculées à partir de la modélisation des pièces du projet.

L’ensemble des locaux du projet doivent être présents dans la maquette numérique. En plus des locaux « nobles » du programme, cette modélisation doit inclure tous les autres types de locaux, tel que les circulations, les locaux techniques, les gaines techniques, …

Les locaux doivent être représentés et décomposés en locaux fonctionnels {% if book.bu == "logement" %}\(Chambre, Séjour, Hall, …\){% else %}\(Bureau, Salle de Réunion, Hall, …\){% endif %}, même si ces locaux appartiennent à un espace physique plus important. Par exemple, {% if book.bu == "logement" %}un séjour et une cuisine{% else %}un hall et une cafétéria{% endif %} ouverts l'un sur l'autre devront être représentés comme deux locaux distincts.

Les locaux doivent être modélisés depuis le sol fini jusqu’au plafond fini. En l’absence de faux-plafonds, les locaux doivent être modélisés jusqu’à la hauteur libre prévue par le programme. Les locaux doivent être identifiés par leur nom, en suivant les valeurs du tableau "Nom des pièces" ci-dessous.

#### Modélisation

Dans Revit, ces locaux doivent être modélisé à l’aide de l’outil Pièce :

![Pièces](/02_Modelisation/02_architecte/images/SURFACE_02.PNG)

Les propriétés suivantes sont à compléter :

| Propriété | Valeurs possibles | Explication |
| :--- | :--- | :--- |
| Nom | Voir [« Nom des pièces »](#Nom_pieces) ci-dessous | Cette propriété indique le type de local, suivant la décomposition décrite ci-dessus. |
| Commentaire | Voir [« Destination des pièces »](#destination_piece) ci-dessous| Cette propriété indique la destination des pièces réalisées. |
| Décalage limite | Hauteur libre \(en m\) | Cette propriété permet d’indiquer la hauteur libre dans le local. Les propriétés « Niveau » et « Limite supérieure » doivent donc également avoir la même valeur. |

On completera également le revêtement de sol :

| Propriété | Valeurs possibles | Explication |
| :--- | :--- | :--- |
| Finition du sol | Voir [« Revêtements de sols »](#revêtements_sols) ci-dessous | Cette propriété indique le type de revêtement de sol dans la pièce. |

#### Exemple

![Propriétés des pièces](/02_Modelisation/02_architecte/images/pieces_proprietes_logement.png)

#### Pièces sous 1,80 m

On découpe la pièce en séparant les espaces sous 1,80 m. On appele ces espaces "COMBLE".

#### Nom des pièces{#Nom_pieces}

Le tableau ci-dessous liste les noms de pièces à utiliser sur l'operation:

{% include "/00_Referentiel/NomDesPieces.md" %}

#### Revêtements de sols{#revêtements_sols}

{% include "/00_Referentiel/TypesDeRevetements.md" %}

#### Destination des pièces{#destination_piece}

Le tableau ci-dessous liste les destinations possible pour une pièces:

{% include "/00_Referentiel/NomDesProduits.md" %}

### Modélisation des logements{#logements}

Les pièces constituants un logement doivent être regroupées ensembles. Il est nécéssaire d'ajouter les propriétés suivantes aux pièces à l'aide de trois paramètres partagés :

* ZoneName
* ZoneObjectType
* ZoneDescription.

Ces trois paramètres permettent de créer des IfcZones au moment de l'export IFC

| Propriété | Valeurs possibles | Explication |
| :--- | :--- | :--- |
| ZoneName | Voir [« Noms des logements »](#nom_logement) ci-dessous | Cette propriété permet de regrouper les pièces d'un logement.|
| ZoneDescription | Voir [« Typologie des logements »](#typologie_logement) ci-dessous | Cette propriété permet de préciser la typologie du logement (T1, T2, ...).|
| ZoneObjectType | Voir [« Collections »](#collection) ci-dessous  | Cette propriété permet de préciser la collection du logement.|

![Zones](/02_Modelisation/02_architecte/images/zones_proprietes_logement.png)

![Regroupement en logements](/02_Modelisation/02_architecte/images/RegroupementEnLogements.png)

#### Nom des Logements{#nom_logement}

{% include "/00_Referentiel/NomDesLogements.md"  %}

#### Typologie des logements{#typologie_logement}

{% include "/00_Referentiel/TypologieDesLogements.md"  %}

#### Collections{#collection}

{% include "/00_Referentiel/Collection.md"  %}

### Modélisation des places de parking{#parking}

Les places de parking sont modélisées à l’aide d’une famille de la catégorie Parking (Par exemple, la famille "Place de parking.rfa" incluse avec Revit). La propriété suivante est alors à compléter :

| Propriété | Valeurs possibles | Explication |
| :--- | :--- | :--- |
| Commentaire | Un numéro unique | Cette propriété permet d’identifier la places de parking. |

![Parking](/02_Modelisation/02_architecte/images/Parking.PNG)

### Modélisation des façades de placards{#placards}

Les placards doivent être modélisé à l'aide de la famille de placard fournie, disponible [en cliquant ici](https://github.com/BIM-Bouygues-Immobilier/BIM-Execution-Plan/raw/master/02_Modelisation/02_architecte/images/Placard.rfa)

Cette famille de placard, basée sur une ligne, permet de représenter les façades de placards. La profondeur du placard est un paramètre de type.

![Placard](/02_Modelisation/02_architecte/images/Placard.png)

### Modélisation des murs{#murs}

{% include "/categories/murs.md"  %}

### Modélisation des poteaux{#poteaux}

{% include "/categories/poteaux.md"  %}

{% endblock %}