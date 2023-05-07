# Création de la passerelle de réseau virtuel

### recherchez "Passerelles de réseau virtuel" dans "tous les services" :
![image](https://user-images.githubusercontent.com/120634098/236682270-47de2bc7-1ca8-4cd6-95d7-14a5bf8717ad.png)

### Choisissez "VPN" comme "Type de passerelle", puis "Basé sur itinéraires" comme "Type de VPN" :
![image](https://user-images.githubusercontent.com/120634098/236681957-1f5b76b0-765a-45fa-85fa-299cf5239e58.png)
![2023-04-28 15_49_49-VNet1GW - Microsoft Azure](https://user-images.githubusercontent.com/120634098/236682140-20828bfc-6720-4f0b-8b27-4fae8976b856.png)

### Attendre une trentaine de minute le temps du déploiement.

# Ajouter une connexion site-à-site

![2023-04-28 15_49_31-VNet1GW - Microsoft Azure](https://user-images.githubusercontent.com/120634098/236682387-75e23609-a2d7-4e2b-86ab-2b221a06cf18.png)

### Ajouter une connexion :
![image](https://user-images.githubusercontent.com/120634098/236682439-51facf4b-784d-40bd-8cca-1190965c580f.png)

### Bien choisir "Site à site (IPsec)" comme "Type de connexion", puis cliquez sur "Choisir une passerelle de réseau local" :
![image](https://user-images.githubusercontent.com/120634098/236682463-b8284dc0-f9d5-4939-b3ec-e738e71f6daf.png)

### Déclarer le PfSense avec son adresse IP :
![2023-04-28 15_52_43-Site1 - Microsoft Azure](https://user-images.githubusercontent.com/120634098/236682758-6c2914dd-efe5-45fc-abcf-675d7214936b.png)

### Définir par la suite la clé partagée PSK
![2023-04-28 15_50_30-VNet1GW - Microsoft Azure](https://user-images.githubusercontent.com/120634098/236682598-f36b92b2-581c-41e9-bbe3-cfb1222fa982.png)

### Résultat :
![2023-04-28 15_50_15-VNet1GW - Microsoft Azure](https://user-images.githubusercontent.com/120634098/236682343-a7f4b595-fd94-4aa6-9edd-315154c1b0c3.png)
