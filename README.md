# FIAP - Faculdade de Informática e Administração Paulista

<p align="center">
<a href= "https://www.fiap.com.br/"><img src="assets/logo-fiap.png" alt="FIAP - Faculdade de Informática e Admnistração Paulista" border="0" width=40% height=40%></a>
</p>

<br>


## Grupo 67

## 👨‍🎓 Integrantes: 
- <a href="https://www.linkedin.com/in/vittor-augusto/">Vitor Augusto Gomes</a>
- <a href="https://www.linkedin.com/company/inova-fusca">João Vitor Lopes Beiro</a>
- <a href="https://www.linkedin.com/company/inova-fusca">Thyego Brandão</a> 
- <a href="https://www.linkedin.com/company/inova-fusca">Lucas Gabriel Alves Costa</a> 
- <a href="https://www.linkedin.com/company/inova-fusca">Lucas Ferreira Hillesheim</a>

## 👩‍🏫 Professores:
### Tutor(a) 
- <a href="https://www.linkedin.com/in/leonardoorabona/">Leonardo Ruiz Orabona</a>
### Coordenador(a)
- <a href="https://www.linkedin.com/in/profandregodoi/">André Godoi Chiovato</a>


## 📜 Descrição

### Projeto Challenge Ingredion - Fase 2: 🌱 Previsão de Produção Agrícola com Regressão Linear ###
Este projeto tem como objetivo prever a produção agrícola em toneladas (ton) no Brasil utilizando dados públicos reais (da CONAB, MAPA e IBGE), com variáveis derivadas calculadas a partir dos dados brutos. Utilizamos Regressão Linear para fazer a previsão do valor para o ano de 2025.


### 📊 Dados Utilizados ###
Os dados foram coletados de fontes públicas confiáveis como:

-CONAB - Companhia Nacional de Abastecimento

-MAPA - Ministério da Agricultura, Pecuária e Abastecimento

-IBGE - Instituto Brasileiro de Geografia e Estatística

O arquivo base (dados_produtividade.csv) contém as colunas:

-Ano

-Produção (ton)

-Área Plantada (ha)

-Produtividade (kg/ha)

-Fonte


### 🧪 Processamento de Dados ###
Foram realizadas as seguintes etapas de tratamento:

1. Conversão dos valores numéricos para float, substituindo vírgulas por pontos.
2. Remoção de valores ausentes (NaN).
3. Criação de variáveis derivadas:

python
 
*Produtividade estimada com base na produção e área plantada*

df_derived['Produtividade Calculada'] = (df_derived['Produção (ton)'] * 1000) / df_derived['Área Plantada (ha)']

*Variação percentual da produtividade entre os anos*

df_derived['Variação Produtividade (%)'] = df_derived['Produtividade Calculada'].pct_change() * 100

*Densidade de produção (ton/ha)*

df_derived['Densidade de Produção (ton/ha)'] = df_derived['Produção (ton)'] / df_derived['Área Plantada (ha)']



### 🤖 Modelo de Previsão ###
Utilizamos Regressão Linear com a biblioteca scikit-learn. As variáveis preditoras foram:

-Ano

-Área Plantada (ha)

-Produtividade Calculada

-Variação Produtividade (%)

-Densidade de Produção (ton/ha)

O modelo foi treinado com todos os dados históricos e utilizou a média das variáveis para realizar a previsão de 2025.

python

from sklearn.linear_model import LinearRegression

modelo = LinearRegression()
modelo.fit(X, y)

previsao_2025 = modelo.predict(dados_2025)[0]


### 📈 Resultado da Previsão ###

✅ A previsão de produção para 2025 foi:

46438.50 toneladas


### 🖼️ Gráfico da Previsão ###

![Gráfico da Previsão](document/grafico_previsao_2025.png)
![Produtividade Real vs Prevista](document/produtividade_real_vs_pvista.png)

### 🧹 Documentação do Processo de Preparação dos Dados ###

O processo de preparação dos dados envolveu várias etapas para garantir a qualidade e a consistência das informações utilizadas no modelo. Inicialmente, os dados foram carregados a partir de um arquivo CSV, com atenção especial ao separador e à codificação para lidar com possíveis variações nos formatos dos dados.​

Em seguida, foram realizadas limpezas nas colunas numéricas, substituindo vírgulas por pontos para padronizar os separadores decimais e removendo pontos utilizados como separadores de milhar. Essas colunas foram então convertidas para o tipo numérico adequado, e linhas com valores ausentes foram descartadas para evitar inconsistências no treinamento do modelo.​

Além disso, foram criadas colunas derivadas para enriquecer o conjunto de dados:​

* Produtividade Calculada (kg/ha): calculada dividindo a produção em toneladas pela área plantada em hectares e multiplicando por 1.000 para converter para kg/ha.​
* Variação da Produtividade (%): calculada como a variação percentual da produtividade calculada em relação ao ano anterior.​
* Densidade de Produção (ton/ha): obtida dividindo a produção em toneladas pela área plantada em hectares.​

Essas transformações permitiram uma análise mais aprofundada e a extração de insights relevantes para a modelagem preditiva.

### 📊 Justificativa da Escolha das Variáveis ###

A seleção das variáveis independentes para o modelo de regressão linear foi baseada na relevância e na disponibilidade dos dados. As variáveis escolhidas foram:​

* Ano: incluído para capturar tendências temporais e possíveis efeitos sazonais na produção agrícola.​
* Área Plantada (ha): representa o tamanho da área cultivada, sendo um fator direto que influencia a quantidade total de produção.​
* Produtividade Calculada (kg/ha): indicador da eficiência da produção por unidade de área, refletindo fatores como tecnologia, manejo agrícola e condições climáticas.​
* Variação da Produtividade (%): permite capturar mudanças ano a ano na produtividade, indicando melhorias ou declínios na eficiência produtiva.​
* Densidade de Produção (ton/ha): oferece uma medida adicional da produtividade, considerando a produção total em relação à área plantada.​

Essas variáveis foram selecionadas por sua capacidade de representar fatores críticos que afetam a produção agrícola e por estarem disponíveis de forma consistente nos dados históricos.

### 🧠 Justificativa do Modelo e Lógica Preditiva ###

Optou-se pela utilização de um modelo de regressão linear devido à sua simplicidade, interpretabilidade e adequação ao conjunto de dados disponível. A regressão linear é eficaz para identificar relações lineares entre variáveis independentes e uma variável dependente, o que é apropriado para o objetivo de prever a produção agrícola com base em fatores como área plantada e produtividade.​

A lógica preditiva do modelo consiste em ajustar uma equação linear que melhor se aproxima dos dados históricos, minimizando a soma dos erros quadráticos entre os valores previstos e os observados. Uma vez treinado, o modelo pode ser utilizado para prever a produção futura ao fornecer valores estimados para as variáveis independentes.

### 📈 Justificativa Técnica com Métricas e Gráficos ###

Para avaliar o desempenho do modelo de regressão linear, foram utilizadas as seguintes métricas:​

* Erro Absoluto Médio (MAE): mede a média dos erros absolutos entre as previsões e os valores reais, fornecendo uma indicação clara da magnitude média dos erros.​
* Coeficiente de Determinação (R²): indica a proporção da variabilidade na variável dependente que é explicada pelas variáveis independentes no modelo. Um valor de R² próximo de 1 sugere um bom ajuste do modelo aos dados.​

Além das métricas quantitativas, foram gerados gráficos para visualizar o desempenho do modelo, incluindo:​

* Gráfico de Produção Real vs. Produção Prevista: compara os valores observados com as previsões do modelo, permitindo identificar padrões e discrepâncias.​
* Gráfico de Resíduos: exibe os erros de previsão em relação aos valores previstos, ajudando a detectar heterocedasticidade ou padrões não capturados pelo modelo.​

Essas análises visuais complementam as métricas numéricas, proporcionando uma compreensão mais abrangente do desempenho do modelo.​

### 🧾 Explicação do Funcionamento do Código ###

O código do projeto segue uma estrutura sequencial que abrange todas as etapas do processo de modelagem preditiva:​

1. Importação de Bibliotecas: carrega as bibliotecas necessárias para manipulação de dados, modelagem e visualização.​
Gist

2. Carregamento e Limpeza dos Dados: lê o arquivo CSV contendo os dados brutos, realiza a limpeza e conversão de tipos para garantir a consistência dos dados.​

3. Criação de Variáveis Derivadas: calcula colunas adicionais que enriquecem o conjunto de dados e fornecem insights adicionais para o modelo.​

4. Divisão dos Dados: separa os dados em conjuntos de treino e teste para avaliar o desempenho do modelo de forma imparcial.​

5. Treinamento do Modelo: ajusta o modelo de regressão linear aos dados de treino, aprendendo os coeficientes que melhor representam as relações entre as variáveis.​

6. Avaliação do Modelo: utiliza o conjunto de teste para calcular métricas de desempenho e gerar gráficos que ilustram a eficácia do modelo.​

7. Previsão para 2025: utiliza o modelo treinado para prever a produção agrícola para o ano de 2025, com base em valores estimados das variáveis independentes.​

8. Exportação dos Resultados: salva as previsões em um arquivo CSV para posterior análise e apresentação.​

Essa estrutura modular facilita a compreensão e a manutenção do código, além de permitir futuras extensões ou ajustes no modelo.

### Códigos Google Collab ###

Os códigos/scrpits utilizados no Google Collab se encontram em */Códigos Collab.ipynb* na pasta raíz.


### 💾 Exportação Final ###

O DataFrame com os dados reais e a linha da previsão de 2025 foi exportado para:

(document/dados_com_previsao_2025.csv)

Você pode abrir o arquivo em Excel, LibreOffice, ou outro sistema para visualizar e usar os dados.

### 🛠️ Tecnologias e Bibliotecas ###

* Python 3.x
* pandas
* numpy
* scikit-learn
* matplotlib


### 🚀 Como Executar ###

1. Instale as bibliotecas com pip install pandas scikit-learn matplotlib.

2. Coloque o arquivo dados_produtividade.csv na mesma pasta do script Python.

3. Execute o script para treinar o modelo e gerar o gráfico.

4. O arquivo dados_com_previsao_2025.csv será gerado automaticamente.


### 📌 Observações ###

* O valor para 2025 é uma estimativa com base nas médias históricas.

* A precisão depende da qualidade e quantidade dos dados disponíveis.


## 📁 Estrutura de pastas

Dentre os arquivos e pastas presentes na raiz do projeto, definem-se:

- <b>.github</b>: Nesta pasta ficarão os arquivos de configuração específicos do GitHub que ajudam a gerenciar e automatizar processos no repositório.

- <b>assets</b>: aqui estão os arquivos relacionados a elementos não-estruturados deste repositório, como imagens.

- <b>config</b>: Posicione aqui arquivos de configuração que são usados para definir parâmetros e ajustes do projeto.

- <b>document</b>: aqui estão todos os documentos do projeto que as atividades poderão pedir. Na subpasta "other", adicione documentos complementares e menos importantes.

- <b>scripts</b>: Posicione aqui scripts auxiliares para tarefas específicas do seu projeto. Exemplo: deploy, migrações de banco de dados, backups.

- <b>src</b>: Todo o código fonte criado para o desenvolvimento do projeto ao longo das 7 fases.

- <b>README.md</b>: arquivo que serve como guia e explicação geral sobre o projeto (o mesmo que você está lendo agora).



## 📋 Licença

<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1"><p xmlns:cc="http://creativecommons.org/ns#" xmlns:dct="http://purl.org/dc/terms/"><a property="dct:title" rel="cc:attributionURL" href="https://github.com/agodoi/template">MODELO GIT FIAP</a> por <a rel="cc:attributionURL dct:creator" property="cc:attributionName" href="https://fiap.com.br">Fiap</a> está licenciado sobre <a href="http://creativecommons.org/licenses/by/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">Attribution 4.0 International</a>.</p>


