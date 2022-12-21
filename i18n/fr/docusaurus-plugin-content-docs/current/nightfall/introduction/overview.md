---
id: overview
title: Aperçu
sidebar_label: Overview
description: Un aperçu de Nightfall
keywords:
  - docs
  - polygon
  - nightfall
  - privacy
  - rollup
  - zk
image: https://matic.network/banners/matic-network-16x9.png
---

Polygon croit en une vision dans laquelle de nombreuses entreprises pourront interagir dans un avenir proche les unes
avec les autres par le biais de contrats intelligents pour l'exécution de la logique commerciale et la gestion de l'échange de biens et de services.

En collaboration avec [Ernst & Young](https://blockchain.ey.com/), Polygon propose une solution de rollup de couche 2 publique et axée sur la confidentialité appelée Polygon Nightfall pour permettre l'accessibilité et la confidentialité pour les entreprises souhaitant
utiliser Ethereum.

## Un protocole de preuve à divulgation nulle de connaissance pour les entreprises {#a-zk-proof-protocol-for-enterprises}

Polygon Nightfall fait partie de la gamme de solutions d'évolutivité de Polygon, qui comprennent
[Polygon Hermez](https://polygon.technology/solutions/polygon-hermez/),
[Polygon Miden](https://polygon.technology/solutions/polygon-miden/)
et [Polygon Zero](https://polygon.technology/solutions/polygon-zero/).
La principale différence est que Nightfall est un rollup axé sur la confidentialité conçu pour les cas d'utilisation d'entreprise en combinant
les concepts de rollups optimistes et de cryptographie de preuve à divulgation nulle de connaissance pour offrir des transactions privées et évolutives.

Alors que Nightfall permet l'évolutivité, il est également conçu pour supprimer un obstacle majeur auquel les entreprises sont confrontées aujourd'hui
lors de l'utilisation de la blockchain : le manque de confidentialité des transactions. Nightfall ajoute une couche de confidentialité, de sorte que les paramètres de transaction clés (par exemple, la valeur et la destination) ne peuvent pas être retracés. Ces deux caractéristiques ont nourri l'intérêt des entreprises privées qui voient Nightfall comme un moyen d'exécuter leur logique commerciale et de coordonner leur chaîne d'approvisionnement dans un réseau décentralisé à un prix durable, tout en maintenant la sécurité et la confidentialité.

## Piliers de Nightfall {#nightfall-s-pillars}

La principale proposition de valeur de Polygon Nightfall est de permettre des transferts sécurisés, privés et à faible coût des
données dans un réseau décentralisé.

![](../imgs/overview.png)

## Confidentialité {#privacy}

Polygon Nightfall utilise les pour envoyer des transactions privées. Un utilisateur peut générer une preuve à divulgation nulle de connaissance de
la transaction sans révéler les paramètres de transaction clés tels que la destination ou la valeur de la
transaction. Plus de détails sur la composante confidentialité de Nightfall sont disponibles dans le
guide des [protocoles](../protocol/protocol.md).

## Sécurité {#security}

> Nightfall fait actuellement l'objet d'un audit de sécurité, qui devrait se terminer mi-juin 2022.
> Une fois le processus de vérification terminé, les résultats seront postés ici.

> En tant que nouveau réseau avec une période d'amorçage, Nightfall dispose de mesures de sécurité transitoires pour
> protéger le système dans le but de les supprimer et de le conserver entièrement décentralisé.

Polygon Nightfall est une construction de couche 2, car elle tire parti d'Ethereum en empruntant sa sécurité en tant que
blockchain publique robuste. Nightfall repose sur certaines hypothèses qui garantissent le recouvrement d'actifs. Ces hypothèses sont
basées sur plusieurs décisions de conception et d'architecture autour de ZK-SNARKS, qui utilisent
certaines primitives cryptographiques, telles que les hachages et les signatures.
Enfin, Nightfall intègre des règles d'exploitation dans différents contrats intelligents pour garantir que les opérateurs ne bloquent pas
les transactions utilisateur et que les utilisateurs peuvent retirer leurs actifs à tout moment.

En résumé, Nightfall pose les hypothèses de sécurité suivantes :

1. Hypothèses de sécurité d'Ethereum.
2. Hypothèses Groth16 (connaissance de l'hypothèse de l'exposant).
3. Certaines hypothèses cryptographiques de primitives telles que les hachages (Poséidon) et les signatures.
4. Hypothèses de sécurité logicielle qui reposent sur une conception et une mise en œuvre correctes.

## Efficacité {#efficiency}

Les proposeurs de bloc collectent les transactions de divers utilisateurs et les regroupent dans un bloc L2.
Les tailles de blocs L2 typiques contiennent environ 32 transactions.

Les coûts de gaz prévus pour un dépôt, un transfert et un retrait sont de 9000, 1200 et 9500. Ce coût est dû au stockage de 574 octets de données d'appel par transaction, plus certaines
données d'appel fixes et de calcul pour traiter un bloc L2. Les fais peuvent baisser de 80 % après
[EIP 4488](https://eips.ethereum.org/EIPS/eip-4488).

## Transferts non refusables {#non-deniable-transfers}

Dans le cadre de la preuve à divulgation nulle de connaissance de la transaction de transfert, Nightfall inclut le chiffrement des secrets (adresse du jeton,
valeur, identifiant et salt) requis pour traiter l'engagement transféré. Cela oblige l'utilisateur à chiffrer les secrets
avec une clé connue du destinataire. Comme la clé fait partie de la preuve à divulgation nulle de connaissance, le destinataire s'appuie sur la possibilité de refus plausible
car l'expéditeur peut prouver que la clé de chiffrement correcte a été utilisée.

## Décentralisation {#decentralization}

Les valideurs et les [challengers](docs/nightfall/protocol/actors) font partie intégrante de Nightfall. Ils veillent à ce que
les transactions et les blocs L2 produisent correctement et en temps voulu. Un mécanisme de consensus fondé sur la preuve de participation est
utilisé pour sélectionner le prochain [proposant](docs/nightfall/protocol/actors) du réseau. D'autre part, les challengers surveillent
le bon fonctionnement du réseau en soulevant des challenges lorsqu'un bloc incorrect est détecté et en conservant le
stake avancée par le proposant.


## Preuve future {#future-proof}
Grâce à la flexibilité apportée par la mise en œuvre de rollup optimiste de Nightfall, il est possible d'inclure de nouvelles transactions
à l'avenir sans compromettre les transactions existantes, simplement en définissant et en enregistrant un nouveau type de circuit qui a mis en œuvre la
transaction dans ZK.

## Références {#references}

1. [A Multi-Sided Approach to ZK Scaling](https://messari.io/article/polygon-a-multi-sided-approach-to-zk-scaling)
2. [Vision de Paul Brody sur Nightfall](https://www.linkedin.com/pulse/say-hello-nightfall-paul-brody-1f/)
