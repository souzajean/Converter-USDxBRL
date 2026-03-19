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
![Fluxo](imagens/Screenshot_17.png)
```
setOrderXML
```

<br>

### Configurando o Content Modifier
![Fluxo](imagens/Screenshot_18.png)
```
Content Modifier - setOrderXML
Exchange Property
create - _orderXML - Expression - ${body} - java.lang.String
```

<br>

### Adicionando o Join
![Fluxo](imagens/Screenshot_19.png)

<br>

### Adicionando o Gather
![Fluxo](imagens/Screenshot_20.png)

<br>

### Configurando o Gather
![Fluxo](imagens/Screenshot_21.png)

<br>

### Conectando o Request Replay no Receiver
![Fluxo](imagens/Screenshot_22.png)

<br>

### Adicionando o HTTP
![Fluxo](imagens/Screenshot_23.png)

<br>

### Configurando o Request Replay
![Fluxo](imagens/Screenshot_24.png)
```
Request Reply
Address: https://api.frankfurter.app/latest
Query: from=USD&to=BRL
Proxy Type: Internet
Method: GET
Authentication: None
```

<br>

### Conectando o Request Replay no JSON to XML Dolar
![Fluxo](imagens/Screenshot_25.png)

<br>

### Conectando o Request Replay no Receiver
![Fluxo](imagens/Screenshot_26.png)
```
Name: JSON to XML Dolar
Processing - Add XML Root Element
Name: Exchange
```

<br>

### Conectando o JSON to XML Dolar no Join
![Fluxo](imagens/Screenshot_27.png)

<br>

### Iflow vai ficar dessa forma
![Fluxo](imagens/Screenshot_28.png)

<br>

### Adicionar Message Mapping
![Fluxo](imagens/Screenshot_29.png)

<br>

### Renomeando o Message Mapping
![Fluxo](imagens/Screenshot_30.png)

<br>

### Criando o Message Mapping
![Fluxo](imagens/Screenshot_31.png)
```
mm_req
```
<br>

### Message Mapping
Adicionar o Source e Target
![Fluxo](imagens/Screenshot_32.png)

### Vamos subir o arquivo source.xsd
Adicionar o Source e Target
![Fluxo](imagens/Screenshot_33.png)

```
<?xml version="1.0" encoding="UTF-8"?>

<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">

  <xs:element name="Messages">
    <xs:complexType>
      <xs:sequence>

        <!-- Message1 -->
        <xs:element name="Message1">
          <xs:complexType>
            <xs:sequence>

              <xs:element name="Exchange">
                <xs:complexType>
                  <xs:sequence>

                    <xs:element name="amount" type="xs:decimal"/>
                    <xs:element name="base" type="xs:string"/>
                    <xs:element name="date" type="xs:string"/>

                    <xs:element name="rates">
                      <xs:complexType>
                        <xs:sequence>
                          <xs:element name="BRL" type="xs:decimal"/>
                        </xs:sequence>
                      </xs:complexType>
                    </xs:element>

                  </xs:sequence>
                </xs:complexType>
              </xs:element>

            </xs:sequence>
          </xs:complexType>
        </xs:element>

        <!-- Message2 -->
        <xs:element name="Message2">
          <xs:complexType>
            <xs:sequence>

              <xs:element name="Order">
                <xs:complexType>
                  <xs:sequence>
                    <xs:element name="OrderId" type="xs:string"/>
                    <xs:element name="Amount" type="xs:decimal"/>
                    <xs:element name="currency" type="xs:string"/>
                  </xs:sequence>
                </xs:complexType>
              </xs:element>

            </xs:sequence>
          </xs:complexType>
        </xs:element>

      </xs:sequence>
    </xs:complexType>
  </xs:element>

</xs:schema>
```

<br><br>

### Vamos subir o arquivo source.xsd
Adicionar o Source 
![Fluxo](imagens/Screenshot_34.png)


<br>

### Upload arquivo source.xsd
Adicionar o Source
![Fluxo](imagens/Screenshot_35.png)

<br>

### Adicionando arquivo target.xsd
Adicionar o Target
![Fluxo](imagens/Screenshot_36.png)

<br>

### Adicionando arquivo target.xsd
Adicionar o Target
![Fluxo](imagens/Screenshot_37.png)
```
<?xml version="1.0" encoding="UTF-8"?>

<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">

  <xs:element name="Order">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="OrderId" type="xs:string"/>
        <xs:element name="AmountBRL" type="xs:decimal"/>
      </xs:sequence>
    </xs:complexType>
  </xs:element>

</xs:schema>
```


<br>

### Realizando as conexões
Adicionar o Target
![Fluxo](imagens/Screenshot_38.png)

<br>

### Realizando as as conexões na funções
![Fluxo](imagens/Screenshot_39.png)

<br>

### Realizando as conexões na funções
![Fluxo](imagens/Screenshot_40.png)

<br>

### Adicionadno o Multiply nas Funções
![Fluxo](imagens/Screenshot_41.png)

<br>

### Adicionadno o formatNumber nas Funções
![Fluxo](imagens/Screenshot_42.png)

<br>

### Configurando no Postman
![Fluxo](imagens/Screenshot_43.png)



<br>
<br>








## 📦 Exemplo prático – iFlow para baixar

📦 [Download do iFlow – Converter-USDxBRL](https://github.com/souzajean/Converter-USDxBRL/raw/main/Package/ConvertendoDollarparaReal.zip)



> O arquivo pode ser importado diretamente no SAP Integration Suite (CPI).

