# Malware Project (Projet 3A Mines)

## Informations supplémentaires

Programme informatique utilisant des techniques d'obfuscation et d'automodification sur un système Windows XP 32 Bits.

Principe de base, effectuer un echo.

### Easter Egg

Le programme aura une réponse spéciale si l'input se résume à un unique 42.
### Principe de fonctionnement

une fonction est injectée dans la fonction createfilew de la dll kernel32. Elle incrémente la valeur d'une variable Z à travers un pointeur définit précédemment.  

Au cours de l'éxécution CreatefileW sera appelé plusieurs fois, et différentes conditions sur la valeur de Z feront effectuer des jumps à différents endroits du code. Les jumps successifs font que l'injection de la fonction précédemment citée se fait après un premier createfileW explicite, qui ne comptera donc pas dans l'incrémentation de Z. 

Le code manipule plusieurs fois un même fichier, et va à un moment effectuer un CopyFileW. Sous certaines conditions d'état des fichiers manipulés, CopyFileW va appeler un certain nombre de fois CreateFileW (ici, 4 fois), le programme s'assure d'avoir toujours les mêmes conditions d'état pour ces fichiers pour assurer la stabilité à chaque éxécution. En ajoutant un 5ème appel au repassage du code sur le premier CreateFileW, la condition qui se lève en première sera z == 5 (Ici stocké sous une valeur "5 xor Key").


Enfin, les fonctions primaires (printf, system, strlen, strcpy etc) sont pointées dynamiquement grâce à GetProcAddress, et leur nom n'apparaîtra jamais dans l'executable final. Si la fonction apparait (exemple, printf en fin d'éxécutable), c'est un leurre.

### Encryptage des chaines de caractères

Les chaines de caractères sont quasiment toutes cryptées grâce à un algorithme de type RC4 écrit en Assembly.  

### Easter Eggs  

Certains fichiers sont manipulés pendant l'éxécution du code, des phrases cachées y sont écrites. Le seul moyen de voir ce qu'il y a dedans est d'utiliser un debuggeur sur l'éxécutable. 

Le programme est "pudique", mieux vaut sauvegarder toutes vos autres tâches en cours avant d'utiliser un debuggeur sur lui car il n'aime pas trop cela... 

### Reel code source

Le code dans ce repository est rendu illisible volontairement. Envoyez un mail à **julienelk@gmail.com** pour obtenir l'accès au repo privé comptenant le code source en claire.