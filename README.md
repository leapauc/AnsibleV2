# Ansible-FinalProject
Mettre en oeuvre un déploiement automatisé avec Ansible pour préparer l’installation de la plateforme d’elearning Moodle en configurant deux machines virtuelles distinctes

## DEPENDANCES:
- vagrant
Il est à prévoir une installation de vagrant pour pouvoir faire l'ensemble de la routine de déploiement automatisé.
https://developer.hashicorp.com/vagrant/install

## ETAPES:
1. Créer le fichier Vagrantfile
   Cf. fichier Vagrantfile

   lancer dans la dossier où il y a le fichier :
   ```
   vagrant up
   ```
3. Créer la clé ssh
   Via vagrant en ce connectant à master :

   ```
   vagrant ssh master
   ssh-keygen
   cat .ssh/id_rsa.pub
   ```

   copier le contenu

   pour sortir du server master
   ```
   exit
   ```
   Ce connecter à master via "vagrant ssh master"
   
5. Ajouter la clé ssh public à chaque VM
   utiliser la connection par vagrant au VM
   exemple pour la VM1 :

   ```
   vagrant ssh VM1
   vi .ssh/authorized_keys
   ```

   coller le contenu

   ```
   sudo vi /etc/ssh/sshd_config
   ```

   uncomment ces lignes

   ```
   PubkeyAuthentication yes
   AuthorizedKeysFile .ssh/authorized_keys
   ```
   Lancer la commande suivante pour relancer ssh
   ```
   sudo systemctl restart ssh
   ```
   
   pour sortir du server VM1
   ```
   exit
   ```
   Faire pareil pour VM2

7. Installer python3 - python3-pip

   ```
   sudo apt update
   sudo apt install python3 python3-pip
   sudo pip install ansible
   ```

8. Fichier hosts sur le serveur

   ```
   [web]
   web ansible_host=192.168.56.2

   [db]
   db ansible_host=192.168.56.3
   ```

6. Rôles de Ansible Galaxy
   Lancer cette commande pour récuprer le role en ligne pour installation de mysql :

   ```
   ansible-galaxy role install geerlingguy.mysql

   ```
   Documentation disponible : https://galaxy.ansible.com/ui/standalone/roles/geerlingguy/mysql/ 

7. Lancer le playbook de configuration global
   lancer la commande suivante et en indiquant, sur la demande de la console, le mot de passe pour l'accès au vault
   ```
   ansible-playbook -i hosts playbook.yml --ask-vault-pass

   ```

