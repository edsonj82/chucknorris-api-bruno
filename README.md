# Chuck Norris Jokes API Automation 🚀

Este repositório contém uma coleção automatizada de testes e requisições para a **Chuck Norris Jokes API**, uma API pública de fatos satíricos sobre Chuck Norris. O projeto foi estruturado seguindo as melhores práticas de engenharia de software, utilizando o cliente de API **Bruno**, garantindo **portabilidade**, **isolamento de ambientes** e **facilidade de integração**.

## 🛠️ Tecnologias Utilizadas

- **Bruno API Client:** Ferramenta open-source para exploração e automação de requisições HTTP.
- **Git:** Gerenciamento de código (a coleção é salva diretamente como arquivos declarativos de texto puro).
- **Environments (.env):** Gerenciamento dinâmico de variáveis globais e locais.

## 🏗️ Arquitetura e Diferenciais Técnicos

### 1. Separação de Ambientes (Environment Isolation)
Como evidenciado em `image_458be4.png`, a URL base não está fixa (*hardcoded*) nas requisições. Criamos um arquivo de ambiente chamado `api.chuck.env.yml` para centralizar as configurações de infraestrutura:
* **Variável `baseURL`:** Mapeia de forma dinâmica o endereço raiz da API (`https://api.chucknorris.io`). Caso a API mude de servidor ou passe por um ambiente de homologação, a alteração é feita em um único arquivo de configuração.

### 2. Parametrização Dinâmica
Todas as chamadas na pasta utilizam a sintaxe de chaves duplas `{{baseURL}}` para herdar o endereço dinâmico (visível em `image_458b80.png`), garantindo manutenibilidade em escala profissional.

### 3. Abordagem Declarativa
Diferente de ferramentas legadas, cada requisição neste projeto é salva de forma limpa em arquivos com extensão `.bru` ou `.yml`, facilitando a leitura de diffs no code review e auditorias do Git.

## 🧪 Cenários e Endpoints Mapeados

Com base na documentação oficial de `image_458f63.png`, a coleção cobre os seguintes comportamentos da API:

### 1. Piadas Aleatórias (Random Jokes)
* **Retrieve a random chuck joke:** Busca um fato completamente aleatório no catálogo.
* **Retrieve a random chuck joke by one or more categories:** Filtra piadas aleatórias direcionadas a categorias específicas (ex: `dev`, `explicit`).

### 2. Customização e Busca Textual
* **Retrieve a random personalized chuck joke:** Permite injetar um nome customizado na requisição (ex: `?name=Bob`) para substituir o termo "Chuck Norris" dinamicamente no retorno da API.
* **Free text search:** Endpoint de busca textual flexível (`/jokes/search?query={query}`) para varreduras indexadas por palavras-chave.

### 3. Metadados do Catálogo
* **Retrieve a list of available categories:** Retorna todas as categorias oficiais válidas disponíveis para uso nos filtros.

---

## 🛡️ Estratégia de Testes e Validações

O coração desta coleção é sua suíte de testes automatizados não-funcionais, de negócio e de contrato arquitetada diretamente nas abas **Script (Post-Response)** e **Tests** do Bruno:

### 📥 1. Response Status & Headers
* **Validação de Código de Status:** Garante que o servidor respondeu com `200 OK`.
* **Mapeamento de Metadados (Content-Type):** Valida estritamente se o cabeçalho retornado é do tipo `application/json`, blindando o cliente contra quebras de formato.
* **Política de Caching:** Checa os cabeçalhos de `cache-control` para assegurar que as diretrizes de persistência temporária estão de acordo com o esperado pela infraestrutura.

### ⏱️ 2. Performance & SLA (Response Time)
* **Limite de Latência:** Uma asserção monitora o tempo de resposta do servidor em milissegundos (`res.getResponseTime()`), garantindo que nenhuma requisição ultrapasse o limite aceitável de SLA tolerado (ex: abaixo de 1500ms).

### 📐 3. Validação de Contrato (JSON Schema com Ajv)
* Em vez de utilizar abordagens legadas ou parciais, as rotas principais utilizam a biblioteca **Ajv** em modo estrito para compilar e validar o esquema JSON inteiro da resposta em uma única varredura. Campos obrigatórios como `id`, `url`, `value`, `created_at` e `categories` têm seus formatos e tipos primitivos monitorados contra quebras de contrato.

### 🔁 4. Validação Dinâmica de Coleções (Arrays)
* **Iteração com `.forEach()` (Busca Livre):** Na rota de pesquisa textual, o script faz o parse do payload e varre o array de resultados (`result`) de forma interativa. Cada item da lista gera uma asserção individualizada no relatório do Bruno, apontando cirurgicamente o índice e o ID da piada caso algum campo obrigatório venha ausente ou nulo.
* **Cruzamento de Gabarito com `.every()` (Categorias):** Na rota de listagem de categorias, o teste utiliza um array de referência estático (gabarito oficial) acoplado aos métodos JavaScript `.every()` e `.includes()`. Isso valida se 100% dos itens da lista dinâmica retornada pelo servidor pertencem ao catálogo homologado, além de aferir a integridade do tamanho total da coleção (`lengthOf`).

---

## 🏗️ Estrutura do Projeto

A organização segue o padrão do ecossistema nativo do Bruno:
```bash
├── CHUCKNORRISJOKE/
│   ├── environments/
│   │   └── api.chuck.env.yml          # Definição da variável {{baseURL}}
│   ├── Free text search.yml           # Requisição de busca livre
│   ├── Retrieve a list of available categories.yml
│   ├── Retrieve a random chuck joke.yml
│   └── opencollection.yml            # Configurações globais da coleção
└── README.md
```

## 🚀 Como Executar

Como o Bruno salva as coleções nativamente na pasta do seu projeto, a execução é extremamente simples:

1. Instale o Bruno API Client em sua máquina (via site oficial ou gerenciador de pacotes do sistema).

2. Abra o aplicativo Bruno.

3. Clique em "Open Collection" na tela inicial e selecione a pasta raiz CHUCKNORRISJOKE deste repositório.

4. No canto superior direito da interface, selecione o ambiente api.chuck.env para inicializar as variáveis.

5. Selecione qualquer requisição da barra lateral esquerda e clique em "Send" para testar as respostas em tempo real (como demonstrado na resposta com status 200 OK).

Este projeto reflete a aplicação de padrões avançados de QA Engineering, focado na criação de pipelines de CI/CD rápidos e resilientes.

---
## 👨‍💻 Autor

**Edson José dos Santos**  
SDET (Software Development Engineer in Test) & Performance Enthusiast


