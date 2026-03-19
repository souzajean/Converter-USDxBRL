# 💵 Convertendo Dollar para Real
## 🚀 SAP BTP Integration Suite (CPI) – Conversão de Moeda com Parallel Multicast

📌 Visão Geral

Este projeto demonstra, na prática, como construir um iFlow no SAP BTP Integration Suite utilizando conceitos avançados de integração.

O cenário implementado realiza a conversão de valores em USD para BRL, combinando dados de entrada com uma API externa de câmbio em tempo real.

<br>

![Fluxo](imagens/capa-linkedin.png)


---

📸 Caso de Uso Real

Esse tipo de cenário é comum em integrações corporativas onde:

É necessário enriquecer dados com informações externas

Processar dados em paralelo para otimizar performance

Consolidar múltiplas fontes em um único payload

---





---


# :building_construction: Arquitetura do iFlow

### :one: O fluxo foi desenvolvido no SAP Cloud Integration (CPI) seguindo as etapas abaixo.
<br><br>
### Criando nosso Iflow
![Fluxo](imagens/Screenshot_1.png)
<br><br><br>

### Criando o Integration Flow
![Fluxo](imagens/Screenshot_2.png)
```
Converter_USDxBRL
```
<br><br>

### Adicionando o Artefato do Integration Flow
![Fluxo](imagens/Screenshot_3.png)

<br><br>

### Criando o Integration Flow
![Fluxo](imagens/Screenshot_4.png)
```
ConvertendoDollarparaReal
```

<br><br>
:gear: Etapas da Integração

<br>

### :two:  Editar o Iflow

### Editar o Iflow
![Fluxo](imagens/Screenshot_5.png)

<br>

### :three:  HTTPS Sender
### Adicionando o HTTPS
![Fluxo](imagens/Screenshot_6.png)
```
Address: /convertendodolar
```
<br>


### Configurando o HTTPS
O fluxo é iniciado através de um endpoint HTTPS, permitindo que aplicações externas consultem o serviço.
![Fluxo](imagens/Screenshot_7.png)
```
Address: /convertendodolar
```
<br>

### :four:  JSON to XML Converter
### Adicionando o JSON to XML Converter
![Fluxo](imagens/Screenshot_8.png)

<br>

### Renomeando o JSON to XML Converter
![Fluxo](imagens/Screenshot_9.png)

<br>

### Configurando o JSON to XML Converter
![Fluxo](imagens/Screenshot_10.png)
```
Order
```

<br>

### Adicionando Request Replay 
![Fluxo](imagens/Screenshot_11.png)

<br>

### Adicionando  JSON to XML Converter

![Fluxo](imagens/Screenshot_12.png)

<br>

### Renomeando o  JSON to XML Converter
![Fluxo](imagens/Screenshot_13.png)
```
JSON to XML Dolar
```
<br>

### Adicionando Multicast Paralel
![Fluxo](imagens/Screenshot_14.png)

<br>

### Renomeando Multicast Paralel
![Fluxo](imagens/Screenshot_15.png)
```
Parallel Multicast
```

<br>

### Adicionando o Content Modifier
![Fluxo](imagens/Screenshot_16.png)

<br>

### Renomeando o Content Modifier
![Fluxo](imagens/Screenshot_16.png)
```
setOrderXML
```

<br>













































































## 📦 Exemplo prático – iFlow para baixar

📦 [Download do iFlow –Apache-Camel](https://github.com/souzajean/Apache-Camel/raw/main/Package/ModifyContentModifier.zip)



> O arquivo pode ser importado diretamente no SAP Integration Suite (CPI).

