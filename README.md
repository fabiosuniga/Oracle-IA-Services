# Motor de Busca Semântica Corporativa (AI Vector Search)

![Oracle APEX](https://img.shields.io/badge/Oracle_APEX-E51B24?style=for-the-badge&logo=oracle&logoColor=white)
![Oracle 23ai](https://img.shields.io/badge/Oracle_23ai-F80000?style=for-the-badge&logo=oracle&logoColor=white)
![PL/SQL](https://img.shields.io/badge/PL/SQL-00758F?style=for-the-badge&logo=oracle&logoColor=white)
![Cohere AI](https://img.shields.io/badge/Cohere_API-3959A6?style=for-the-badge&logo=artificial-intelligence&logoColor=white)

## Sobre o Projeto

Este projeto é uma aplicação *full-stack* projetada para substituir buscas tradicionais baseadas em palavras-chave (`LIKE '%termo%'`) por um **Motor de Busca Semântica**. Em vez de buscar por textos exatos, o sistema entende a **intenção** do usuário utilizando Inteligência Artificial Generativa e *Embeddings* nativos em banco de dados.

Se um usuário pesquisar por *"preciso de ajuda, o servidor caiu"*, o sistema não procura a palavra "servidor", mas sim compreende o contexto e retorna os funcionários do departamento de Tecnologia da Informação (IT).

📹 **[Clique aqui para ver o vídeo da aplicação funcionando no YouTube]** 
*(Nota: Grave um vídeo curto mostrando a tela e coloque o link aqui)*

---

## Arquitetura e Tecnologias

A aplicação foi separada em camadas claras de responsabilidade:

*   **Frontend / View (Oracle APEX):** Utilizado como interface gráfica *low-code* para acelerar a entrega da camada de apresentação.
*   **Backend / Controller (PL/SQL):** Responsável por orquestrar regras de negócio, chamadas RESTful, tratamento de erros e processamento de JSON/CLOBs.
*   **Banco de Dados (Oracle 23ai):** Armazenamento nativo dos vetores multidimensionais gerados pela IA e cálculo de distância utilizando funções vetoriais.
*   **Inteligência Artificial (Cohere API):** Utilização do modelo `embed-multilingual-v3.0` para converter a linguagem humana e os perfis corporativos em matemática pura (*Embeddings* de 1024 dimensões).

---

## Principais Desafios e Soluções (Engenharia de Software)

Desenvolver com IA exige mais do que apenas consumir chamadas HTTP. Durante o desenvolvimento deste motor, enfrentei e solucionei desafios reais de arquitetura:

### 1. Ambiguidade Semântica e Engenharia de Prompt (Data Enrichment)
Modelos multilíngues podem sofrer com diluição de contexto. Uma busca por "contratações" inicialmente retornava o departamento de Compras (*Purchasing*) em vez de Recursos Humanos (*HR*).
**Solução:** Implementei um processo de **Enriquecimento de Dados** no backend, gerando descrições ricas e focadas em ações em português para cada departamento antes de convertê-las em vetores, eliminando pontes falsas de idioma.

### 2. Tratamento de Rate Limits (Bloqueios de API)
Ao popular o banco de dados em lote, a API da nuvem bloqueava requisições simultâneas massivas (Erro HTTP 429 - *Too Many Requests*).
**Solução:** Refatorei o script de atualização vetorial criando um *loop* transacional com tratamento de exceções robusto e pausas lógicas programadas (`DBMS_SESSION.SLEEP`), garantindo que 100% da base fosse processada sem falhas silenciosas.

### 3. Calibragem de Similaridade (Threshold)
Retornar os "Top 5" registros nem sempre é o ideal se a IA tiver que "chutar" muito longe para preencher a lista.
**Solução:** Implementação de uma nota de corte utilizando matemática vetorial (`VECTOR_DISTANCE(..., COSINE) <= 0.55`). O sistema atua como um leão de chácara: se a distância semântica for muito alta, a busca é barrada antes de chegar na camada de visualização.

---

## Estrutura do Repositório

Neste repositório, destaquei o código fonte do backend que sustenta a inteligência da aplicação:

*   `cohere_api_integration.sql`: Scripts PL/SQL de integração com a API da Cohere, geração dinâmica de JSON payload e armazenamento do tipo *Vector* no banco.
*   `vector_search_algorithm.sql`: A lógica principal do motor de busca, mostrando o cruzamento vetorial em tempo real e o filtro lógico usando *Cosine Distance*.
*   `data_enrichment_rules.sql`: Regras de negócio em T-SQL/PL/SQL utilizadas para enriquecer a base de dados corporativa antes de enviá-la para a IA.

---

## 🤝 Contato e Redes

Sinta-se à vontade para explorar o código, clonar o repositório e dar ideias de melhoria!

*   **LinkedIn:** [Seu Nome ou Link do LinkedIn]
*   **E-mail:** [Seu e-mail profissional]
