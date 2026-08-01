# Dashboard Gerencial de Supply Chain — Supermercado Estrela

Dashboard Power BI voltado à gestão da cadeia de suprimentos (*supply chain*) da rede de supermercados **Estrela**, cobrindo desde vendas e estoque até fornecedores, transporte e previsão de tendências.

## Arquivo

- `Dashboard_Gerencial_Supply_SupermercadoEstrela.pbix`

## Visão geral

O relatório é composto por **5 páginas**, cada uma cobrindo uma frente da operação de supply chain, com identidade visual própria (tema customizado "Rede Estrela", paleta azul `#5858F9`/`#7878F6`, logo da rede e navegação entre páginas via botões).

### 1. Visão Geral
Painel executivo com os principais indicadores do negócio:
- Cards de **Vendas (Unidades)**, **Receita Total**, **Taxa de Ruptura** e **OTIF %**
- Gráfico combinado (linha + coluna) de **Receita Total por Mês**
- **Donut chart** e **treemap** de Receita por Categoria

### 2. Estoque & Ruptura
Foco em disponibilidade de produto e saúde do estoque:
- Cards de **Dias até Ruptura Projetada**, **Cobertura de Estoque (dias)**, **Giro de Estoque** e **Taxa de Ruptura**
- Gráfico de colunas: Taxa de Ruptura ao longo do tempo
- Gráfico de barras: Cobertura de Estoque por Categoria
- Tabela dinâmica (pivot) de Estoque de Segurança e Ponto de Pedido por loja/produto
- Gráfico de dispersão relacionando perda por validade, cobertura de estoque e prazo de validade dos produtos perecíveis

### 3. Fornecedores & Compra
Avaliação de performance de fornecedores:
- Cards de **Confiabilidade Fornecedor (Real)**, **Custo Unitário Médio de Compra**, **Valor Total** e **Lead Time Médio (dias)**
- Gráfico de dispersão: Custo Unitário x Lead Time x Confiabilidade por fornecedor

### 4. Transporte & Logística
Indicadores de transportadoras e distribuição:
- Cards de **Lead Time Ponta a Ponta (dias)**, **Fill Rate de Abastecimento**, **OTIF %** e **Confiabilidade Transportadora (Real)**
- Gráfico de pizza: Confiabilidade por transportadora
- Tabela com Custo por KM, Confiabilidade, Cargas Totais e OTIF % por transportadora
- **Visual em Python (matplotlib)**: mapa do estado de São Paulo com a localização das lojas e do centro de distribuição, plotado a partir de latitude/longitude de cada loja

### 5. Previsão & Tendência
Análise exploratória de causas de ruptura:
- **Key Influencers** (visual de IA do Power BI) para identificar os principais fatores que influenciam a **Taxa de Ruptura**, cruzando Categoria, Classe de Popularidade, Cidade, Dia da Semana e Transportadora

## Modelo de dados

Modelagem em **esquema estrela**, com uma tabela fato e cinco dimensões, além de uma tabela dedicada de medidas:

| Tabela | Papel |
|---|---|
| `Fato_Compras` | Fato central — compras/abastecimento |
| `Dim_Produtos` | Produtos (categoria, classe de popularidade, perecibilidade, prazo de validade) |
| `Dim_Lojas` | Lojas (nome, cidade, latitude/longitude) |
| `Dim_Fornecedores` | Fornecedores |
| `Dim_Transportadoras` | Transportadoras |
| `Dim_Calendario` | Calendário (data, dia da semana) |
| `Medidas` | Tabela de medidas DAX centralizadas |

### Principais medidas (DAX)

**Vendas & Receita**
- Vendas (Unidades)
- Receita Total

**Estoque & Ruptura**
- Taxa de Ruptura
- Dias até Ruptura Projetada
- Cobertura de Estoque (dias)
- Giro de Estoque
- Estoque de Segurança
- Ponto de Pedido
- Perda por Validade (Unidades)

**Fornecedores & Compra**
- Confiabilidade Fornecedor (Real)
- Custo Unitário Médio de Compra
- Lead Time Fornecedor - Real (dias)

**Transporte & Logística**
- OTIF %
- Fill Rate Abastecimento
- Lead Time Ponta a Ponta (dias)
- Confiabilidade Transportadora (Real)
- Cargas Totais
- Custo por KM

## Tecnologias

- **Power BI** (relatório criado/editado via Power BI Service — Fabric, versão 2026.07)
- **DAX** para as medidas do modelo
- **Python (matplotlib)** para o visual customizado de mapa geográfico das lojas
- Tema visual customizado da Rede Estrela
