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
CustomContentModifier
```
<br><br>

### Adicionando o Artefato do Integration Flow
![Fluxo](imagens/Screenshot_3.png)

<br><br>

### Criando o Integration Flow
![Fluxo](imagens/Screenshot_4.png)
```
ModifyContentModifier
```

<br><br>
:gear: Etapas da Integração

<br>

### :two:  Editar o Iflow

### Editar o Iflow
![Fluxo](imagens/Screenshot_5.png)

<br>

### Remover o Receiver
![Fluxo](imagens/Screenshot_6.png)

<br>

### :three:  HTTPS Sender
### Adicionando o HTTPS
![Fluxo](imagens/Screenshot_7.png)

<br>


### Configurando o HTTPS
O fluxo é iniciado através de um endpoint HTTPS, permitindo que aplicações externas consultem o serviço.
![Fluxo](imagens/Screenshot_8.png)
```
Address: /modificar
```
<br>

### :four:  Content Modifier
### Adicionando o Content Modifier
Vamos criar 3 Content Modifier na conexão
![Fluxo](imagens/Screenshot_9.png)

<br>

### Ficando dessa forma
![Fluxo](imagens/Screenshot_10.png)

<br>

### Renomear  Content Modifier - Header
![Fluxo](imagens/Screenshot_11.png)
```
setHeader
```

<br>

### Configurando Content Modifier - Header
![Fluxo](imagens/Screenshot_12.png)
```
Create  -  setHeader  - Constant  -  ValorHeader
```
<br>

### Renomear  Content Modifier - Property

![Fluxo](imagens/Screenshot_13.png)

```
setProperty
```
<br>

### Configurando Content Modifier - Property
![Fluxo](imagens/Screenshot_14.png)
```
Create  -  setProperty  - Constant  -  ValorProperty
```
<br>

### Renomear  Content Modifier - Body
![Fluxo](imagens/Screenshot_15.png)
```
Prepare Email Payload
```
<br>

### Configurando o Content Modifier - Body
![Fluxo](imagens/Screenshot_16.png)

Alteramos o Type: 
```
Expression
```
<br>

No Body:
```
Message Header:       ${header.setHeader}
Exchange Property:    ${property.setProperty}
Message Body CPI:     Mensagem do CPI
Message Body Postman: ${body}
```
<br>

### Configurando o Postman
![Fluxo](imagens/Screenshot_17.png)
```
Mensagem do Postman
```

Resultado:
```
Message Header:       ValorHeader
Exchange Property:    ValorProperty
Message Body CPI:     Mensagem do CPI
Message Body Postman: Mensagem do Postman
```

<br><br>

## 📦 Exemplo prático – iFlow para baixar

📦 [Download do iFlow –Apache-Camel](https://github.com/souzajean/Apache-Camel/raw/main/Package/ModifyContentModifier.zip)



> O arquivo pode ser importado diretamente no SAP Integration Suite (CPI).

