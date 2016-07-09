# Char

Un [Char](http://crystal-lang.org/api/Char.html) représente un [point de code](https://fr.wikipedia.org/wiki/Point_de_code)
[Unicode](http://fr.wikipedia.org/wiki/Unicode).
Il occupe 32 bits.

Il est créé en encadrant un caractère UTF-8 entre guillemets simples.

```crystal
'a'
'z'
'0'
'_'
'あ'
```

Vous pouvez utiliser un antislash pour protéger certains caractères:

```crystal
'\'' # guillement simple
'\\' # antislash
'\e' # échappement
'\f' # saut de page
'\n' # nouvelle ligne
'\r' # retour chariot
'\t' # tabulation
'\v' # tabulation verticale
```

Vous pouvez utiliser un antislash suivi par au plus trois chiffres pour représenter un point de code en octal:

```crystal
'\101' # == 'A'
'\123' # == 'S'
'\12'  # == '\n'
'\1'   # point de code 1
```

Vous pouvez utiliser un antislash suivi d'un *u* et quatre caractères hexadécimaux pour représenter un point de code unicode:

```crystal
'\u0041' # == 'A'
```

Vous pouvez utiliser des parenthèses bouclées pour représenter un hexadécimal jusqu'à 6 nombres (0 à 10FFFF):

```crystal
'\u{41}'    # == 'A'
'\u{1F52E}' # == '🔮'
```
