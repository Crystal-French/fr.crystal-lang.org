# Documentation de code

Les commentaires de documentation Crystal utilisent un sous-ensemble de [Markdown](https://daringfireball.net/projects/markdown/).

* La documentation devrait être positionnée juste en dessous des définitions de classes,
modules et méthodes. Ne laissez aucun blanc entre eux.

```crystal
# Une licorne est un **animal légendaire** (voir le `Legendary` module) qui fut
# descrit à l'antiquité comme la bête avec une large, corne en spirale
# sortant de son front.
class Unicorn
end

# Mauvais: commentaire attaché à aucune classe.

class Legendary
end
```

* La documentation d'une méthode est incluse dans le résumé de la méthode et dans les détails de la méthode.
Le premier inclut seulement la première ligne, le second inclut la documentation entière.
Pour résumer, il est préférable de:

  1. Déclarer le but ou l'utilité d'une méthode dans la première ligne.
  2. Compléter cela avec des détails et usages dans ce qui suit.

Par exemple:

``````crystal
# Retourne le nombre defini de cornes
#
# ```
# Unicorn.new.horns # => 1
# ```
def horns
  @horns
end
``````

* Utilisez la troisième personne: `Returns the number of horns this unicorn has` Au lieu de `Return the number of horns this unicorn has`.

* Les noms de paramètres devraient être en *italique* (encadrés par un astérisque `*` ou des soulignés `_`):

```crystal
# Crée un licorne avec un nombres definie de *cornes(horns)*.
def initialize(@horns = 1)
  raise "Not a unicorn" if @horns != 1
end
```

* Des blocs de code avec du code Crystal peuvent être encadrés par des triples quotes inversées ou indentés par quatre espaces.

``````crystal
# ```
# unicorn = Unicorn.new
# unicorn.speak
# ```
``````

ou

```crystal
#     unicorn = Unicorn.new
#     unicorn.speak
```

* Des blocs de texte, par exemple pour afficher la sortie d'un programme, doivent être encadrés par des triples quotes inversées suivies par le mot clé "text".

``````crystal
# ```text
# "I'm a unicorn"
# ```
``````

* Pour se lier automatiquement aux autres types, encadrez-les par de simples quotes inversées.

```crystal
# the `Legendary` module
```

* Pour se lier automatiquement à des méthodes du type courant documenté, utilisez un hash comme `#horns` ou `#index(char)`,
et encadrez-le avec une simple quote inversée.

* Pour se lier automatiquement avec des méthodes d'autres types, utilisez `OtherType#method(arg1, arg2)` ou simplement `OtherType#method`,
et encadrez-le avec une simple quote inversée.

Par exemple:

```crystal
# Check the number of horns with `#horns`.
# See what a unicorn would say with `Unicorn#speak`.
```

* Pour afficher la valeur d'une expression dans des blocs de code, utilisez `#=>`.

```crystal
1 + 2             # => 3
Unicorn.new.speak # => "I'm a unicorn"
```

* Utilisez `ditto` pour ré-utiliser le même commentaire qe la déclaration précédente.

```crystal
# ditto
def number_of_horns
  horns
end
```

* Utilisez `:nodoc:` pour cacher les déclarations publiques de la documentation générée.
Les méthodes privées et protégées sont toujours cachées.

```crystal
class Unicorn
  # :nodoc:
  class Helper
  end
end
```

### Flagging Classes, Modules, and Methods

Suivant un mot-clé valide, Crystal va automatiquement générer des drapeaux visuels afin d'aider à mettre en valeur les
problèmes, notes et/ou les possibles erreurs.

Les mots-clés drapeau supportés sont:

- BUG
- DEPRECATED
- FIXME
- NOTE
- OPTIMIZE
- TODO

Les mots-clés doivent se trouver en premier sur leur ligne et doivent être en lettres capitales.
Un signe deux-points final est à privilégier pour la lisibilité.

````crystal
# Faite parler la licorne sur la sortie standard
#
# NOTE: En temps normale les licornes ne parle pas, mais celle la est speciale
# TODO: vérifier si la licorne dort et signalé une exception si la licorne n'éest pas en mesure de parler
# TODO: Crée une nouvelle methode `speak` qui prend un argument une chaine de charactére et qui l'affiche
  puts "I'm a unicorn"
end

# Faite parler la licorne sur la sortie standard
#
# DEPRECATED: Utilise `speak`
def talk
  puts "I'm a unicorn"
end
`````

### Utilisez le formateur de code de Crystal

Le formateur de code inclut dans Crystal peut être utilisé non seulement pour formater votre code,
mais aussi pour formater les exemples de code inclus dans les blocs de documentation.

Il est exécuté automatiquement à l'invocation de `crystal tool format`,
qui formate automatiquement tous les fichiers `.cr` du dossier courant.

Pour formater un fichier en particulier:

```
$ crystal tool format file.cr
```

Pour formater tous les fichiers `.cr` d'un dossier:

```
$ crystal tool format src/
```

Utilisez cet outil pour harmoniser le style de codage et pour soumettre des
améliorations de documentation au projet Crystal.

Le formateur est également rapide, ainsi peu de temps est perdu si vous formatez
un projet entier au lieu d'un unique fichier.

### Un exemple complet

``````crystal
# A unicorn is a **legendary animal** (see the `Legendary` module) that has been
# described since antiquity as a beast with a large, spiraling horn projecting
# from its forehead.
#
# To create a unicorn:
#
# ```
# unicorn = Unicorn.new
# unicorn.speak
# ```
#
# The above produces:
#
# ```text
# "I'm a unicorn"
# ```
#
# Voir le nombre de corne avec `#horns`.
class Unicorn
  include Legendary

  # Creates a unicorn with the specified number of *horns*.
  def initialize(@horns = 1)
    raise "Not a unicorn" if @horns != 1
  end

  # Retourne le nombres de cornes que detient la licorne
  #
  # ```
  # Unicorn.new.horns # => 1
  # ```
  def horns
    @horns
  end

  # ditto
  def number_of_horns
    horns
  end

  # Soyez sur d'afficher le message sur la sortie standard
  def speak
    puts "I'm a unicorn"
  end

  # :nodoc:
  class Helper
  end
end
``````

### Générer la Documentation

Pour générer la documentation d'un projet, invoquez `crystal doc`. Cela va créer un dossier `doc`, avec le point d'entrée `doc/index.html`.
Tous les fichiers du dossier racine `src` seront pris en considération.
