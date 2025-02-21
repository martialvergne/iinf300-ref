# Mise en place d'un déploiement continu d'une application docker sur Harbor
## Présentation du repo

Ce repo possède un dossier `docker` , dans celui-ci on retrouve un fichier `Dockerfile` qui créé une application basée sur les sources dans le dossier `docker/app`.

Nous retrouvons également le dossier `.github/workflows`. Dans celui-ci nous retrouvons le fichier build-demo qui sert pour la mise en place d'une pipeline qui permet de déployer une image sur harbor. Plus d'info "https://docs.github.com/en/actions/writing-workflows/quickstart"

## Consignes d'amélioration 

### Exercice 1

Par groupe clonez ce repo et vérifiez que le workflow fonctionne bien. 

Attention, placez le mot de passe habituel qui va bien dans https://github.com/___urldevotrerepo___/settings/secrets/actions et changez `harbor.kakor.ovh/ipi/correction` par `harbor.kakor.ovh/ipi/groupe-x`.

## Exercice 2

En partant de l'exemple https://github.com/marketplace/actions/python-linter, mettez en place un linter pour le code Python dans un job séparé dans le fichier `build-demo.yml`

## Exercice 3

Mettez en place Hadolint via l'exemple du repo ci-dessous de la même manière que pour PEP8 : https://github.com/marketplace/actions/python-linter

## Exercice 4 

En partant de l'exemple fonctionnel du lien suivant https://aschmelyun.com/blog/using-docker-run-inside-of-github-actions/, testez l'image en vous assurant que vous pouvez créer un nouveau livre en utilisant la commande suivante : ```curl --header "Content-Type: application/json" http://localhost:5000/librairie/livres -d '{"titre": "DevSecOps DEAVSETS", "auteur": "Jordan Assouline"}' ```

## Exercice 5

En vous connectant sur https://sonarqube.apps.openshift.kakor.ovh en utilisant le user ipi et le mot passe habituel dédoublé, générez un token qui vous servira pour ajouter le job suivant :

```
  sonarqube:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
      with:
        fetch-depth: 0
    - name: SonarQube Scan
      uses: SonarSource/sonarqube-scan-action@<ce/actions/official-sonarqube-scan
      env:
        SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
        SONAR_HOST_URL: https://sonarqube.apps.openshift.kakor.ovh
```

> Attention à mettre votre token dans les secret github et à modifier le fichier `sonar-project.properties` pour que le nom de projet soit dépendant du groupe