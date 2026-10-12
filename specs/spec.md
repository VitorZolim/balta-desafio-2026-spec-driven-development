# Gerador de Senhas Fortes

## Problema
Desenvolvedores e sistemas precisam gerar senhas que sejam criptograficamente fortes e seguras, e precisam de uma forma simples de armazenar e recuperar essas senhas sem lidar diretamente com a lógica de geração.

## Objetivo
Uma API simples, capaz de gerar senhas de alta complexidade de forma automatizada, armazená-las e permitir sua consulta posterior através de um identificador único.

## Usuários
- Aplicações Front-End que precisam de um gerador de senhas para seus usuários.
- Desenvolvedores que consumirão a API localmente para testes.

## Histórias
- Como sistema cliente, eu quero solicitar a geração de uma senha forte para que meu usuário tenha uma credencial segura, recebendo um identificador (GUID) em troca.
- Como sistema cliente, eu quero consultar uma senha previamente gerada enviando o seu identificador (GUID) para recuperar o acesso àquela senha.

## Requisitos funcionais
- **RF01:** O sistema deve gerar uma senha aleatória, armazená-la e retornar um identificador único (GUID).
- **RF02:** O sistema deve receber um identificador (GUID) e retornar a senha correspondente armazenada.

## Regras de negócio
- **RN01:** As senhas geradas devem conter no mínimo 16 caracteres.
- **RN02:** As senhas geradas devem incluir, obrigatoriamente, caracteres especiais.
- **RN03:** As senhas geradas não podem conter espaços em branco.
- **RN04:** As senhas geradas devem incluir pelo menos uma letra maiúscula, uma minúscula e um número.
- **RN05:** Não há necessidade de encriptar senha ou outros recursos de segurança no momento.

## Casos de borda
- **CB01 - GUID Inexistente:** Se uma consulta for feita com um GUID que não consta no banco de dados, o sistema deve retornar um erro claro de "Não Encontrado" (404).
- **CB02 - GUID Inválido:** Se o usuário enviar um texto que não seja um GUID válido na consulta, o sistema deve rejeitar a requisição com erro de validação (400).

## Fora de escopo
- Não teremos interface gráfica (front-end).
- Não teremos login/autenticação/JWT.
- Não haverá funcionalidade para deletar ou atualizar senhas.
- Este projeto não será preparado para publicação em ambiente de produção (foco educacional).

## Critérios de aceite
- É possível chamar o endpoint de geração e receber um GUID válido em retorno.
- Toda senha gerada respeita rigorosamente as regras (16+ chars, sem espaços, com caracteres especiais, letras e números).
- É possível chamar o endpoint de consulta passando o GUID recebido e obter exatamente a senha que foi gerada.