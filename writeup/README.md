#**Challenge S4-1**

##**Introduction :**

	Ce challenge était compliqué pour moi, je n’avais jamais abordé le ftp, j’ai dû passer beaucoup de temps à travailler dessus.

	On nous donne un fichier fic.pcapng, et l’indice nous annonce 3 étapes à suivre.


##**I°/ L’analyse du pcapng :**

	C’est une capture réseau basique, mais on peut voir dans les statistiques un échange de data FTP.

![alt text](https://github.com/T-Ratnosaure/fic-S4-1/writeup/image1.png "Image 1")
![alt text](https://github.com/T-Ratnosaure/Writeups/fic-S4-1/image2.png "Image 2")

	
On ne va alors sélectionner que cette trame étrange, et on voit en bas une connection à un serveur ftp avec le nom d’utilisateur et le mot de passe.
	
writeup/
	Aïe coup dur, lorsque l’on veut s’y connecter, on est instantanément kické.

	Je vais donc essayer de récupérer les fichiers avec wget. Voici la commande utilisée : 
		**wget ftp://fic2020tr_1:cdaisifi-2020@ftp-fic2020tr.alwaysdata.net**

##**II°/ L’analyse des fichiers :**


	On se retrouve avec 3 fichiers : Credits.txt qui comprend la fin de la documentation de volatility, fic.txt qui contient une wordlist, ainsi que settings.xml qui contient des données.

	On y voit la ligne 	**cpassword="8ZuFA0CxVmqxiN86jwdS7cJ9xFTZMxiZmLIhlUBZHp7vEOcv88HbvORNIo8pQ/E9iuNzk2omHvJb7p7lvAYN7Q"**

	On se souvient alors d’un challenge, et on exécute gpp-decrypt sur ce cpassword, et cela nous donne une image.

##**III°/L’analyse de l’image :**

	On a une image ainsi qu’une wordlist, on va donc utiliser steghide, ainsi qu’un joli script ( <3 Bdenneu ).

	
```bash


stegfile=$1
dico=$2

for line in $(cat $2); do
	steghide --extract -sf $stegfile -p "$line" ;
	echo "$line"
done
exit 0```

Et boom on obtient le flag !!!
