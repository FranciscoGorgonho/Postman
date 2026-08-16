# 🚀 Postman Student Expert & Library API v2

Olá! Me chamo Francisco e sou QA Analyst.

Desenvolvi este repositório para consolidar e compartilhar as coleções de testes de API criadas durante a minha jornada de certificação como **Postman Student Expert**, concluída em **Abril/2023**. Aqui você encontrará conjuntos de requisições HTTP, scripts de pré-requisição (*pre-request scripts*), testes de validação automatizados e fluxos avançados de execução em API REST.

---

## 📌 Sobre o Projeto

O objetivo principal deste repositório é servir como referência prática para automação e validação de requisições utilizando o Postman e o Newman. O projeto contém duas coleções principais:

1. **Postman Library API v2**: Coleção focada na automação CRUD completa de um sistema de biblioteca (gerenciamento de livros), manipulando parâmetros de busca, cabeçalhos de autenticação via *API Key*, armazenamento dinâmico de IDs em variáveis de coleção e testes de submissão do curso.
2. **Student Expert Training**: Coleção desenvolvida durante o treinamento oficial da Postman, cobrindo conceitos essenciais de requisições HTTP, scripts de teste avançados, manipulação dinâmica de variáveis de ambiente e controle de fluxo de execução (*collection runner*).

---

## 🛠️ Funcionalidades e Cobertura de Testes

### 📚 1. Postman Library API v2
- **Listagem de Livros (`GET /books`)**: Consulta geral do acervo.
- **Filtro Avançado (`GET /books?genre=fiction&checkedOut=false`)**: Uso de Query Parameters para busca segmentada.
- **Busca por ID (`GET /books/:id`)**: Utilização de Path Variables dinâmicas.
- **Cadastro de Livro (`POST /books`)**: Envio de payload JSON e captura automática do `id` retornado para uso em requisições subsequentes.
- **Atualização / Empréstimo (`PATCH /books/:id`)**: Alteração parcial do status do livro.
- **Remoção de Livro (`DELETE /books/:id`)**: Deleção de registros cadastrados.
- **Validação de Habilidades (`POST /skillcheck`)**: Autenticação via header e manipulação de scripts de resposta.

### 🧪 2. Student Expert Training
- **Verbos HTTP Básicos**: Exemplos práticos de `GET`, `POST`, `PUT` e `DELETE` no endpoint de gerenciamento de partidas (`/matches`).
- **Scripts e Execução em Lote**: Validação de *status code 200*, parsing de JSON, extração aleatória de dados e uso do comando `postman.setNextRequest()` para alteração dinâmica da sequência de testes.
- **Testes Automatizados de Coleção**: Suíte interna que valida a integridade da própria coleção (presença de autenticação, tipos de requisições utilizados e variáveis configuradas).

---

## 📋 Pré-requisitos

Para importar e executar as coleções localmente ou via terminal, você precisará de:

- **[Postman Desktop App](https://www.postman.com/downloads/)** (ou versão web)
- **[Node.js](https://nodejs.org/)** (v18 ou superior)
- **[Newman](https://www.npmjs.com/package/newman)** e **[Newman Reporter HTMLEXTRA](https://www.npmjs.com/package/newman-reporter-htmlextra)** (para execução via CLI e geração de relatórios)

---

## 🔧 Como Importar e Configurar

### 1. Clonar o repositório
```bash
git clone https://github.com/seu-usuario/postman-student-expert.git
cd postman-student-expert
```

### 2. Importar no Postman
1. Abra a aplicação do **Postman**.
2. Clique no botão **Import** (canto superior esquerdo).
3. Selecione os arquivos JSON do projeto:
   - `Postman Library API v2.postman_collection.json`
   - `Student expert.postman_collection.json`

### 3. Configurar Variáveis
As coleções utilizam variáveis de coleção para dinamicidade dos testes. Certifique-se de preencher ou ajustar os valores na aba **Variables** de cada coleção:
- `baseUrl`: URL base da API de livros.
- `email_key`: Seu e-mail de identificação nos testes.
- `skillcheckBaseUrl`: `https://postman-echo.com/post`

---

## 🚀 Como Executar os Testes

### 1. Execução na Interface Gráfica (Postman GUI)
1. Selecione a coleção desejada no menu lateral esquerdo.
2. Clique no ícone de opções (`...`) ao lado da coleção e escolha **Run collection**.
3. Escolha a ordem das requisições ou mantenha a padrão.
4. Clique no botão **Run [Nome da Coleção]**.

### 2. Execução via Linha de Comando (Newman CLI)
Caso queira rodar os testes sem abrir a interface gráfica do Postman, utilize o Newman:

```bash
# Instalação global do Newman (caso ainda não tenha)
npm install -g newman

# Execução de uma coleção
newman run "Postman Library API v2.postman_collection.json"
```

### 📊 3. Geração de Relatórios Visuais em HTML (Newman HTMLEXTRA)
Para gerar relatórios completos com gráficos dashboard de aprovação, tempos de resposta e detalhes de payloads:

1. Instale o plugin de relatórios:
   ```bash
   npm install -g newman-reporter-htmlextra
   ```

2. Execute a coleção gerando o relatório HTML:
   ```bash
   newman run "Postman Library API v2.postman_collection.json" -r htmlextra
   ```

> 📁 O arquivo HTML interativo será salvo automaticamente dentro do diretório `./newman` no seu repositório.

---

## 💡 Exemplos de Scripts Utilizados

Neste projeto utilizei scripts em JavaScript nas abas **Pre-request** e **Tests** para automatizar fluxos:

```javascript
// Exemplo 1: Salvar dinamicamente o ID do livro criado para uso posterior
const id = pm.response.json().id;
pm.collectionVariables.set("id", id);
```

```javascript
// Exemplo 2: Validação de código de status e chaves de resposta JSON
pm.test('Status code is 200', function () {
    pm.response.to.have.status(200);
});

pm.test('Stats include all fields', function () {
    var jsonData = pm.response.json().data;
    pm.expect(jsonData).to.have.all.keys('won', 'lost', 'drew');
});
```

---

## 🤝 Contribuições

Contribuições, sugestões de novos cenários de teste ou melhorias nos scripts são super bem-vindas!

1. Faça um **Fork** do projeto.
2. Crie uma branch para sua alteração: `git checkout -b feature/melhoria-script`.
3. Envie seus commits: `git commit -m 'feat: Adiciona validação de schema JSON'`.
4. Faça o push para a branch: `git push origin feature/melhoria-script`.
5. Abra um **Pull Request**.

---

## 📜 Licença

Este projeto está sob a licença [MIT](LICENSE). Sinta-se à vontade para utilizar os exemplos e coleções para estudos ou em seus próprios projetos.

---

## ✉️ Contato

Desenvolvido por **Francisco Gorgonho** — QA Analyst.

- **LinkedIn:** [linkedin.com/in/franciscogorgonho](https://linkedin.com/in/franciscogorgonho)
- **GitHub:** [@francisco-gorgonho](https://github.com/francisco-gorgonho)
- **E-mail:** francisco.gorgonho@gmail.com
- **Certificação:** Postman Student Expert (Concluído em Abril/2023)
