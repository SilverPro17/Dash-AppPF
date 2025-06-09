# Relatório Completo: Exploração Interativa da Distribuição de Plâncton

## 1. Introdução

Este projeto visa desenvolver uma aplicação web interativa para a exploração e análise de dados de distribuição de plâncton, complementados por dados ambientais como a Temperatura da Superfície do Mar (SST) e Clorofila-a. O objetivo principal é proporcionar uma ferramenta que permita aos investigadores e interessados na área da oceanografia biológica visualizar padrões de distribuição de plâncton, analisar tendências temporais e explorar possíveis correlações com variáveis ambientais.

O plâncton desempenha um papel crucial nos ecossistemas marinhos como base da cadeia alimentar e como indicador sensível de mudanças ambientais, incluindo alterações climáticas. A compreensão da sua distribuição espacial e temporal é, portanto, de grande importância para a gestão dos recursos marinhos e para a previsão de impactos das alterações globais nos oceanos.

Este projeto utiliza dados do Continuous Plankton Recorder (CPR), um dos programas de monitorização marinha mais antigos e abrangentes do mundo, que recolhe amostras de plâncton ao longo de rotas marítimas comerciais desde 1931. Estes dados são complementados por medições de temperatura da superfície do mar obtidas através de satélites, permitindo uma análise integrada da distribuição do plâncton em relação a este importante parâmetro ambiental.

## 2. Revisão de Literatura

### 2.1 Importância do Plâncton nos Ecossistemas Marinhos

O plâncton, composto por organismos que vivem em suspensão na coluna de água e têm capacidade limitada de locomoção contra as correntes, é fundamental para os ecossistemas marinhos. O fitoplâncton (plâncton vegetal) é responsável por aproximadamente 50% da produção primária global, convertendo dióxido de carbono em matéria orgânica através da fotossíntese. O zooplâncton (plâncton animal) constitui o elo entre os produtores primários e os níveis tróficos superiores, sendo alimento para peixes, mamíferos marinhos e outros organismos (Falkowski, 2012).

### 2.2 O Continuous Plankton Recorder (CPR) Survey

O CPR Survey, iniciado em 1931 por Alister Hardy, é um dos programas de monitorização marinha mais longos e consistentes do mundo. Utiliza um dispositivo (o CPR) rebocado por navios comerciais a uma profundidade aproximada de 10 metros, que filtra e preserva o plâncton em uma fita de seda contínua. Este método permite a amostragem em vastas áreas oceânicas e a criação de séries temporais extensas, essenciais para a deteção de mudanças de longo prazo nas comunidades planctónicas (Richardson et al., 2006).

### 2.3 Relação entre Plâncton e Variáveis Ambientais

Diversos estudos têm demonstrado a sensibilidade do plâncton a variáveis ambientais, particularmente à temperatura. Beaugrand et al. (2002) documentaram mudanças significativas na distribuição de espécies de copépodes no Atlântico Norte em resposta ao aquecimento das águas. Edwards e Richardson (2004) observaram alterações na fenologia (timing sazonal) de diferentes grupos de plâncton em resposta a mudanças na temperatura, com potenciais impactos na sincronização trófica dos ecossistemas marinhos.

### 2.4 Visualização e Análise Interativa de Dados Ecológicos

A visualização interativa tem-se tornado uma ferramenta cada vez mais importante na ecologia e nas ciências ambientais, permitindo a exploração de conjuntos de dados complexos e multidimensionais. Plataformas como o Dash (Python) e o Shiny (R) têm facilitado o desenvolvimento de aplicações web para visualização científica, democratizando o acesso a dados e análises (Perkel, 2018).

## 3. Descrição dos Datasets

### 3.1 Continuous Plankton Recorder (CPR)

**Fonte:** Global Biodiversity Information Facility (GBIF)  
**Formato:** Darwin Core Archive (DwC-A)  
**Tamanho:** ~3.2GB (ficheiro occurrence.txt)  
**Conteúdo:** Registos de ocorrência de espécies de plâncton, incluindo:
- Coordenadas geográficas (latitude, longitude)
- Data e hora da coleta
- Identificação taxonómica (espécie, género, família)
- Contagem de indivíduos
- Metadados associados (profundidade, método de amostragem, etc.)

O dataset contém milhões de registos cobrindo principalmente o Atlântico Norte e o Mar do Norte, com algumas amostras de outras regiões oceânicas. Para este projeto, foi utilizada uma amostra representativa para viabilizar a análise interativa.

### 3.2 Temperatura da Superfície do Mar (SST)

**Fonte:** NOAA Optimum Interpolation Sea Surface Temperature V2 High Resolution  
**Formato:** NetCDF4  
**Resolução:** 0.25° (alta resolução)  
**Cobertura temporal:** 1981-presente  
**Conteúdo:** Dados globais de temperatura da superfície do mar em grade regular, derivados de múltiplas fontes (satélites, boias, navios) e interpolados para fornecer cobertura global.

### 3.3 Clorofila-a (Pendente)

**Fonte:** NASA OceanColor Aqua-MODIS L3 Mapped  
**Formato:** NetCDF/HDF  
**Resolução:** 4km  
**Cobertura temporal:** 2002-presente  
**Conteúdo:** Concentração de clorofila-a na superfície do oceano, derivada de sensores de cor do oceano a bordo de satélites.

## 4. Metodologia

### 4.1 Aquisição e Pré-processamento de Dados

#### 4.1.1 Dados de Plâncton (CPR)
- Download do dataset em formato Darwin Core Archive do GBIF
- Extração e processamento do ficheiro occurrence.txt em chunks devido ao seu tamanho
- Limpeza de dados: remoção de registos com coordenadas ou datas inválidas, tratamento de valores ausentes
- Conversão de tipos de dados (datas, coordenadas, contagens)
- Criação de uma amostra representativa para análise interativa

#### 4.1.2 Dados de Temperatura da Superfície do Mar (SST)
- Download do dataset NetCDF da NOAA
- Carregamento e processamento usando xarray para lidar com dados multidimensionais
- Cálculo de estatísticas básicas (médias, tendências)
- Extração de séries temporais para pontos específicos

### 4.2 Análise Exploratória de Dados (EDA)

#### 4.2.1 Análise do Dataset de Plâncton
- Estatísticas descritivas gerais (número de registos, cobertura temporal, espacial)
- Identificação das espécies mais frequentes
- Análise da distribuição temporal (registos por ano)
- Visualização da distribuição espacial (mapa de ocorrências)

#### 4.2.2 Análise do Dataset de SST
- Visualização da distribuição espacial da temperatura média
- Análise de séries temporais para regiões específicas
- Identificação de tendências e padrões sazonais

### 4.3 Desenvolvimento da Aplicação Web

#### 4.3.1 Estrutura e Design
- Utilização do framework Dash (Python) para desenvolvimento da aplicação web
- Organização do conteúdo em abas temáticas para facilitar a navegação
- Design responsivo e intuitivo

#### 4.3.2 Componentes Interativos
- Filtros para seleção de espécies e intervalo temporal
- Gráficos interativos para visualização de tendências temporais
- Mapa interativo para exploração da distribuição espacial
- Visualização da correlação entre abundância de plâncton e temperatura

## 5. Resultados e Discussão

### 5.1 Análise Exploratória do Dataset de Plâncton

A análise exploratória revelou uma rica diversidade de espécies no dataset CPR, com predominância de copépodes como *Calanus finmarchicus* e *Calanus helgolandicus*, espécies-chave nos ecossistemas do Atlântico Norte. A distribuição temporal dos registos mostra uma cobertura extensa desde a década de 1950, com variações no esforço de amostragem ao longo dos anos.

A visualização espacial das ocorrências evidencia a concentração de amostragem no Atlântico Norte e Mar do Norte, refletindo as rotas comerciais utilizadas para o reboque dos dispositivos CPR. Esta distribuição não uniforme da amostragem é uma limitação importante a considerar na interpretação dos resultados.

### 5.2 Análise da Temperatura da Superfície do Mar

Os dados de SST mostram o padrão global esperado de temperaturas mais elevadas nos trópicos e mais baixas nas regiões polares. A análise de séries temporais para pontos específicos revela tendências de aquecimento em várias regiões, consistentes com o aquecimento global documentado na literatura científica.

### 5.3 Correlação entre Plâncton e Temperatura

A análise preliminar da relação entre abundância de plâncton e temperatura sugere respostas específicas por espécie. Algumas espécies mostram correlação negativa com a temperatura (diminuindo em abundância com o aumento da temperatura), enquanto outras apresentam correlação positiva ou não mostram relação clara.

Estas observações são consistentes com estudos anteriores que documentaram a sensibilidade diferencial de espécies de plâncton à temperatura, com espécies de águas frias sendo negativamente afetadas pelo aquecimento e espécies de águas quentes expandindo sua distribuição para o norte em resposta ao aquecimento dos oceanos (Beaugrand et al., 2002).

## 6. Conclusões e Trabalho Futuro

### 6.1 Principais Conclusões

Este projeto demonstrou a viabilidade e utilidade de uma aplicação web interativa para a exploração de dados de distribuição de plâncton em relação a variáveis ambientais. A integração de dados do CPR com dados de temperatura da superfície do mar permite uma análise visual das relações entre estes parâmetros, facilitando a identificação de padrões e tendências.

A análise exploratória confirmou observações da literatura sobre a sensibilidade do plâncton à temperatura, com respostas específicas por espécie. A aplicação desenvolvida proporciona uma ferramenta acessível para investigadores e estudantes explorarem estes padrões de forma intuitiva.

### 6.2 Limitações

- A distribuição não uniforme da amostragem no dataset CPR, concentrada em certas regiões e rotas, limita a generalização dos resultados.
- A resolução temporal e espacial dos dados ambientais nem sempre corresponde exatamente à dos dados biológicos, introduzindo potenciais imprecisões nas análises de correlação.
- O tamanho do dataset completo impõe desafios computacionais, exigindo o uso de amostras para análise interativa em tempo real.

### 6.3 Trabalho Futuro

- Integração de dados de Clorofila-a para análise da relação entre plâncton e produtividade primária.
- Implementação de modelos de machine learning para previsão de abundância de plâncton com base em variáveis ambientais.
- Expansão da aplicação para incluir análises estatísticas mais avançadas (ex: análise de séries temporais, modelação espacial).
- Desenvolvimento de funcionalidades para comparação direta entre diferentes regiões oceânicas ou períodos temporais.
- Integração de dados de outros programas de monitorização de plâncton para aumentar a cobertura espacial e temporal.

## 7. Referências

Beaugrand, G., Reid, P. C., Ibañez, F., Lindley, J. A., & Edwards, M. (2002). Reorganization of North Atlantic marine copepod biodiversity and climate. *Science*, 296(5573), 1692-1694.

Edwards, M., & Richardson, A. J. (2004). Impact of climate change on marine pelagic phenology and trophic mismatch. *Nature*, 430(7002), 881-884.

Falkowski, P. G. (2012). Ocean Science: The power of plankton. *Nature*, 483(7387), S17-S20.

Perkel, J. M. (2018). Data visualization tools drive interactivity and reproducibility in online publishing. *Nature*, 554(7690), 133-134.

Richardson, A. J., Walne, A. W., John, A. W. G., Jonas, T. D., Lindley, J. A., Sims, D. W., ... & Witt, M. (2006). Using continuous plankton recorder data. *Progress in Oceanography*, 68(1), 27-74.
