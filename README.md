# Análise Espacial dos Preços de Airbnb no Rio de Janeiro

## 📋 Sobre o Projeto

Este projeto investiga os determinantes espaciais e estruturais dos preços de anúncios do Airbnb no município do Rio de Janeiro. A análise examina como a localização (Áreas de Planejamento) e o tipo de acomodação afetam os valores cobrados, utilizando dados reais de anúncios e mapas da cidade.

## 🎯 Objetivos

- Analisar a distribuição espacial dos preços de Airbnb no Rio de Janeiro
- Identificar prêmios de localização entre as Áreas de Planejamento (APs)
- Avaliar o impacto do tipo de quarto (inteiro, privado, compartilhado, hotel) nos preços
- Mapear a concentração geográfica dos anúncios na cidade

## 🗺️ Dados Utilizados

| Fonte | Descrição |
|-------|-----------|
| **Inside Airbnb** | Listagens de anúncios com preços, tipo de quarto, avaliações e coordenadas |
| **brazilmaps (pacote R)** | Shapefile do município do Rio de Janeiro |
| **Data.Rio** | Limites oficiais dos bairros e Áreas de Planejamento |

## 📊 Principais Resultados

1. **Hierarquia espacial clara**: A Zona Sul (AP2) apresenta o maior prêmio de localização, seguida pela Barra/Jacarepaguá (AP4)
2. **Tipo de quarto importa**: Unidades inteiras têm preços significativamente maiores que quartos compartilhados
3. **Centro é referência intermediária**: A AP1 (Centro) serve como categoria base, com preços médios
4. **Zona Norte (AP3)** tem preços mais baixos, refletindo menor turismo
5. **Zona Oeste (AP5)** é heterogênea, misturando áreas valorizadas como Recreio com bairros periféricos

## 🛠️ Tecnologias Utilizadas

- **Linguagem**: R 4.x
- **Principais pacotes**:
  - `ggplot2` + `ggridges` → visualizações
  - `dplyr` → manipulação de dados
  - `sf` → análise espacial
  - `brazilmaps` → mapas do Brasil
  - `viridis` → paletas de cores acessíveis


## 🔍 Etapas da Análise

### 1. Manipulação dos Dados
- Carregamento da base `listings.csv`
- Conversão de variáveis categóricas (`neighbourhood_group`, `neighbourhood`, `room_type`)
- Tratamento de valores ausentes (`NA`) na variável `price`
- Criação da geometria espacial com `sf` a partir de latitude e longitude
- Uso de limite de bairros disponibilizado pelo https://www.data.rio/

### 2. Exploração dos Dados
- Estatísticas descritivas: média, mediana e moda de preços e noites mínimas
- Distribuição de frequência dos tipos de acomodação
- Top 10 bairros mais frequentes, mais caros e mais baratos
- Histogramas, densidades e gráficos de violino para `price` e `minimum_nights`
- Visualizações segmentadas por tipo de quarto

### 3. Análises Espaciais e de Correlação
- Mapa da estrutura urbana do Rio de Janeiro (Áreas de Planejamento)
- Mapa de concentração dos anúncios de Airbnb na cidade
- Mapa de preço médio por bairro
- Sobreposição dos pontos de anúncios com os limites das APs
- Cruzamento dos dados de anúncios com shapefile de bairros (left join espacial)

### 4. Modelagem Estatística
- Modelo 1: `log(price) ~ area_plane` — efeito puro da localização
- Modelo 2: `log(price) ~ area_plane + room_type` — adiciona tipo de quarto
- Modelo 3: `log(price) ~ area_plane + room_type + number_of_reviews_ltm` — controle de reputação

### 🚧 Próximos Passos (em desenvolvimento)
- Métodos de **Econometria Espacial**:
  - Matriz de vizinhança espacial (W)
  - Teste de autocorrelação espacial (I de Moran)
  - Modelos SAR (Spatial Autoregressive) e SEM (Spatial Error Model)
  - Controle de dependência espacial nos resíduos
