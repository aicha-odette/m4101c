#Ces variables servent à préciser le compilateur que l'on veut utiliser
#ainsi que les paramètres de compilation
CC=gcc
LD=gcc
CFLAGS=-Wall -W -Werror
LDFLAGS=

#Le nom de l'executable à fabriquer
EXE=pawnee

#Les variables HEADERS, CFILES et OBJS vont contenir respectivement
#la listes des fichiers .h .c et le nom des fichiers .o à fabriquer
#On utilise la directive particulière $(wildcard...) qui permet
#de construire automatiquement une liste de fichiers
HEADERS=$(wildcard * .h)
CFILES=$(wildcard *.c)
#Cette construction de variable veut dire : remplacer la ".c" par 
#".o" dans la variable CFILES
#Ceci nous permet de construire la liste des fichiers .o à fabriquer
OBJS=$(CFILES:.c=.o)

#Meme utilisation que précédemment. On précise les régles qui
#ne fabrique pas de fichier du nom de leur cible
.PHONY: all clean mrproper

#La régle par défaut déclenche la fabrication de l'executable
#par dépendance
all: $(EXE)

#Cette régle permet de construire l'executable. Elle dépend des fichiers
#.o et effectue l'édition de lien. Rien de nouveau icic
$(EXE): $(OBJS)
	$(LD) $^ $(LDFLAGS) -o $@
#Cette règle permet de construire automatiquement les règles
#de compilation pour chacun des fichiers .c
#l'option -MM de gcc analyse un fichier .c et
#affiche sur sa sortie standard une règle compatible
#make pour le compiler
#Ceci permet d'ajouter automatiquement les fichiers .h aux dépendances
#des fichier .o à construire. Ainsi, en modifiant un fichier .h 
#tous les fichiers .c qui incluent ce fichier sont recompilés
#Apres votre premiere complation, regardez le contenu du fichier
#makefile.dp généré afin de comprendre exactement de quoi il retourne
makefile.dep: $(CFILES) $(HEADERS)
	$(CC) -MM $(CFILES) > $@

#cette regle efface le fichier de dépendances et les fichiers .o
clean :
	$RM $(OBJS) makefile.dep

#cette regle effectue la precedente et efface en plus l'executable
mrproper: clean
	$(RM) $(EXE)

#On inclue le fichier de dependance qui va contenir les regles
#de construction des fcihiers .o
#sil existe pas , make invoque la regle qui l'a pour cible
include makefile.dep
