# FOSUserBundle 2.x on Symfony 3.1

```
composer create-project symfony/framework-standard-edition fos-user-2.0

cd fos-user-2.0
composer require friendsofsymfony/user-bundle "~2.0@dev"
php bin/console server:run
./bin/console doctrine:database:create
./bin/console generate:doctrine:entity # for AppBundle:Customer (because user is a reserved keyword)
# enable the translator
# add new FOS\UserBundle\FOSUserBundle(),
# edit of app/config/security.yml
# edit of app/config/config.yml
# edit of app/config/routing.yml
php bin/console doctrine:schema:update --force

CREATE TABLE customer (id INT AUTO_INCREMENT NOT NULL, username VARCHAR(180) NOT NULL, username_canonical VARCHAR(180) NOT NULL, email VARCHAR(180) NOT NULL, email_canonical VARCHAR(180) NOT NULL, enabled TINYINT(1) NOT NULL, salt VARCHAR(255) NOT NULL, password VARCHAR(255) NOT NULL, last_login DATETIME DEFAULT NULL, locked TINYINT(1) NOT NULL, expired TINYINT(1) NOT NULL, expires_at DATETIME DEFAULT NULL, confirmation_token VARCHAR(180) DEFAULT NULL, password_requested_at DATETIME DEFAULT NULL, roles LONGTEXT NOT NULL COMMENT '(DC2Type:array)', credentials_expired TINYINT(1) NOT NULL, credentials_expire_at DATETIME DEFAULT NULL, UNIQUE INDEX UNIQ_81398E0992FC23A8 (username_canonical), UNIQUE INDEX UNIQ_81398E09A0D96FBF (email_canonical), UNIQUE INDEX UNIQ_81398E09C05FB297 (confirmation_token), PRIMARY KEY(id)) DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci ENGINE = InnoDB;

open http://127.0.0.1:8000/register
```


- pourquoi le service est nommé fos_user.user_provider.username ?
- dès la config on est limité à une seule entité ?
- charset utf8 HEU QUOI ? Merci Doctrine/SYMFONY

        charset:  utf8mb4
        default_table_options:
          charset: utf8mb4
          collate: utf8mb4_unicode_ci
        options:
          charset: utf8mb4
LA BASE! Voir issue #5526 sur le sujet ouverte il y a plus d'1 an

- "The user has been created successfully"
- auto-login quand on s'inscrit par défaut, pas de validation d'email
- login par USERNAME uniquement par défaut
- '(DC2Type:array)' par défaut, ça se change ?
- username 🔩 pas possible, trop petit! Pour un password ok, mais là?!

TODO LOGMATIC SUR SLACK SECRET SANTA ?
