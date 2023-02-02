# Workshop - Découverte du framework Ruby on Rails

## Liens utiles
* Documentation officielle du Ruby on Rails: https://guides.rubyonrails.org/
* Tutoriels Ruby on Rails: https://railstutorial.org/
* API Ruby on Rails: https://api.rubyonrails.org/

## Prérequis
* Ruby 3.0.0 et supérieur (https://www.ruby-lang.org/fr/documentation/installation/)
* Rails 7.0.0 et supérieur (Une fois ruby installé, exécuter la commande `gem install rails`)
* Une fois dans le dossier, utiliser la commande `rails new .`
##### /!\ Important: Une fois dans le projet, exécuter la commande `sudo bundle install` pour installer les dépendances du projet

## Lancer le projet
* Exécuter la commande `rails server` ou `rails s` dans le dossier du projet
* Ouvrir le navigateur à l'adresse `http://localhost:3000/`

## Objectif du workshop
Vous allez découvrir le framework Ruby on Rails en développant une implémentation basique d'un CRUD.

Ce projet est décomposé en plusieurs étapes:
1. Pouvoir créer un "Joueur" possédant un nom, un lieu de naissance (max 50 caractères) et une date de naissance
2. Une fois ce joueur créé, pouvoir le modifier ainsi que le supprimer
3. Pouvoir afficher la liste des joueurs créés
4. Créer un nouvel objet "Équipe" possédant un nom et une liste de joueurs, puis pouvoir créer, modifier et supprimer une équipe
5. Limiter le nombre de joueurs par équipe à 5

##### Bonus
6. Permettre à l'utilisateur de créer un tournoi, celui-ci créera 8 équipes chacunes peuplées de 5 joueurs créés au même moment
7. Lancer ce tournoi, chaque équipe peut gagner (3 points), perdre (0 points) ou faire match nul (1 point), le tournoi se termine quand toutes les équipes ont joué chacune l'une contre l'autre
8. Dresser un classement des équipes en fonction de leur score

## Notions utiles

### CRUD
CRUD signifie Create, Read, Update, Delete et représente les quatre opérations de base pour gérer les données dans une application.

1. Create (Créer) : c'est l'opération pour ajouter de nouvelles données à la base de données.
2. Read (Lire) : c'est l'opération pour récupérer les données stockées dans la base de données.
3. Update (Mettre à jour) : c'est l'opération pour mettre à jour les données existantes dans la base de données.
4. Delete (Supprimer) : c'est l'opération pour supprimer les données de la base de données.

L'acronyme CRUD est largement utilisé pour décrire les opérations de base pour gérer les données dans les systèmes d'information et les applications.

### MVC (Model View Controller)
Ruby on Rails est un framework qui utilise le design pattern MVC. Voici une description détaillée de chaque partie :

#### Model
Le modèle représente les données de l'application, telles que les informations enregistrées dans la base de données. Dans le code suivant, nous avons un exemple de modèle d'article qui utilise la validation de la présence d'un titre et d'un corps d'article.

```ruby
class Article < ApplicationRecord
  validates :title, presence: true
  validates :body, presence: true
end
```

Ici, nous définissons une classe Article qui hérite de ApplicationRecord. Les lignes `validates :title, presence: true` et `validates :body, presence: true` définissent que le titre et le corps d'article sont obligatoires pour que l'article puisse être enregistré dans la base de données.

#### View
La vue est ce que l'utilisateur voit. Elle affiche les données du modèle sous forme d'une interface utilisateur. Dans le code suivant, nous avons un exemple de vue qui affiche le titre et le corps d'un article.

```erb
<h1><%= @article.title %></h1>
<p><%= @article.body %></p>
```

Ici, nous utilisons des tags HTML pour définir le formatage de la page web, et les expressions `<%= @article.title %>` et `<%= @article.body %>` pour afficher respectivement le titre et le corps de l'article stocké dans l'instance `@article`.

#### Controller
Le contrôleur gère les interactions entre le modèle et la vue. Il répond aux actions de l'utilisateur et met à jour les données du modèle. Dans le code suivant, nous avons un exemple de contrôleur d'article qui gère l'affichage d'un article.

```ruby
class ArticlesController < ApplicationController
  def show
    @article = Article.find(params[:id])
  end
end
```

Ici nous définissons une classe ArticlesController qui hérite de ApplicationController. La méthode `show` récupère l'article dont l'identifiant est passé dans l'URL et l'assigne à l'instance `@article`.

### Routes

Les routes sont des fichiers qui définissent les URLs de l'application. Dans le code suivant, nous avons un exemple de route qui permet d'accéder à la page d'un article.

```ruby
Rails.application.routes.draw do
  get '/articles/:id', to: 'articles#show'
end
```

```ruby
Rails.application.routes.draw do
  resources :articles
end
```
