# 🏎️ Porsche Sales Dashboard: Agente de Tratamento de Dados

![Python](https://img.shields.io/badge/Python-3.12-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-data%20cleaning-150458?style=for-the-badge&logo=pandas&logoColor=white)
![HTML](https://img.shields.io/badge/Dashboard-HTML%2FJS-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![Chart.js](https://img.shields.io/badge/Chart.js-gr%C3%A1ficos-FF6384?style=for-the-badge&logo=chartdotjs&logoColor=white)
![Status](https://img.shields.io/badge/Acerto%20vs%20gabarito-100%25-5f9d72?style=for-the-badge)

### [Ver dashboard ao vivo](https://alv-vitoria.github.io/dio-creative-challenges/)

Projeto do desafio da DIO **"Criando uma Dashboard da Porsche com Agentes de IA"**.

A missão era simples de descrever e meio caótica de executar: pegar um cadastro de
vendas de Porsche **completamente sujo** (datas escritas de 7 jeitos diferentes,
preço em dólar/euro/"$121k"/por extenso, quilometragem em milhas e km misturadas,
nomes de pagamento com e sem espaço, maiúscula, hífen, bagunça total) e transformar
isso em um dashboard limpo e bonito de se olhar.

## O agente de tratamento de dados

Em vez de chamar uma LLM linha a linha (o que custaria dinheiro e seria mais lento
que o necessário pra um conjunto finito de padrões), o agente segue o fluxo clássico
de um agente baseado em regras:

1. **Percepção** -> lê a planilha bruta campo a campo.
2. **Raciocínio** -> cada campo tem uma função `normalize_*` que decide o que aquele
   valor bagunçado realmente significa (`"$121k"` → `121000.0`, `"20-23"` → ano
   `2023`, `"KM 18.900"` → converte pra milhas, `"twenty twenty four"` → `2024`...).
3. **Ação** -> grava o dataset limpo em CSV e JSON, pronto pra alimentar o dashboard.

A planilha original já trazia, do lado de cada coluna suja, a coluna "gabarito"
(`*Sanitized`) usada nas aulas. O script `validate_against_ground_truth()` compara
o resultado do agente com esse gabarito automaticamente:
```
sale_date          -> 100.0% de acerto
model_year         -> 100.0% de acerto
sale_price         -> 100.0% de acerto
vehicle_mileage    -> 100.0% de acerto
payment_method     -> 100.0% de acerto
city               -> 100.0% de acerto
state              -> 100.0% de acerto
delivery_status    -> 100.0% de acerto
```
> Se um dia esse dataset ficar mais "selvagem" (texto livre, gírias, erros de
> digitação imprevisíveis), o próximo passo natural é plugar uma chamada de LLM
> (Groq/Ollama, por exemplo) como *fallback* dentro de cada `normalize_*`, só para
> os casos que as regras não reconhecerem. Para o que a base trazia, regras
> explícitas resolveram com 100% de precisão e zero custo de API.


## O dashboard
<p align="center">
<a href="https://raw.githubusercontent.com/alv-vitoria/dio-creative-challenges/main/challenges/dashboard_porsche_sales/assets/dashboard-preview.png">
  <img src="https://raw.githubusercontent.com/alv-vitoria/dio-creative-challenges/main/challenges/dashboard_porsche_sales/assets/dashboard-preview.png" width="300">
</a>

Construído em HTML/CSS/JS puro (Chart.js embutido, sem dependência de internet
pra abrir), com identidade visual inspirada na estética minimalista e exclusiva da
Porsche, preto profundo, vermelho racing, detalhes em dourado, tipografia serifada
para os títulos e condensada pros números, como uma ficha técnica de carro.

**Filtros:** modelo, ano do modelo, cidade e forma de pagamento -> tudo reativo.

**Principais perguntas de negócio respondidas:**
- Quanto a concessionária faturou, quantos carros vendeu e qual o ticket médio?
- Quais modelos geram mais receita (e isso muda por cidade/ano/pagamento)?
- Em quais cidades estão as melhores vendas?
- Como está a saúde logística das entregas (entregue x cancelado x pendente)?
- Como os clientes estão pagando?
- Quem são os vendedores que mais faturam?

Todos os gráficos recalculam ao vivo conforme os filtros: selecionar uma cidade,
por exemplo, já responde "qual o modelo que mais vende ali" sem precisar de um
gráfico extra só pra isso.

---
<p align="center">
  <img src="https://assets.dio.me/0XjbOY4B8O2AVkaVEylhZZr0_OtikC59t60NSG9SDT8/f:webp/h:120/q:80/L3RyYWNrcy80NGMxZDg4MC03NjVlLTRlM2MtOGZkNS0yNTk1ODQ2ZDhmMzEucG5n"
       alt="Badge DIO"
       width="100">
<p>

Bootcamp **Aceleração: AI Reports com Excel, GPT Agents e Claude Code**
Desafio original: **DIO Criando uma Dashboard da Porsche com Agentes de IA**

---

### Autor: Vitória Alvares

## Contatos
[![Email](https://img.shields.io/badge/ProtonMail-7B5EA7?style=for-the-badge&logo=protonmail&logoColor=white)](mailto:Alvares26Sa@proton.me)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/vitória-alvares/)
[![GitHub](https://img.shields.io/badge/GitHub-0d1117?style=for-the-badge&logo=github&logoColor=B4A0E5)](https://github.com/alv-vitoria)
