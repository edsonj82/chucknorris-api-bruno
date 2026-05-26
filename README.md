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


