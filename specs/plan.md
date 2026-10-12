# Plano técnico

## Contexto
Construiremos uma API utilizando as tecnologias definidas na Constituição (ASP.NET Core Minimal API, .NET 10, C#). A API tem um escopo direto e enxuto focado em dois endpoints: um para geração e persistência de senhas fortes, e outro para consulta dessas senhas baseada em um identificador único (GUID).

## Arquitetura
A aplicação seguirá uma separação lógica simples dentro de um único projeto Web:
- **Program.cs (Endpoints):** Ponto de entrada da Minimal API. Fará apenas o roteamento HTTP, injeção de dependência e delegação de chamadas. Não conterá regras de negócio nem acesso a dados.
- **Pasta `Services`:** Conterá as classes de serviço (ex: `PasswordService`). Aqui viverá toda a lógica de negócio (geração da senha, validação das regras) e a orquestração do banco de dados.
- **Pasta `Context`:** Conterá o `AppDbContext` do Entity Framework Core para o SQLite.
- **Pasta `Entities`:** Conterá os modelos de domínio e eventuais DTOs (Data Transfer Objects).

## Decisões
- **D-01: Uso de Minimal API em vez de Controllers.**
  *Justificativa:* O projeto possui apenas 2 endpoints. Minimal APIs reduzem a complexidade e melhoram a performance de inicialização para escopos pequenos.
- **D-02: Uso de SQLite.**
  *Justificativa:* É um projeto para aprender o SDD. O SQLite não exige a instalação de servidores de banco de dados, facilitando a execução imediata.
- **D-03: Delegação de lógica para a camada de Service.**
  *Justificativa:* Atende à restrição da Constituição, permitindo que a regra de geração de senhas seja testada via Testes Unitários (xUnit) de forma isolada, sem depender do contexto HTTP.

## Modelo de dados
O banco de dados SQLite conterá apenas uma tabela principal gerada pelo EF Core:

**Tabela: `Passwords`**
- `Id` (GUID) - Chave Primária (Primary Key).
- `Value` (String) - Obrigatório (Required). Armazenará a senha gerada (mínimo de 16 caracteres).
- `CreatedAt` (DateTime) - Obrigatório. Data e hora em que a senha foi gerada.

## Contratos
A API terá as seguintes rotas HTTP:

### 1. Gerar Senha
- **Rota:** `POST /api/passwords`
- **Request:** (Vazio)
- **Response (201 Created):**
  ```json
  {
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "value": "aB3!dE8@fG1#hI4$"
  }

### 2. Consultar Senha
- **Rota:** `GET /api/passwords/{id}`
- **Request:** Parâmetro id na URL (GUID)
- **Response (200 Ok):**
  ```json
  {
    "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "value": "aB3!dE8@fG1#hI4$"
  }
- **Response - Erro (404 Not Found):** Retornado caso o GUID não exista.
- **Response - Erro (400 Bad Request):** Retornado no formato ProblemDetails caso o GUID seja inválido.

## Riscos
- Segurança de Dados: As senhas estão sendo armazenadas em texto puro (plain text) no banco de dados. Como o escopo é exclusivamente para entender SDD e aprender, será aceito esse risco.

- Geração Aleatória (Random): A geração de senhas pode falhar não incluindo todos os tipos de caracteres esperados. Para evitar isso, serão feitos testes unitários.