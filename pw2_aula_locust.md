---
theme: default
transition: fade
colorSchema: dark
lineNumbers: true
layout: image
image: /cover.svg
description: Programação Web 2
author: José Roberto Bezerra
title: Locust
exportFilename: pw2_aula6_componentes
---

# {{ $slidev.configs.title }}
{{ $slidev.configs.description }}

---

# Objetivo de Aprendizagem
- Conhecer, criar e utilizar componentes React

---

# Agenda

- Performance
- Locust
- Primeiros testes

---
layout: quote
---

# Como testar a Performance de um aplicação web?

> Existem diversas métricas que podem ser consideradas para testar o desempenho de aplicações web.

---

# Performance
Métricas Típicas

> **Tempo de resposta** (*response time*); tempo total desde o envio da requisição até o recebimento completo da resposta

---

# Performance
Métricas Típicas

> **Requisições por Segungo** (RPS); Número de requisições por segundo que o sistema suporta/atende

---

# Performance
Métricas Típicas

> **Taxa de Erro** (%); Percentual de requisições com status 4xx/5xx

---

# Performance
Métricas Típicas


# Percentis

| Percentil | Significado | Por que usar |
|-----------|-------------|---------------|
| **p50 (mediana)** | Metade das requisições foi mais rápida que isso | Visão geral |
| **p95** | 95% das requisições foram mais rápidas que isso | Padrão da indústria para SLAs |
| **p99** | 99% – cauda longa | Detecta outliers e gargalos |
| **p99.9** | Requisições muito lentas | Para sistemas críticos (financeiro, saúde) |

---


# Métricas Aceitáveis

- $p95 < 300ms $
- $p99 < 800ms $
- $Taxa de erro < 0,1%$
- *Throughput* mínimo de 500 RPS sob carga de 1000 usuários virtuais 

---
layout: section
---

# Locust

---

# Load Testing Tools

- Apache JMeter (Java)
- Gatling (Scala)
- Locust (Python)

---

# O que é Locust?

> Locust is an open source performance/load testing tool for HTTP and other protocols. 

---

# Locust
*Features*

- Criar cenários via *scripts*
- Interface web
- Versatilidade de protocolos

---
layout: section
---

# Primeiros Testes

---

# Como Criar um Cenário de Teste?

1. Criar um ambiente virtual Python (venv)
2. Listar as rotas que devem ser acessadas
3. Escrever o arquivo `locustfile.py``

---

# `locustfile.py`

```python
import time
from locust import HttpUser, task, between

class QuickstartUser(HttpUser):
    wait_time = between(1, 5)

    @task
    def hello_world(self):
        self.client.get("/hello")
        self.client.get("/world")

    @task(3)
    def view_items(self):
        for item_id in range(10):
            self.client.get(f"/item?id={item_id}", name="/item")
            time.sleep(1)

    def on_start(self):
        self.client.post("/login", json={"username":"foo", "password":"bar"})
```

---

# Como Criar um Cenário de Teste?

4. Rodar o comando `locust`
5. Acessar a interface web

---
image: https://docs.locust.io/en/stable/_images/webui-splash-light.png
layout: image-right
backgroundSize: contain
---

[http://localhost:8089](http://localhost:8089)

6. Configure os parâmetros
    - Quantidade de usuários
    - Taxa de crescimento (usuários/segundo)
    - O alvo do teste (*host*)
7. Inicie o teste (Start)

---



---
layout: fact
---

# Perguntas?

---
layout: fact
---

# Exercícios

---

# 1

---

# Referências

- [Locust Documentation](https://docs.locust.io/en/stable/index.html)

---
src: /snippets/end.md
---

