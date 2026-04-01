# Blog Post API

<div align="center">

![.NET Core](https://img.shields.io/badge/.NET%20Core-3.1-512BD4?logo=dotnet)
![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?logo=mysql&logoColor=white)
![C#](https://img.shields.io/badge/C%23-9.0-239120?logo=csharp)
![License](https://img.shields.io/badge/license-MIT-green)

**API RESTful para gerenciamento de posts de blog desenvolvida com ASP.NET Core**

</div>

---

## 📋 Índice

- [Sobre o Projeto](#-sobre-o-projeto)
- [Funcionalidades](#-funcionalidades)
- [Arquitetura](#%EF%B8%8F-arquitetura)
- [Tecnologias Utilizadas](#%EF%B8%8F-tecnologias-utilizadas)
- [Pré-requisitos](#-pré-requisitos)
- [Instalação](#-instalação)
- [Configuração](#%EF%B8%8F-configuração)
- [Executando o Projeto](#-executando-o-projeto)
- [Endpoints da API](#-endpoints-da-api)
- [Estrutura do Projeto](#-estrutura-do-projeto)
- [Modelo de Dados](#-modelo-de-dados)
- [Exemplos de Uso](#-exemplos-de-uso)
- [Contribuindo](#-contribuindo)
- [Licença](#-licença)

---

## 📖 Sobre o Projeto

A **Blog Post API** é uma aplicação RESTful construída com **ASP.NET Core 3.1** que permite a criação, leitura, atualização e exclusão (CRUD) de posts de blog. O projeto foi desenvolvido utilizando o **Visual Studio Code** e utiliza **MySQL** como banco de dados para persistência das informações.

Esta API foi projetada para ser simples, eficiente e servir como base para aplicações de blog ou sistemas de gerenciamento de conteúdo (CMS).

### 🎯 Objetivos

- Fornecer uma API REST completa para gerenciamento de posts
- Demonstrar boas práticas de desenvolvimento com .NET Core
- Implementar operações assíncronas para melhor performance
- Utilizar ADO.NET com MySqlConnector para acesso direto ao banco de dados

---

## ✨ Funcionalidades

- ✅ **Listar posts** - Recupera os 10 posts mais recentes
- ✅ **Buscar post por ID** - Recupera um post específico pelo identificador
- ✅ **Criar novo post** - Adiciona um novo post ao blog
- ✅ **Atualizar post** - Modifica o título e conteúdo de um post existente
- ✅ **Deletar post** - Remove um post específico
- ✅ **Deletar todos os posts** - Remove todos os posts do banco de dados
- ✅ **Operações assíncronas** - Todas as operações utilizam async/await para melhor performance
- ✅ **Validação de existência** - Retorna 404 quando um post não é encontrado

---

## 🏗️ Arquitetura

O projeto segue uma arquitetura em camadas simplificada:

```
┌─────────────────────────────────────┐
│         Controllers                 │  ← Camada de Apresentação (API)
│      (BlogController)               │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│         Query Layer                 │  ← Camada de Consulta
│      (BlogPostQuery)                │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│         Model Layer                 │  ← Camada de Modelo
│       (BlogPost)                    │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│      Database Access                │  ← Camada de Acesso a Dados
│         (AppDb)                     │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│      MySQL Database                 │  ← Banco de Dados
└─────────────────────────────────────┘
```

---

## 🛠️ Tecnologias Utilizadas

### Framework e Linguagem
- **[.NET Core 3.1](https://dotnet.microsoft.com/)** - Framework de desenvolvimento multiplataforma
- **[C# 9.0](https://docs.microsoft.com/pt-br/dotnet/csharp/)** - Linguagem de programação orientada a objetos
- **[ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/)** - Framework para construção de APIs Web

### Banco de Dados
- **[MySQL](https://www.mysql.com/)** - Sistema de gerenciamento de banco de dados relacional
- **[MySqlConnector 0.69.2](https://mysqlconnector.net/)** - Driver ADO.NET para MySQL (alto desempenho)

### Ferramentas de Desenvolvimento
- **[Visual Studio Code](https://code.visualstudio.com/)** - Editor de código
- **[Git](https://git-scm.com/)** - Controle de versão

### Padrões e Práticas
- ✅ RESTful API design
- ✅ Dependency Injection
- ✅ Async/Await pattern
- ✅ Repository pattern (simplificado)
- ✅ ADO.NET com queries parametrizadas (proteção contra SQL Injection)

---

## 📋 Pré-requisitos

Antes de começar, certifique-se de ter instalado em sua máquina:

- **[.NET Core SDK 3.1+](https://dotnet.microsoft.com/download/dotnet/3.1)** - Para compilar e executar o projeto
- **[MySQL Server 5.7+](https://dev.mysql.com/downloads/mysql/)** - Banco de dados
- **[Visual Studio Code](https://code.visualstudio.com/)** (opcional) - Editor de código recomendado
- **[Postman](https://www.postman.com/)** ou **[Insomnia](https://insomnia.rest/)** (opcional) - Para testar os endpoints

### Verificar Instalações

```bash
# Verificar versão do .NET Core
dotnet --version

# Verificar MySQL
mysql --version
```

---

## 🚀 Instalação

### 1. Clone ou extraia o projeto

```bash
# Se estiver usando Git
git clone <url-do-repositorio>
cd blog-post-api-master

# Ou extraia o arquivo ZIP
unzip blog-post-api-master.zip
cd blog-post-api-master
```

### 2. Restaurar dependências

```bash
dotnet restore
```

### 3. Criar o banco de dados

Conecte-se ao MySQL e execute os comandos SQL:

```sql
-- Criar o banco de dados
CREATE DATABASE blog CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

-- Usar o banco de dados
USE blog;

-- Criar a tabela BlogPost
CREATE TABLE BlogPost (
    Id INT AUTO_INCREMENT PRIMARY KEY,
    Title VARCHAR(255) NOT NULL,
    Content TEXT NOT NULL,
    CreatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UpdatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

-- Inserir dados de exemplo (opcional)
INSERT INTO BlogPost (Title, Content) VALUES
('Primeiro Post', 'Este é o conteúdo do primeiro post do blog.'),
('Introdução ao ASP.NET Core', 'ASP.NET Core é um framework moderno e multiplataforma...'),
('Trabalhando com MySQL', 'MySQL é um dos bancos de dados mais populares do mundo...');
```

---

## ⚙️ Configuração

### Configurar String de Conexão

Edite o arquivo `appsettings.json` e ajuste a string de conexão conforme seu ambiente:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "server=localhost;user id=root;password=SUA_SENHA;port=3306;database=blog;"
  }
}
```

**Parâmetros da conexão:**
- `server`: Endereço do servidor MySQL (padrão: localhost)
- `user id`: Usuário do banco de dados
- `password`: Senha do usuário
- `port`: Porta do MySQL (padrão: 3306)
- `database`: Nome do banco de dados (blog)

### Configuração de Ambiente de Desenvolvimento

Para ambiente de desenvolvimento, você pode usar o arquivo `appsettings.Development.json` que sobrescreve as configurações do `appsettings.json`.

---

## 🏃 Executando o Projeto

### Modo de Desenvolvimento

```bash
# Executar a aplicação
dotnet run

# Ou com watch (recompila automaticamente ao detectar mudanças)
dotnet watch run
```

### Compilar para Produção

```bash
# Compilar o projeto
dotnet build --configuration Release

# Publicar a aplicação
dotnet publish --configuration Release --output ./publish
```

### Executar Testes

```bash
dotnet test
```

### Acessar a API

Após iniciar a aplicação, a API estará disponível em:

- **HTTP:** `http://localhost:5000`
- **HTTPS:** `https://localhost:5001`

---

## 🔗 Endpoints da API

### Base URL
```
http://localhost:5000/api/blog
```

### Endpoints Disponíveis

| Método | Endpoint | Descrição | Status Code |
|--------|----------|-----------|-------------|
| `GET` | `/api/blog` | Lista os 10 posts mais recentes | 200 OK |
| `GET` | `/api/blog/{id}` | Busca um post específico por ID | 200 OK / 404 Not Found |
| `POST` | `/api/blog` | Cria um novo post | 200 OK |
| `PUT` | `/api/blog/{id}` | Atualiza um post existente | 200 OK / 404 Not Found |
| `DELETE` | `/api/blog/{id}` | Deleta um post específico | 200 OK / 404 Not Found |
| `DELETE` | `/api/blog` | Deleta todos os posts | 200 OK |

---

## 📁 Estrutura do Projeto

```
blog-post-api-master/
│
├── Controllers/
│   ├── BlogController.cs          # Controller principal com endpoints CRUD
│   └── WeatherForecastController.cs # Controller de exemplo (padrão .NET)
│
├── Model/
│   ├── BlogPost.cs                # Entidade BlogPost com operações CRUD
│   └── BlogPostQuery.cs           # Queries de consulta ao banco
│
├── Properties/
│   └── launchSettings.json        # Configurações de execução
│
├── .vscode/
│   └── [arquivos de configuração do VS Code]
│
├── AppDb.cs                       # Classe de conexão com banco de dados
├── Program.cs                     # Ponto de entrada da aplicação
├── Startup.cs                     # Configuração de serviços e middleware
├── BlogPostApi.csproj             # Arquivo de projeto .NET
├── appsettings.json               # Configurações da aplicação
├── appsettings.Development.json   # Configurações de desenvolvimento
├── .gitignore                     # Arquivos ignorados pelo Git
└── README.md                      # Documentação original
```

### Descrição dos Principais Arquivos

#### `Program.cs`
Ponto de entrada da aplicação. Configura e inicializa o host web.

#### `Startup.cs`
Configura os serviços da aplicação (Dependency Injection) e o pipeline de requisições HTTP.

#### `AppDb.cs`
Gerencia a conexão com o banco de dados MySQL usando o padrão Disposable.

#### `BlogController.cs`
Controller REST que expõe os endpoints da API e gerencia as requisições HTTP.

#### `BlogPost.cs`
Modelo de domínio que representa um post do blog. Contém métodos para Insert, Update e Delete.

#### `BlogPostQuery.cs`
Classe responsável pelas consultas (SELECT) ao banco de dados.

---

## 💾 Modelo de Dados

### Entidade: BlogPost

| Campo | Tipo | Descrição | Restrições |
|-------|------|-----------|------------|
| `Id` | `INT` | Identificador único do post | Primary Key, Auto Increment |
| `Title` | `VARCHAR(255)` | Título do post | NOT NULL |
| `Content` | `TEXT` | Conteúdo do post | NOT NULL |
| `CreatedAt` | `TIMESTAMP` | Data de criação | DEFAULT CURRENT_TIMESTAMP |
| `UpdatedAt` | `TIMESTAMP` | Data de atualização | ON UPDATE CURRENT_TIMESTAMP |

### Modelo C#

```csharp
public class BlogPost
{
    public int Id { get; set; }
    public string Title { get; set; }
    public string Content { get; set; }
}
```

---

## 📝 Exemplos de Uso

### 1. Listar Posts Recentes

**Requisição:**
```http
GET /api/blog HTTP/1.1
Host: localhost:5000
```

**Resposta:**
```json
[
  {
    "id": 3,
    "title": "Trabalhando com MySQL",
    "content": "MySQL é um dos bancos de dados mais populares do mundo..."
  },
  {
    "id": 2,
    "title": "Introdução ao ASP.NET Core",
    "content": "ASP.NET Core é um framework moderno e multiplataforma..."
  },
  {
    "id": 1,
    "title": "Primeiro Post",
    "content": "Este é o conteúdo do primeiro post do blog."
  }
]
```

### 2. Buscar Post por ID

**Requisição:**
```http
GET /api/blog/1 HTTP/1.1
Host: localhost:5000
```

**Resposta:**
```json
{
  "id": 1,
  "title": "Primeiro Post",
  "content": "Este é o conteúdo do primeiro post do blog."
}
```

### 3. Criar Novo Post

**Requisição:**
```http
POST /api/blog HTTP/1.1
Host: localhost:5000
Content-Type: application/json

{
  "title": "Meu Novo Post",
  "content": "Este é o conteúdo do meu novo post sobre tecnologia."
}
```

**Resposta:**
```json
{
  "id": 4,
  "title": "Meu Novo Post",
  "content": "Este é o conteúdo do meu novo post sobre tecnologia."
}
```

### 4. Atualizar Post

**Requisição:**
```http
PUT /api/blog/4 HTTP/1.1
Host: localhost:5000
Content-Type: application/json

{
  "title": "Meu Post Atualizado",
  "content": "Conteúdo atualizado com novas informações."
}
```

**Resposta:**
```json
{
  "id": 4,
  "title": "Meu Post Atualizado",
  "content": "Conteúdo atualizado com novas informações."
}
```

### 5. Deletar Post

**Requisição:**
```http
DELETE /api/blog/4 HTTP/1.1
Host: localhost:5000
```

**Resposta:**
```http
200 OK
```

### 6. Deletar Todos os Posts

**Requisição:**
```http
DELETE /api/blog HTTP/1.1
Host: localhost:5000
```

**Resposta:**
```http
200 OK
```

---

## 🔧 Exemplos com cURL

### Listar todos os posts
```bash
curl -X GET http://localhost:5000/api/blog
```

### Buscar post por ID
```bash
curl -X GET http://localhost:5000/api/blog/1
```

### Criar novo post
```bash
curl -X POST http://localhost:5000/api/blog \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Novo Post via cURL",
    "content": "Conteúdo do post criado via linha de comando"
  }'
```

### Atualizar post
```bash
curl -X PUT http://localhost:5000/api/blog/1 \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Post Atualizado",
    "content": "Novo conteúdo atualizado"
  }'
```

### Deletar post
```bash
curl -X DELETE http://localhost:5000/api/blog/1
```

### Deletar todos os posts
```bash
curl -X DELETE http://localhost:5000/api/blog
```

---

## 🔍 Detalhes Técnicos

### Injeção de Dependência

A aplicação utiliza o sistema de Dependency Injection nativo do ASP.NET Core:

```csharp
services.AddTransient<AppDb>(_ => 
    new AppDb(Configuration["ConnectionStrings:DefaultConnection"]));
```

A classe `AppDb` é registrada como **Transient**, criando uma nova instância a cada requisição.

### Operações Assíncronas

Todas as operações de banco de dados são assíncronas para melhor performance:

```csharp
public async Task<IActionResult> GetLatest()
{
    await Db.Connection.OpenAsync();
    var query = new BlogPostQuery(Db);
    var result = await query.LatestPostsAsync();
    return new OkObjectResult(result);
}
```

### Segurança

- ✅ **Queries Parametrizadas** - Proteção contra SQL Injection
- ✅ **HTTPS Redirection** - Redirecionamento automático para HTTPS
- ✅ **CORS** - Configurável para ambientes específicos

### Performance

- ⚡ Uso de ADO.NET direto (sem ORM) para máxima performance
- ⚡ Operações assíncronas para melhor escalabilidade
- ⚡ Connection pooling automático do MySqlConnector

---

## 🐛 Solução de Problemas

### Erro de Conexão com MySQL

**Problema:** `Unable to connect to any of the specified MySQL hosts`

**Solução:**
1. Verifique se o MySQL está em execução
2. Confirme as credenciais no `appsettings.json`
3. Verifique se a porta 3306 está acessível

### Erro de Certificado SSL

**Problema:** `The certificate chain was issued by an authority that is not trusted`

**Solução:** Adicione `SslMode=None` na string de conexão (apenas em desenvolvimento):
```
server=localhost;user id=root;password=root;port=3306;database=blog;SslMode=None;
```

### Post não encontrado (404)

**Problema:** Sempre retorna 404 ao buscar posts

**Solução:**
1. Verifique se o banco de dados `blog` existe
2. Confirme se a tabela `BlogPost` foi criada
3. Verifique se existem dados na tabela

---

## 🧪 Testando a API

### Com Postman

1. Importe a collection (criar arquivo `BlogPostApi.postman_collection.json`)
2. Configure a variável de ambiente `base_url` como `http://localhost:5000`
3. Execute as requisições

### Com Swagger (Opcional)

Para adicionar Swagger ao projeto:

```bash
dotnet add package Swashbuckle.AspNetCore
```

Adicione no `Startup.cs`:

```csharp
// Em ConfigureServices
services.AddSwaggerGen();

// Em Configure
app.UseSwagger();
app.UseSwaggerUI(c => {
    c.SwaggerEndpoint("/swagger/v1/swagger.json", "Blog Post API V1");
});
```

Acesse: `http://localhost:5000/swagger`

---

## 📊 Melhorias Futuras

- [ ] Adicionar autenticação e autorização (JWT)
- [ ] Implementar paginação nos resultados
- [ ] Adicionar filtros e busca por título/conteúdo
- [ ] Implementar validação de dados com Data Annotations
- [ ] Adicionar logging estruturado (Serilog)
- [ ] Implementar cache (Redis)
- [ ] Adicionar testes unitários e de integração
- [ ] Migrar para Entity Framework Core
- [ ] Adicionar suporte a upload de imagens
- [ ] Implementar sistema de tags/categorias
- [ ] Adicionar versionamento de API
- [ ] Implementar rate limiting
- [ ] Adicionar documentação Swagger/OpenAPI
- [ ] Containerizar com Docker

---

## 🤝 Contribuindo

Contribuições são bem-vindas! Para contribuir:

1. Fork o projeto
2. Crie uma branch para sua feature (`git checkout -b feature/NovaFuncionalidade`)
3. Commit suas mudanças (`git commit -m 'Adiciona nova funcionalidade'`)
4. Push para a branch (`git push origin feature/NovaFuncionalidade`)
5. Abra um Pull Request

### Padrões de Código

- Siga as convenções de nomenclatura do C#
- Utilize async/await para operações I/O
- Comente código complexo quando necessário
- Mantenha os métodos pequenos e com responsabilidade única

---

## 📝 Notas Importantes

> ⚠️ **Atenção:** Este projeto não possui arquivo de solução (.sln), portanto não é possível carregá-lo diretamente no Visual Studio completo. Utilize o Visual Studio Code ou execute via linha de comando com `dotnet run`.

> 🔒 **Segurança:** Nunca commite arquivos `appsettings.json` com senhas reais em repositórios públicos. Utilize variáveis de ambiente ou Azure Key Vault em produção.

> 🗄️ **Banco de Dados:** Este projeto utiliza ADO.NET direto ao invés de um ORM como Entity Framework Core, o que proporciona maior controle e performance, mas requer maior atenção na escrita de queries SQL.

---

## 📄 Licença

Este projeto está sob a licença MIT. Consulte o arquivo `LICENSE` para mais detalhes.

---

## 👨‍💻 Autor

Desenvolvido como projeto de estudo de ASP.NET Core e APIs RESTful.

---

## 📚 Recursos Adicionais

### Documentação Oficial

- [ASP.NET Core Documentation](https://docs.microsoft.com/pt-br/aspnet/core/)
- [MySQL Documentation](https://dev.mysql.com/doc/)
- [MySqlConnector Documentation](https://mysqlconnector.net/)

### Tutoriais Recomendados

- [Building REST APIs with ASP.NET Core](https://docs.microsoft.com/pt-br/aspnet/core/tutorials/first-web-api)
- [Working with MySQL in .NET](https://mysqlconnector.net/tutorials/connect-to-mysql/)
- [Async/Await Best Practices](https://docs.microsoft.com/pt-br/archive/msdn-magazine/2013/march/async-await-best-practices-in-asynchronous-programming)

---

## 🙏 Agradecimentos

- Microsoft pela excelente documentação do ASP.NET Core
- Comunidade .NET por tutoriais e suporte
- Desenvolvedores do MySqlConnector pelo driver de alta performance

---

<div align="center">

**Feito com ❤️ e ASP.NET Core**

⭐ Se este projeto foi útil, considere dar uma estrela!

</div>
