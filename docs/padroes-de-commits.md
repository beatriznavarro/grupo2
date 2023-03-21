## Padrões de commit

Optamos por escolher o [convetionalcommits](https://www.conventionalcommits.org/pt-br/v1.0.0/) como especificação e padronização para realização dos commits.

A mensagem do commit deve ser estruturada da seguinte forma:

![Mensagem do commit](/images/commit/commit-estrutura.PNG)

### Tipos 

- fix: alguma correção realizada no código
- feat: uma nova funcionalidade adicionada ao código

#### Tipos adicionais (baseado na Convenção do Angular)

- build:, chore:, ci:, docs:, style:, refactor:, perf:, test:

### Escopo

Um escopo pode ser fornecido ao tipo do commit, para fornecer informações contextuais adicionais

Ex.: feat(parser): adiciona capacidade de interpretar arrays.

### Rodapé

- BREAKING CHANGE: um commit que contém no rodapé opcional o texto BREAKING CHANGE:, ou contém o símbolo ! depois do tipo/escopo, insere uma modificação que quebra a compatibilidade da API. Pode ser usado com qualquer tipo de commit.

### Benefícios ao utilizar um padrão

- Facilidade ao criar automações para geração de CHANGELOGs
- Facilidade para entender as mudanças realizadas