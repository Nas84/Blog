---
title: 'Découverte et amorçage de projet : qu&rsquo;avons-nous appris de la planification par capacités ?'
author: Tiphaine
date: 2015-02-19T15:46:00+00:00
featured_image: /wp-content/uploads/2016/04/2.Produits.jpg
tumblr_sogilisblog_permalink:
  - http://sogilisblog.tumblr.com/post/111473929716/découverte-et-amorçage-de-projet-quavons-nous
tumblr_sogilisblog_id:
  - 111473929716
pyre_show_first_featured_image:
  - no
pyre_portfolio_width_100:
  - default
pyre_image_rollover_icons:
  - default
pyre_post_links_target:
  - no
pyre_related_posts:
  - default
pyre_share_box:
  - default
pyre_post_pagination:
  - default
pyre_author_info:
  - default
pyre_post_meta:
  - default
pyre_post_comments:
  - default
pyre_slider_position:
  - default
pyre_slider_type:
  - no
pyre_avada_rev_styles:
  - default
pyre_display_header:
  - yes
pyre_header_100_width:
  - default
pyre_header_bg_full:
  - no
pyre_header_bg_repeat:
  - repeat
pyre_displayed_menu:
  - default
pyre_display_footer:
  - default
pyre_display_copyright:
  - default
pyre_footer_100_width:
  - default
pyre_sidebar_position:
  - default
pyre_page_bg_layout:
  - default
pyre_page_bg_full:
  - no
pyre_page_bg_repeat:
  - repeat
pyre_wide_page_bg_full:
  - no
pyre_wide_page_bg_repeat:
  - repeat
pyre_page_title:
  - default
pyre_page_title_text:
  - default
pyre_page_title_text_alignment:
  - default
pyre_page_title_100_width:
  - default
pyre_page_title_bar_bg_full:
  - default
pyre_page_title_bg_parallax:
  - default
pyre_page_title_breadcrumbs_search_bar:
  - default
fusion_builder_status:
  - inactive
avada_post_views_count:
  - 2011
sbg_selected_sidebar:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_replacement:
  - 'a:1:{i:0;s:0:"";}'
sbg_selected_sidebar_2:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_2_replacement:
  - 'a:1:{i:0;s:0:"";}'
categories:
  - DÉVELOPPEMENT
tags:
  - agile
  - capabilities
  - planning
  - project
  - risk
  - storymap

---
Dans ce dernier article, nous allons revoir les <span style="text-decoration: underline;"><a href="http://sogilis.com/blog/decouverte-amorcage-projet-storymap/" target="_blank">problèmes rencontrés avec les story maps</a></span> et expliquer comment la planification par capacités apporte des réponses plus pertinentes dans notre contexte. Cette rétrospective nous montrera que l&rsquo;essentiel n&rsquo;est pas dans la méthode de Liz, mais bien dans sa façon d&rsquo;approcher et de prioriser les problèmes &#8211; favoriser <span style="text-decoration: underline;"><a href="http://www.agilemanifesto.org/iso/fr/" target="_blank">« les individus et leurs interactions plus que les processus et les outils »</a></span>. Ceci nous mènera naturellement à une petite réflexion sur notre approche de l&rsquo;agilité avec nos porteurs de projet.

<!-- more -->

## Quelques leçons tirées de la cartographie par capacité

### Les utilisateurs ne représentent que la partie visible des acteurs du projet

Dans le cadre d&rsquo;une story map, l&rsquo;accent est mis sur les activités et les cas d&rsquo;utilisation du système. Cela peut conduire à se focaliser sur les utilisateurs principaux du système, au détriment d&rsquo;autres acteurs moins en vue mais dont l&rsquo;implication dans le projet peut être déterminante. Ainsi, au cours du développement d&rsquo;une application web, nous avions fixé des pré-requis pour les navigateurs des clients. Mais nous nous sommes rendus compte bien tardivement que certains de nos collègues (impliqués indirectement dans le projet) n&rsquo;avaient alors plus accès à l&rsquo;application, car les pré-requis étaient trop hauts pour leur machine !

De plus, un focus trop rapide sur les utilisateurs entraîne facilement un focus sur les fonctionnalités, ce qui se fait au détriment de l&rsquo;analyse des besoins et de la recherche de solutions. Le niveau de détails est trop bas pour s&rsquo;imprégner des enjeux et des problématiques du projet. Cela peut même <span style="text-decoration: underline;"><a href="http://lizkeogh.com/2010/02/02/theyre-not-user-stories/" target="_blank">induire en erreur</a></span> sur l&rsquo;acteur et le besoin réel auquel répond la fonctionnalité.

La vision du projet, avec sa proposition de valeur mais aussi son impact sur les acteurs, est à cultiver dès le début : **balayer tous les acteurs du projet, essayer de comprendre leurs besoins, leur attitude et leur impact sur le projet, si celui-ci sert leurs intérêts ou bien peut être un frein**. Cette analyse a aussi pour but de ne pas se fixer d&rsquo;oeillères sur ce qu&rsquo;il faut réaliser : le but est de satisfaire au maximum les besoins de chaque acteur du projet. La solution ne passe pas forcément par une liste de fonctionnalités !

### Le focus est sur la résolution de problèmes, pas sur les fonctionnalités

Le focus trop rapide sur les fonctionnalités peut aussi avoir des effets négatifs lors de la réalisation du projet.

  * Le besoin de la fonctionnalité est peu approfondie ; il n&rsquo;en reste qu&rsquo;une description superficielle, de laquelle il est difficile de revenir aux sources si on cherche une solution alternative.
  * La liste des fonctionnalités de la story map apparaît parfois comme un périmètre, à la manière d&rsquo;un cahier des charges. Or beaucoup de choses peuvent encore changer en cours de projet.
  * La granularité des fonctionnalités peut être très hétérogène et leur description aussi : les « petites » fonctionnalités auront tendance à être plus détaillées que les grosses, car plus évidentes ; conjointement la complexité des grosses peut être masquée par le manque de détails dans leur description.
  * Des notions de valeur et de coût sont parfois utilisées pour aider à la priorisation des fonctionnalités. Ces notions posent des problèmes de définition (s&rsquo;agit-il de la valeur en tant que nouveauté ou nécessité ? Quelle est l&rsquo;échelle pour l&rsquo;estimation du coût : _story points_, jour-hommes ?) Se focaliser sur ces estimations peut masquer des problèmes de dépendances : la fonctionnalité X n&rsquo;est pas jugée intéressante car coûteuse, pourtant une sous-partie est nécessaire à une autre partie valorisable.

Bref, la story map peut donner une fausse impression de complétude, à la manière d&rsquo;un cahier des charges, avec différents lots de fonctionnalités définis à l&rsquo;avance. En cas de problème lors de la réalisation, le champ d&rsquo;action pour rétablir le projet peut être limité car les acteurs auront du mal à sortir des rails de la story map.

**Tout projet propose une vision différente par rapport à l&rsquo;existant. Mais il existe plusieurs façons de réaliser cette vision.** L&rsquo;important est donc de ne pas avoir d&rsquo;oeillères sur le chemin de la réalisation. Parler de capacités doit permettre de se concentrer sur le problème et le besoin à résoudre.

  * En prenant une approche centrée sur le problème, il y a moins de risque de passer du temps sur les détails d&rsquo;une solution (la fonctionnalité) au détriment d&rsquo;autres possibilités.
  * En exprimant les futures _capacités_ du système, vous savez que vous devez chercher une solution pour satisfaire ces capacités. Les moyens de les satisfaire sont multiples et peuvent être remises en cause en cours de projet (nouvelles options, solutions alternatives et moins coûteuses). Le terme de capacité permet aussi plus facilement d&rsquo;aborder les aspects non fonctionnels du système (robustesse, performance…).
  * En cas d&rsquo;échec avec une solution, il est plus facile de repartir de la capacité que d&rsquo;une fonctionnalité (quel est le problème, le besoin ? Comment y répondre ?).

### La planification est basée sur le dérisquage et la valorisation du projet, pas sur la priorisation par estimation

La pratique courante issue des story maps et des méthodologies agiles est de prioriser les stories par rapport à leur valeur et leur coût estimé, pour les placer dans l&rsquo;ordre dans le backlog. La notion de chemin critique, voire de MVP, est parfois abordée mais pas nécessairement approfondie. Le backlog ressemble alors à une liste de fonctionnalités à développer.

  * Le suivi se base sur la réalisation d&rsquo;un plan (même s&rsquo;il est léger) et il peut se créer un ressenti de retard ou de travail mal fait à cause des sacrifices faits par rapport au plan (fonctionnalité ou qualité).
  * La priorisation liée aux dépendances entre fonctionnalités est souvent masquée dans cette approche ; cela peut rendre la repriorisation complexe.
  * Si une fonctionnalité se révèle mal estimée en cours de sprint, des décalages liés à la résolution des problèmes se créent dans le suivi de charge, ce qui peut être perturbant pour une équipe mal rôdée ; l&rsquo;équipe pense prendre du retard, qui ne peut être rattrapé sauf à changer le périmètre.
  * Même tard en fin de projet, on peut tomber sur une exigence complexe, mal estimée, qui rend difficile la vision sur la fin du projet.
  * Plus on est ignorant sur un aspect du projet, moins on sera pertinent pour son estimation, plus on prend des risques à s&rsquo;engager. Or les plans type story map tendent malgré tout à un engagement, même peu formalisé.

En se focalisant sur les risques d&rsquo;échec ainsi que sur les points différenciants, l&rsquo;accent est mis sur l&rsquo;essentiel : trouver la prochaine étape la plus sûre et la plus rapide pour démontrer la valeur du projet, avant de passer à la suivante. **L&rsquo;approche vise la réalisation de la vision**, la résolution des problèmes rencontrés, plutôt que la coche de fonctionnalités dans une liste.

### Traiter l&rsquo;estimation comme une projection, pas un engagement

Bien que l&rsquo;on sorte du cadre strict de la planification, l&rsquo;estimation du coût d&rsquo;un projet est la suite logique pour un porteur. Là encore, Dan North en a très bien décrit les enjeux et les écueils dans <span style="text-decoration: underline;"><a href="http://dannorth.net/2009/07/01/the-perils-of-estimation/" target="_blank">The Perils of Estimation</a></span> et même proposé son idée dans <span style="text-decoration: underline;"><a href="http://dannorth.net/2013/08/08/blink-estimation/" target="_blank">Blink Estimation</a></span>.

Sans rentrer dans le détail de ce débat (voir tout ce qui concerne le <span style="text-decoration: underline;"><a href="https://twitter.com/search?q=%23NoEstimates&src=typd" target="_blank">No Estimates</a></span>), la méthode de Liz apporte son petit grain de sel aux estimations. En effet, plus vous estimez que le niveau de risque est fort, plus il y a d&rsquo;inconnus sur les problèmes que vous allez rencontrer, et plus votre estimation sera incertaine. Jusqu&rsquo;au point où une estimation n&rsquo;est plus pertinente et où vous devez commencer par une approche exploratoire, moins risquée et moins coûteuse.

Plus simplement, la question de l&rsquo;estimation peut être traitée par l&rsquo;équipe comme une projection dans l&rsquo;avenir. **Quelle horizon se donne-t-elle pour trouver une solution à ce problème ? Et quelle confiance a-t-elle dans cette horizon ?** Si l&rsquo;équipe n&rsquo;est pas confiante, comment réduire le risque ? Si besoin, l&rsquo;équipe peut renforcer son opinion en utilisant le poker planning, mais l&rsquo;estimation ne doit pas se transformer en chiffrage de fonctionnalités à la carte.

### Et si le porteur de projet a déjà un cahier des charges, un backlog, des idées toutes prêtes…

Stop ! La démarche ci-dessus doit normalement pousser tout le monde à remettre en cause des fonctionnalités prématurées, à proposer d&rsquo;autres solutions. Si le porteur insiste pour inclure une fonctionnalité dans votre cartographie, comment pouvez-vous la réexprimer comme une capacité, en gardant la fonctionnalité comme un exemple de solution concrète pour cette capacité ? Comme proposé par Liz, demandez au porteur **pourquoi** il veut cette fonctionnalité et jusqu&rsquo;à remonter aux besoins pour pouvoir exprimer la capacité.

## Obsolète, la story map ?

Comme noté dans le premier article, la story map pose problème dans notre contexte de découverte de projet, où le domaine est souvent nouveau pour l&rsquo;équipe et les pratiques agiles inconnues des porteurs de projet. **La planification par capacités est plus abordable** et nous permet de découvrir plus rapidement les fondamentaux d&rsquo;un projet naissant, mais aussi d&rsquo;organiser les premières itérations, produire des prototypes de démonstration, prévoir les prochaines étapes &#8211; et pourquoi pas servir de base à une story map qui détaillera plus les fonctionnalités.

Quand l&rsquo;équipe a acquis plus de maturité sur le domaine, ses enjeux et ses problèmes, il peut être intéressant d&rsquo;engager un processus orienté story map. Celle-ci permet de récapituler la vision de ce qu&rsquo;on veut réaliser, la réordonner, préparer les détails des prochaines itérations, quand la vision du projet s&rsquo;est stabilisée. Elle permettra alors un **suivi des étapes du projet** à la vue de tous, lot par lot.

Peut-on complètement se passer de la story map ? Je crois que oui. Comme noté par Dan North, des <span style="text-decoration: underline;"><a href="http://dannorth.net/2013/01/15/accelerating-agile/" target="_blank">équipes très efficaces</a></span> se sont construites en dehors de la culture agile classique, simplement en appliquant du bon sens dans leurs pratiques. La planification par capacités n&rsquo;est qu&rsquo;une des pratiques supportant ce type d&rsquo;approche.

## Changer notre approche de l&rsquo;agilité (encore et toujours)

Avoir persisté si longtemps dans une approche inadaptée amène une remise en question. Au-delà de l&rsquo;utilité de la planification par capacités, cette expérience nous a forcé à oublier certaines méthodes et pratiques de l&rsquo;agilité pour revenir aux fondamentaux.

### Sortir des rails des process agiles

Tout le monde a vécu un jour ou l&rsquo;autre cette expérience : copier une approche qui a « déjà marché » ailleurs ; et quand ça ne marche pas, recommencer en expliquant que les règles n&rsquo;ont pas été bien suivies. Certaines méthodes agiles ont un côté très cadré, cérémonieux qui encouragent ce comportement. Dans le pire des cas, on arrive à <span style="text-decoration: underline;"><a href="http://mikehadlow.blogspot.co.uk/2014/03/coconut-headphones-why-agile-has-failed.html" target="_blank">l&rsquo;agilité Cargo Cult</a></span>, où l&rsquo;équipe se déclare agile parce qu&rsquo;elle applique toutes les règles, mais sans en tirer les bénéfices car elle n&rsquo;a pas su les adapter à son contexte.

Ce qui est rarement dit sur les méthodes agiles, c&rsquo;est qu’**elles demandent souvent une bonne maturité sur le domaine du projet pour être 100% effective**. Rien n&rsquo;est plus plaisant que de travailler sur un projet complexe où chaque itération réussit son objectif, car l&rsquo;équipe maîtrise les enjeux, réagit immédiatement aux problèmes rencontrés, communique efficacement avec les autres acteurs du projet.

Mais quand nous avons affaire à des domaines inconnus, ces éléments sont loins d&rsquo;être acquis : l&rsquo;équipe cherche le bon niveau de communication, les zones d&rsquo;ombre sont nombreuses, les enjeux encore mal identifiés. Il est tentant, et rassurant, pour l&rsquo;équipe comme pour le porteur de se retrancher derrière un process, un contrat, un cahier des charges…

Par ailleurs, les outils agiles comme la story map semblent souvent simples, voire triviaux en apparence, mais demandent une bonne expérience pour être bien menés. Amener des nouveaux venus à utiliser ce type d&rsquo;outil dès les premiers contacts rend les choses complexes !

C&rsquo;est pourquoi choisir une approche moins structurée que la story map, comme la planification par capacité, est intéressant. Le niveau d&rsquo;entrée est faible, car n&rsquo;imposant pas différents concepts hiérarchisés (activité, cas d&rsquo;utilisation, fonctionnalité) : la _capacité_ résume ces concepts tout étant suffisamment souple pour que chacun se l&rsquo;approprie. A ce stade, l&rsquo;essentiel pour nous est d&rsquo;échanger sur le projet. **En enlevant des barrières de communication, il est plus facile pour l&rsquo;équipe de faire valoir son point de vue, sa force de proposition, et de ne pas apparaître comme une simple exécutante.**

### La culture de l&rsquo;accompagnement

Mais dans l&rsquo;approche de Liz Keogh, l&rsquo;aspect le plus intéressant et révélateur est certainement la prise en considération de sa propre ignorance et des risques associés. D&rsquo;abord parce qu&rsquo;elle met l&rsquo;accent sur le non-dit des projets au forfait, typique des SSII : sur quelles bases et quelles estimations la proposition de forfait a-t-elle été faite ? Quels risques ont été pris en compte ? Comment l&rsquo;équipe va-t-elle gérer et communiquer sur ces risques ? En règle générale, les risques ne sont considérés que comme un facteur multiplicateur dans l&rsquo;estimation (car le temps est court pour faire une proposition) et les risques seront gérés comme ils arrivent, et parfois dans l&rsquo;urgence de la crise.

Le risque, l&rsquo;inconnu est un paramètre essentiel de n&rsquo;importe quel projet, en particulier pour une start-up. C&rsquo;est pourquoi nous voulons le mettre au centre de notre approche. Pour un porteur de projet, notre première proposition est donc un accompagnement. La réponse que nous apportons n&rsquo;est pas forcément une estimation de son projet mais plutôt une projection : que pouvons-nous faire, quelle est la prochaine étape ? Notre métier n&rsquo;est pas que de développer des fonctionnalités, mais **d&rsquo;accompagner les porteurs à travers des étapes en proposant des solutions à moindre risque**.

<div>
  <img class="alignleft" src="http://www.gravatar.com/avatar/58778f8cc14e8a484568a663266c3029.png" alt="Simon Denier" width="124" height="124" /><a href="mailto:simon+blog@sogilis.com" target="_blank">Simon Denier</a><br /> <a href="http://twitter.com/simondenier" target="_blank"><span class="share-link-twitter"><i class="fa fa-twitter"></i> simondenier</span></a><br /> <a href="https://github.com/sdenier" target="_blank"><i class="fa fa-github"></i> sdenier</a><br /> <a href="https://plus.google.com/100056946931947086533?rel=author" target="_blank"><span class="share-link-google-plus"><i class="fa fa-google-plus"></i> +SimonDenier</span></a>
</div>