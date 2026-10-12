# Constituição do projeto

## Stack
- .NET 10, C#
- Minimal API
- Persistência em SQLite com Entity Framework Core
- Testes automatizados com xUnit

## Arquitetura
- O endpoint não deve acessar o banco de dados diretamente; o acesso deve ser feito sempre via serviço de aplicação.
- As regras de negócio não devem ficar nos endpoints nem nos handlers HTTP.
- Nenhuma dependência nova deve ser adicionada sem uma justificativa prévia escrita no plano.

## Qualidade
- Toda regra de negócio precisa de cobertura com testes unitários.
- Todo endpoint precisa de pelo menos um teste de integração focado no caminho feliz.
- Erros de validação devem retornar obrigatoriamente HTTP 400 no formato `ProblemDetails`.

## Convenções
Padrão C# .NET estabelecido para o projeto:

| Elemento do Código | Padrão Utilizado | Exemplo Prático |
| :--- | :--- | :--- |
| Classes, Structs, Records | PascalCase | `public class ProcessadorPagamento` |
| Interfaces | PascalCase (prefixo I) | `public interface IRepositorio` |
| Métodos e Propriedades | PascalCase | `public void CalcularTotal()` / `public int Id { get; }` |
| Variáveis Locais e Argumentos | camelCase | `int quantidadeItens`, `double precoUnitario` |
| Campos Privados (private) | camelCase (prefixo _) | `private string _nomeUsuario;` |
| Tipos Primitivos | Minúsculas (aliases do C#) | `int`, `string`, `bool` (evitar Int32, String, Boolean) |
| Uso do var | Apenas quando o tipo for óbvio | `var lista = new List<string>();` |
| Chaves ({ }) | Estilo Allman (nova linha) | `if (valido) { \n // código \n }` |

## Governança
- A aplicação é considerada concluída quando compilar sem erros ou warnings, todos os testes passarem e executar sem erros.
- A inteligência artificial deve executar apenas uma tarefa (do tasks.md) por vez.
- Não devem ser realizadas alterações em arquivos ou escopos que não estejam explícitos na tarefa atual.