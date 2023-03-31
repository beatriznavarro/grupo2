## Estratégias de teste

Segundo o [ChatGPT](https://chat.openai.com/) estratégias de testes são:

![Estratégias de testes](/images/testes/chatGPT-testing-estrategies.PNG)


No iFood entendemos que, não somente essas , mas as principais estratégias a serem utilizadas são:

- Testes de caixa preta: para garantir que as funcionalidades do nosso software estão de acordo com o esperado pelos interessados aplicamos as técnicas de testes de caixa preta onde a pessoa testadora não tem acesso ao código do sistema.

Aqui usamos automação de testes nos cenários mais relevantes e assim é possível facilitar a execução destes cenários através de uma pipeline, possibilitando que não só os responsáveis pela automação executem os testes periodicamente, mas qualquer pessoa com acesso a pipeline.

Aqui também usamos o conhecimento do negócio dos nossos tester manuais para executar os cenários de forma exploratória.

Possuímos testes do frontend da aplicação (Testes de UI) e no backend (Testes de API).


- Testes de integração: Um sitema de pedidos online possui algumas integrações essenciais sem as quais não é possível funcionar, que são: Meio de pagamentos e  Tecnologias de localização; e algumas outras integrações que melhoram a experiência do usuário, como: tecnologias de recomendação, chatbots, etc.

Desta forma a realização de testes de integração é essencial, tanto entre componentes menores (Sandwich testing) quanto considerando o sistema como um todo (Big bang   testing).


- Testes de performance: Conhecendo nossos horários de pico conseguimos desenhar uma estratégia de testes de performance para garantir que em momentos de alta demanda nosso serviço funcionará adequadamente.

Alguns tipos de testes que realizamos são:

Teste de estresse;
Teste de volume;
Teste de escalabilidade.


- Teste de segurança: Como nossa principal integração é realizada com meios de pagamentos precisamos garantir que os dados de pagamentos dos nossos clientes sejam tratados de forma segura. Para isso realizamos testes de segurança a fim de evitar qualquer possível vulnerabilidade.


Vale relembrar que já utilizamos o TDD como metodologia de desenvolvimento 😍
