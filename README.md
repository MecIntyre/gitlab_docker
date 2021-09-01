# GitLab

Gitlab-Installation mit den offiziellen Docker-Images

### Voraussetzungen:

1. installierter Docker, Benutzer in der docker-Gruppe
2. installiertes docker-compose

### Benutzung

1. Anpassen der /etc/hosts:

    - in der Zeile 127.0.0.1 zusätzlich den Eintrag gitlab anhängen
    
2. Terminal öffnen

      ```bash
      cd
      git clone https://github.com/JoergEF/gitlab
      cd gitlab/docker
      docker-compose up -d
      ```
      
3. wenn beide Container laufen (dauert einige Minuten)

      ```bash
      docker exec -it docker_gitlab_1 /bin/bash
      gitlab-rails console -e production
      user = User.find(1)
      user.password = 'Pa$$w0rd'
      user.password_confirmation = 'Pa$$w0rd'
      user.save!
      exit
      exit
      
      docker exec -it docker_gitlab-runner_1 /bin/bash
      gitlab-runner register
        # -> http://gitlab
        # -> <Registration-Token> aus http://gitlab
        # -> Runner im Docker-Container
        # -> docker, linux
        # -> shell
      exit
      ```
      
4. GitLab aufrufen

      http://gitlab
      
5. Anmelden

      ```
      Benutzername: root
      Passwort:     Pa$$w0rd
      ```
      
### alles stoppen

```bash
cd ~/gitlab/docker
docker-compose stop
```

### alles löschen

```bash
cd ~/gitlab/docker
docker-compose rm
# wenn die Daten gelöscht werden sollen
sudo rm -rf /srv/gitlab
```
