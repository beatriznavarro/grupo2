## CI/CD Pipeline

Segundo o [ChatGPT](https://chat.openai.com/) CI/CD é:

![CI/CD Pipeline](/images/ci-cd/chatGPT-ci-cd.PNG)


Um pipeline CI/CD é uma série de etapas automatizadas que permitem a construção, teste e implantação de software de forma contínua e consistente. É uma implementação prática do processo de CI/CD.

O pipeline é composto por várias etapas que automatizam todo o processo de entrega de software, desde a integração do código até a implantação em um ambiente de produção. Essas etapas incluem, por exemplo, a construção do código fonte, testes automatizados, verificação de qualidade de código, criação de artefatos, implantação em ambiente de homologação e, por fim, a implantação em produção.

Cada etapa do pipeline é configurada para executar automaticamente após a conclusão da etapa anterior, permitindo que a equipe de desenvolvimento automatize todo o processo de entrega de software. Além disso, o pipeline pode ser configurado para notificar automaticamente os desenvolvedores em caso de falhas ou erros, permitindo que a equipe de desenvolvimento possa corrigi-los rapidamente.

O pipeline CI/CD pode ser implementado em ferramentas específicas ou construído utilizando uma plataforma de automação de processos, como o Jenkins, Travis CI, GitLab CI/CD, CircleCI, entre outras. Essas ferramentas fornecem a infraestrutura necessária para implementar o pipeline e também oferecem recursos adicionais, como integração com ferramentas de monitoramento, gerenciamento de configuração, e outras.

Em resumo, um pipeline CI/CD automatiza todo o processo de entrega de software, permitindo que as equipes de desenvolvimento possam entregar software de forma mais rápida e eficiente, com maior qualidade e confiabilidade.

Aqui está um exemplo de um pipeline CI/CD:

```yaml

name: Pipeline CI/CD

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v2
    - name: Setup Node.js
      uses: actions/setup-node@v2
      with:
        node-version: '14'
    - name: Install dependencies
      run: npm install
    - name: Lint code
      run: npm run lint
    - name: Build app
      run: npm run build
    - name: Run tests
      run: npm test
      
  deploy:
    needs: build
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main' && github.event_name == 'push'
    
    steps:
    - name: Setup SSH keys
      run: |
        echo "${{ secrets.SSH_PRIVATE_KEY }}" > ~/.ssh/id_rsa
        chmod 600 ~/.ssh/id_rsa
        ssh-keyscan github.com >> ~/.ssh/known_hosts
    - name: Deploy to production
      run: ssh -o StrictHostKeyChecking=no user@hostname "cd /var/www/ifood && git pull && npm install && pm2 restart ifood"
```

Este pipeline possui duas tarefas (jobs): "build" e "deploy". A primeira tarefa executa a compilação, teste e verificação de qualidade do código, enquanto a segunda tarefa faz o deploy do código para o ambiente de produção.

Na primeira tarefa "build", as etapas realizadas são:

    "Checkout" do código fonte: Faz o download do código fonte do repositório Github.
    "Setup Node.js": Configura o ambiente para a versão do Node.js especificada.
    "Install dependencies": Instala as dependências necessárias do projeto.
    "Lint code": Realiza a verificação de qualidade do código, utilizando uma ferramenta de análise estática de código.
    "Build app": Compila o código e cria os artefatos necessários para a implantação.
    "Run tests": Executa os testes automatizados, garantindo que o código esteja funcionando corretamente.

A segunda tarefa "deploy", por sua vez, executa as seguintes etapas:

    "Setup SSH keys": Configura as chaves SSH para autenticação no servidor de produção, que permite a conexão segura e a realização do deploy.
    "Deploy to production": Executa o comando SSH para acessar o servidor de produção, entrar no diretório de destino do projeto, fazer o pull do código atualizado do repositório Github, instalar as dependências necessárias e reiniciar o aplicativo Node.js (no caso deste exemplo, usando o gerenciador de processos PM2).

Por fim, o pipeline CI/CD é acionado sempre que houver um push ou pull request na branch "main" do repositório Github. A tarefa "deploy" é executada somente em caso de push na branch "main". Além disso, a etapa "Setup SSH keys" utiliza variáveis de ambiente secretas (secrets) para armazenar a chave privada SSH, garantindo que informações sensíveis sejam protegidas.