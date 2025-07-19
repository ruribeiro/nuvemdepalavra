# nuvemdepalavra
# **Relatório de Desenvolvimento de Projeto: Análise de Tópicos em Redes Sociais com Nuvem de Palavras**

**Data:** 16 de julho de 2025

**Autor:** RAFAEL UCHÔA RIBEIRO

## **1. Introdução e Objetivo**

Este relatório detalha o processo de desenvolvimento de um projeto cujo objetivo, conforme a "Avaliação de Prática e Laboratório II", é gerar uma nuvem de palavras para analisar dados de uma rede social. O projeto foi conduzido utilizando a linguagem de programação Python e suas bibliotecas especializadas, com uma etapa obrigatória de pré-processamento dos dados coletados antes da visualização.

O objetivo final é criar uma representação visual (nuvem de palavras) que destaque os termos mais frequentes em discussões online, permitindo uma análise qualitativa dos temas em voga em uma determinada comunidade.

## **2. Metodologia e Fases do Projeto**

O projeto foi estruturado em quatro fases principais:

1.  **Fase 1: Exploração e Seleção da Plataforma de Dados:** Avaliação de diferentes redes sociais para a coleta de dados.
2.  **Fase 2: Coleta de Dados:** Implementação de um script para extrair dados da plataforma escolhida.
3.  **Fase 3: Pré-processamento e Limpeza dos Dados:** Tratamento do texto bruto para remover ruídos e prepará-lo para análise.
4.  **Fase 4: Geração e Visualização da Nuvem de Palavras:** Utilização dos dados processados para criar a representação gráfica final.

## **3. Execução do Projeto**

### **3.1. Fase 1: Exploração e Seleção da Plataforma**

A escolha da fonte de dados é um passo crítico que impacta a viabilidade e a estabilidade do projeto. Três plataformas foram consideradas:

* **Twitter/X:** A primeira abordagem considerou o uso da API oficial do Twitter. No entanto, devido a mudanças recentes na plataforma que restringiram o acesso gratuito, explorou-se o método de Web Scraping com a biblioteca `Selenium`. Embora funcional, concluiu-se que esta abordagem era frágil e violava os termos de serviço da plataforma, sendo inadequada para um projeto robusto.

* **Instagram:** A possibilidade de extrair dados do Instagram foi avaliada. Esta opção foi rapidamente descartada devido a desafios técnicos intransponíveis para este projeto: a necessidade de login obrigatório, a estrutura do site ofuscada e, principalmente, as agressivas medidas anti-automação da plataforma, que representavam um alto risco de bloqueio da conta utilizada.

* **Reddit (Plataforma Escolhida):** O Reddit foi selecionado como a plataforma ideal. A decisão foi baseada em suas vantagens claras:
    * **API Pública e Acessível:** O Reddit oferece uma API bem-documentada e amigável para desenvolvedores.
    * **Biblioteca Especializada (`PRAW`):** A existência da biblioteca `PRAW` (Python Reddit API Wrapper) simplifica drasticamente a autenticação e a coleta de dados.
    * **Riqueza de Conteúdo:** A estrutura em comunidades (subreddits) permite focar a análise em nichos de interesse específicos, gerando resultados mais coesos.

### **3.2. Fase 2: Coleta de Dados do Reddit**

Após a escolha do Reddit, o processo de coleta foi implementado da seguinte forma:

1.  **Autenticação na API:** Foi criada uma aplicação do tipo *`script`* no portal de desenvolvedores do Reddit para obter as credenciais necessárias: `client_id` e `client_secret`.
2.  **Desenvolvimento do Script:** Utilizando a biblioteca `PRAW`, um script em Python foi desenvolvido para se autenticar na API com as credenciais obtidas, além do nome de usuário e senha da conta.
3.  **Extração de Dados:** O script foi configurado para se conectar a um subreddit específico (ex: `r/brasil`) e extrair o conteúdo textual dos títulos dos posts mais populares ("hot") e dos comentários mais relevantes de cada post.

> **Observação:** Durante esta fase, foi encontrado um erro comum (`401 Unauthorized`), que indicava falha na autenticação. O problema foi solucionado revisando e corrigindo as credenciais fornecidas ao script, garantindo que correspondiam exatamente às geradas no portal do Reddit.

### **3.3. Fase 3: Pré-processamento dos Dados**

Esta etapa foi crucial para garantir a qualidade da nuvem de palavras. O texto bruto coletado do Reddit continha muitos elementos que poderiam poluir a análise. O script realizou as seguintes tarefas de limpeza:

1.  **Normalização:** Todo o texto foi convertido para letras minúsculas para garantir que palavras como "Governo" e "governo" fossem tratadas como uma só.
2.  **Remoção de Ruídos:** Foram removidos URLs, menções a outros usuários, pontuações e caracteres especiais, mantendo apenas o conteúdo textual relevante.
3.  **Remoção de Stopwords:** Foi utilizada uma lista de "stopwords" (palavras comuns sem valor semântico, como "de", "a", "o", "que", "e", "para") em português. Essas palavras foram filtradas para que não ofuscassem os termos realmente importantes na visualização.

### **3.4. Fase 4: Geração da Nuvem de Palavras**

Com os dados limpos e processados, a etapa final foi a visualização:

1.  **Utilização da Biblioteca `WordCloud`:** O texto processado foi fornecido à biblioteca `WordCloud`.
2.  **Criação da Imagem:** A biblioteca calculou a frequência de cada palavra e gerou uma imagem onde o tamanho de cada termo é diretamente proporcional à sua frequência nos dados coletados.
3.  **Exibição e Salvamento:** A imagem foi exibida utilizando a biblioteca `Matplotlib` e salva como um arquivo `.png`, concluindo o objetivo do projeto.

## **4. Conclusão**

O projeto foi concluído com sucesso, seguindo uma metodologia estruturada de avaliação de plataformas, coleta de dados via API, pré-processamento rigoroso e visualização. A escolha do Reddit como fonte de dados provou-se a mais eficiente e estável. A nuvem de palavras resultante oferece um panorama visual claro e imediato sobre os principais assuntos discutidos na comunidade online selecionada, cumprindo todos os requisitos da avaliação.

---
