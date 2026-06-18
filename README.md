<header>

# Trabalho de Grafos — Logística de Merendas

_Desenvolva códigos usando o GitHub Codespaces e o Visual Studio Code!_

</header>

#🧠 Explicação Detalhada do Código

Esta seção descreve a engenharia de software utilizada no projeto, destacando como as estruturas de dados foram combinadas para atender aos requisitos operacionais e às restrições do problema.

🏢 1. Arquitetura das Estruturas de Dados (Modelagem do Grafo)

  O maior destaque técnico deste código é o uso de uma estrutura híbrida (Matriz + Lista Encadeada) para representar o      grafo de logística:
  > Aresta (Nó Secundário): Uma estrutura dinâmica que armazena o idDestino e a distancia real em quilômetros (float). Ela funciona como uma lista simplesmente encadeada de conexões para cada creche.
  > Node (Nó Principal): Representa cada vértice (creche). Armazena o nome, o id numérico e possui um ponteiro (conexoes) para a sua própria lista de arestas adjacentes.
  > Grafo (Estrutura Unificada): Une os dois mundos exigidos. Contém a matrizAdjacencia (estática, armazenando apenas 0 e 1 para checagem rápida de existência de rotas) e o ponteiro listaCreches (para gerenciar os nós e pesos de forma dinâmica).
    
🚀 Análise das Funcionalidades Principais.



  > O sistema foi modularizado em funções dedicadas, onde cada algoritmo resolve um problema específico de logística urbana:
  
📂 Carga Dinâmica de Dados (carregarGrafo)
  
  > O que faz: Abre e faz a leitura de um arquivo .txt configurado.
  > Destaque do Código: Em um único fluxo de leitura, a função inicializa a matriz com zeros, insere as creches na lista e   popula simultaneamente as duas estruturas (define 1 nas coordenadas correspondentes da matriz bidimensional e aloca os      nós de distância nas listas encadeadas das creches de origem e destino).
    
📊 Grau de Conectividade (informarNumeroConexoes)

  > O que faz: Exibe quantas rotas de saída estão disponíveis para cada unidade.
  > Destaque do Código: Utiliza a matriz estática para realizar uma checagem em tempo constante \(O(1)\) para cada par de vértices. Ao iterar pela linha correspondente à creche na matriz, ela conta rapidamente a presença do bit 1, evitando varreduras lineares complexas na memória dinâmica.

🏎️ Ordenação de Rotas por Proximidade (listarConexoesOrdenadas)

  > O que faz: Lista os vizinhos de uma creche em ordem crescente de distância.
  > Destaque do Código: Esta é uma das partes mais sofisticadas do programa. A função faz uma cópia das conexões para uma lista encadeada auxiliar temporária (AuxNode). Durante a própria cópia, ela aplica o algoritmo de Inserção Ordenada. Os elementos já entram na memória na posição correta (menor para o maior), limpando e liberando (free) a memória temporária logo após a exibição para evitar vazamento de memória (memory leak).

📏 Consulta de Distâncias Inteligente (informarDistancia)

  > O que faz: Informa a quilometragem exata entre duas creches fornecidas por nome.
  > Destaque do Código: Aplica um filtro de validação em duas etapas:Localiza os IDs internos através de buscas de strings (buscarIdPorNome).
  > Consulta a matriz estática para ver se a rota existe. Se o valor for 0, o programa responde imediatamente que não há conexão, sem gastar processamento percorrendo listas. Se for 1, ele faz a busca precisa do float na lista dinâmica através da função obterDistanciaLista.

🛣️ Expansão da Malha Logística (incluirNovaConexao)

  > O que faz: Insere uma nova estrada/rota no sistema em tempo de execução.
  > 

Destaque do Código: Garante a integridade dos dados ao atualizar as duas estruturas ao mesmo tempo. Ela altera os índices correspondentes na matriz estática para 1 e faz a alocação dinâmica da nova Aresta com a distância informada, tornando a nova rota disponível imediatamente para consultas e ordenações.

<footer>

---

Obtenha ajuda: [Acesse nosso fórum de discussões](https://github.com/orgs/skills/discussions/categories/code-with-codespaces) &bull; [Status do GitHub](https://www.githubstatus.com/)

&copy; 2026 GitHub &bull; [Código de Conduta](https://www.contributor-covenant.org/version/2/1/code_of_conduct/code_of_conduct.md) &bull; [Licença MIT](https://gh.io/mit)

</footer>
