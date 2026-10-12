# Tarefas

| ID | Tarefa | Origem | Depende de | Concluída quando |
| :--- | :--- | :--- | :--- | :--- |
| T-01 | Criar projeto, estrutura de pastas e instalar pacotes (EF Core, xUnit) | Constituição | - | Projeto compila e pastas (Services, Context, Entities) existem |
| T-02 | Criar entidade `Password`, o `AppDbContext` (SQLite) e gerar a primeira migração | Plano (Modelo de Dados) | T-01 | A migração roda e o banco de dados é gerado com sucesso |
| T-03 | Criar a lógica de geração de senhas (`PasswordGenerator`) | Spec (RN01, RN02, RN03, RN04) | T-01 | Testes unitários comprovam que a senha tem 16+ chars, números, letras, caracteres especiais e zero espaços |
| T-04 | Criar o serviço de aplicação (`PasswordService`) para orquestrar a geração e salvamento no banco | Plano (Arquitetura) | T-02, T-03 | Teste comprova que a senha é gerada e inserida no `AppDbContext` |
| T-05 | Implementar endpoint de geração de senha (`POST /api/passwords`) | Spec (RF01), Plano (Contratos) | T-04 | Teste de integração (Caminho feliz) bate na rota e retorna HTTP 201 com o JSON esperado |
| T-06 | Implementar método no serviço para buscar senha pelo GUID | Spec (RF02), Plano (Arquitetura) | T-02 | Teste unitário busca senha salva no banco via Contexto |
| T-07 | Implementar endpoint de consulta (`GET /api/passwords/{id}`) e validações | Spec (RF02, CB01, CB02) | T-06 | Teste de integração retorna 200 (sucesso), 404 (Não Encontrado) e 400 (ProblemDetails para GUID inválido) |