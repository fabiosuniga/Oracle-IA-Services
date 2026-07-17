# Motor de Busca Semântica Corporativa (AI Vector Search)

![Oracle APEX](https://img.shields.io/badge/Oracle_APEX-E51B24?style=for-the-badge&logo=oracle&logoColor=white)
![Oracle 23ai](https://img.shields.io/badge/Oracle_23ai-F80000?style=for-the-badge&logo=oracle&logoColor=white)
![PL/SQL](https://img.shields.io/badge/PL/SQL-00758F?style=for-the-badge&logo=oracle&logoColor=white)
![Cohere AI](https://img.shields.io/badge/Cohere_API-3959A6?style=for-the-badge&logo=artificial-intelligence&logoColor=white)

## Sobre o Projeto

Este projeto é uma aplicação *full-stack* para demonstrar algumas ferramentas Oracle e seu uso na prática. IA generativa configurada apenas para nos tirar dúvidas de assuntos envolvendo PL/SQL e SQL Oracle.
OCI Vision que foi configurado para extrair textos de imagens, e o Vector Search que foi configurado para realizar buscas semânticas e nos retornar com os funcionários mais adeptos para a tarefa desejada.

📹 **[Clique aqui para ver o vídeo da aplicação funcionando no YouTube]** 
---

## Arquitetura e Tecnologias

A aplicação foi separada em camadas claras de responsabilidade:

*   **Frontend / View (Oracle APEX):** Utilizado como interface gráfica *low-code* para acelerar a entrega da camada de apresentação.
*   **Backend / Controller (PL/SQL):** Responsável por orquestrar regras de negócio, chamadas RESTful, tratamento de erros e processamento de JSON/CLOBs.
*   **Banco de Dados (Oracle 23ai):** Armazenamento nativo dos vetores multidimensionais gerados pela IA e cálculo de distância utilizando funções vetoriais.
*   **Inteligência Artificial (Cohere API):** Utilização do modelo `embed-multilingual-v3.0` para converter a linguagem humana e os perfis corporativos em matemática pura (*Embeddings* de 1024 dimensões).

---

## Estrutura do Repositório

Neste repositório, destaquei o código fonte do backend que sustenta a inteligência da aplicação:

*   `chamar-OCI-VISION`: Script em PL/SQL que chama o serviço de Visão da Oracle diretamente em nossa aplicação APEX.
*   `chamar-ia-generativa`: Script em PL/SQL que envia a pergunta do usuário para a Oracle, e a Oracle retorna uma resposta do modelo Cohere previamente configurado.
*   `treinamento-VETOR-SEARCH`: Regras de negócio em T-SQL/PL/SQL utilizadas para enriquecer a base de dados corporativa antes de enviá-la para a IA.
*   `rag`: Busca vetorial onde utilizamos uma tabela com regras de negócio onde o usuário pode consultar, editar, criar ou deletar diretamente pela aplicação.

