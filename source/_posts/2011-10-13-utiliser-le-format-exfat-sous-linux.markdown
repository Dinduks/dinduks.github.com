---
comments: true
date: 2011-10-13 00:00:03
layout: post
slug: utiliser-le-format-exfat-sous-linux
title: Utiliser le format exFat sous Linux
categories:
- Tutorials
tags:
- exfat
- linux
- ubuntu
---

Bonjour,

Si comme moi vos disques durs externes sont formatés en exFat (pour gérer les fichiers de plus de 4Go par exemple), et que vous utilisez souvent Linux, vous savez sûrement que le système de fichiers de Microsoft n'est pas géré nativement par Linux.  
Il y a par contre une solution, facile mais difficilement trouvable sur le net, et c'est celle que je partagerai avec vous.

Pour cela, il faut installer FUSE:

    sudo apt-add-repository ppa:relan/exfat
    sudo apt-get install fuse-exfat

Ensuite, branchez votre disque dur si ce n'est déjà fait, et vérifiez le nom de votre lecteur avec la commande suivante:

    more /proc/partitions

Une liste de tous les périphériques de stockage sera alors affichée, votre disque dur externe sera sûrement dans la fin de la liste, vous le reconnaîtrez grâce à sa taille.
Notez son nom, on va utiliser _/dev/sdc1_ dans cet exemple.

Maintenant créer un répertoire vide pour y monter votre DD:

    cd /mnt
    sudo mkdir usbdrive/

Et montez le disque dur:

    sudo mount -t exfat /dev/sdc1 usbdrive

Et voilà, votre lecteur devra s'afficher sur le bureau. Si ce n'est pas le cas, accédez à /mnt/usbdrive avec votre explorateur de fichier.

Si vous avez terminé d'utiliser votre disque dur et que vous voulez le démonter, un simple `umount` suffit:

    umount /mnt/usbdrive

Tutoriel basé sur: [http://apcmag.com/how-to-enable-exfat-in-ubuntu.htm](http://apcmag.com/how-to-enable-exfat-in-ubuntu.htm).
