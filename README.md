# DevSecOps-Pipeline-Jenkins-SonarQube-Trivy-Command
#Mise à jour des listes de paquets
sudo apt update -y
# Téléchargement de la clé GPG du dépôt Adoptium
wget -qO - https://packages.adoptium.net/artifactory/api/gpg/key/public | sudo apt-key add –
Ajout du dépôt Adoptium
sudo echo "deb https://packages.adoptium.net/artifactory/deb focal main" | sudo tee /etc/apt/sources.list.d/adoptium.list
#Mise à jour des listes de paquets (à nouveau)
sudo apt update
# Installation d'OpenJDK 17 (JDK et JRE)
sudo apt install openjdk-17-jdk openjdk-17-jre
# Installation de temurin-17
sudo apt install temurin-17-jdk
# Vérification de l'installation de Java
java –-version
# Installation de curl 
sudo apt install curl
## Installation du serveur Jenkins ##
# Installation de la clé Jenkins
sudo curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
# Ajout du dépôt Jenkins
sudo echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
# Mise à jour des listes de paquets (à nouveau)
sudo apt update -y
# Installation de Jenkins
sudo apt install jenkins -y
# Démarrage du service Jenkins
sudo systemctl start jenkins
# Vérification du statut de Jenkins
sudo systemctl status jenkins
## Installation de SonarQube ##
# Installation de Docker
sudo apt install docker.io -y
# Ajout de l'utilisateur 'oumaima' au groupe Docker
sudo usermod -aG docker oumaima
# (Facultatif) Ajout de l'utilisateur 'jenkins' au groupe Docker
sudo usermod -aG docker jenkins
# Actualisation des appartenances aux groupes
newgrp docker
#Accorder des permissions de lecture, d'écriture et d'exécution (777) 
au socket Docker
sudo docker run -d --name sonar -p 9000:9000 sonarqube:lts-community
# Affichage de tous les conteneurs Docker, y compris ceux arrêtés
sudo docker ps -a
## Installation de Trivy ##
# Installation des paquets requis
sudo apt install wget apt-transport-https gnupg lsb-release -y
# Ajout de la clé GPG du dépôt Trivy
sudo wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null
# Ajout du dépôt Trivy
sudo echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main" | sudo tee -a /etc/apt/sources.list.d/trivy.list
# Mise à jour des listes de paquets
sudo apt update
# Installation de Trivy
sudo apt install trivy -y
#Afficher les informations de version
Trivy --version
