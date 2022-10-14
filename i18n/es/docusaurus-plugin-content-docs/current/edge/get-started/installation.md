---
id: installation
title:
description: ""
keywords:
  - docs
  - polygon
  - edge
  - install
  - installation
---





##  {#pre-built-releases}





---

##  {#docker-image}



`docker pull 0xpolygon/polygon-edge:latest`

---

##  {#building-from-source}





```shell
git clone https://github.com/0xPolygon/polygon-edge.git
cd polygon-edge/
go build -o polygon-edge main.go
sudo mv polygon-edge /usr/local/bin
```

---

##



`go install github.com/0xPolygon/polygon-edge@develop`


