# Trabalhe na Codevance

A [Codevance](https://codevance.com.br) é uma software house que tem como missão otimizar os resultados e gerar valor ao seu negócio utilizando tecnologia como meio.

Somos especialistas em Python, nosso time atua todo de forma remota e nossos clientes possuem grandes desafios tecnológicos.

Se você:

- Tem sangue no olho e é, ou busca ser, um ótimo programador;
- Tem interesse em crescer profissionalmente;
- É organizado, tem disciplina e autonomia para trabalhar do conforto da sua casa;
- Gosta da linguagem Python ou já utilizou em algum projeto profissional;

Eu te convido a clonar esse repositório, meter a mão na massa e mostrar pra gente as suas qualidades.

Temos vagas para todos os perfis. Não é preciso ter experiência e não fazemos nenhum tipo de distinção.

## Como participar

1. Clone este repositório
1. Siga as instruções abaixo
1. Suba o projeto em algum lugar (heroku, de preferência)
1. Envie um e-mail para ronaldo *dot* oliveira *at* codevance *dot* com *dot* br

## Especificações

Você vai desenvolver um sistema de antecipação de pagamentos.

Imagine que haja uma série de pagamentos a serem feitos por uma empresa no decorrer dos próximos meses, mas a empresa quer fazer um plano com seus fornecedores para fazer estes pagamentos de forma adiantada, concedendo um desconto relacionado a quantidade de dias de diferença entre a data de vencimento original do pagamento e a nova data de pagamento.

O objetivo é fornecer melhor fluxo de caixa ao fornecedor e rentabilizar o caixa da empresa através dos descontos.

Para descobrir o novo valor a ser pago nesta antecipação, o cálculo a ser feito é:

```
NOVO_VALOR = VALOR_ORIGINAL - (VALOR_ORIGINAL * ((3% / 30) * DIFERENCA_DE_DIAS))
```

Vamos a um exemplo prático:

```
DATA DE VENCIMENTO ORIGINAL = 01/10/2019
VALOR ORIGINAL = R$ 1.000,00
NOVA DATA DE VENCIMENTO = 15/09/2019

NOVO VALOR = 1000 - (1000 * ((3% / 30) * 16))
NOVO VALOR = 1000 - (1000 * 0,016)
NOVO VALOR = 1000 - 16

NOVO VALOR = R$ 984,00
```

### Características

- O sistema deve armazenar os pagamentos e suas informações básicas
  - id do pagamento, data de emissão, data de vencimento, valor original, a qual fornecedor pertence, dados cadastrais básicos deste fornecedor, como razão social e CNPJ.
- Para um pagamento ser adiantado, o fornecedor deve fazer uma solicitação, então o operador da empresa escolhe se libera a antecipação ou nega a antecipação. Toda essa movimentação deve ficar armazenada em um log.
  - Essa solicitação pode vir via sistema ou por outras vias. Quando vier por outras vias, o operador da empresa fará a solicitação no sistema.
- O fornecedor deve ter acesso a uma área, através de autenticação via email e senha, onde ele possa solicitar a antecipação de um pagamento. É necessário também que ele veja todos os pagamentos disponíveis para antecipação, todos os pagamentos aguardando liberação, todos os aprovados e todos os negados.
  - Importantíssimo que um fornecedor não veja os pagamentos de outro
- Para cada ação sobre um pagamento (solicitação, liberação, negação) o sistema deve enviar um email ao fornecedor.
  - Este envio de email deve ser feito de forma assíncrona (`celery` é seu amigo)
- Caso um pagamento chegue até sua data de vencimento sem ser antecipado, o mesmo deve ser indisponibilizado para operação, mas mantido no histórico.
  - Fornecedores não podem ver pagamentos indisponibilizados disponíveis para antecipação
- Deve haver uma API Rest básica com dois endpoints:
  - Um endpoint que liste as operações de um fornecedor, que estará autenticado via JWT. Este endpoint deve permitir filtro por estado do pagamento (indisponível, disponível, aguardando confirmação, antecipado, negado)
  - Outro endpoint que será responsável pela solicitação de antecipação de um pagamento. Este endpoint deve receber o identificador do pagamento e, obviamente, um usuário logado só pode solicitar antecipação dos pagamentos associados ao seu usuário.

## Requisitos técnicos

- Utilize Python 3.7 (ou mais recente) como linguagem e PostgreSQL como banco de dados;
- Utilize um framework (dica: com django é mais fácil);
- O código deve estar em inglês (commits podem estar em pt-br);
- O sistema deve estar online, rodando, em algum lugar (dica: com heroku é mais fácil);
- O sistema deve ter testes automatizados (dica: com pytest é mais fácil);
- O repositório deve conter documentação sobre como fazer deployment e como testar;
- Deve conter uma documentação da API;

## Recomendações e dicas

- Caso for utilizar Django, temos [nosso cookiecutter](https://github.com/codevance/cookiecutter-django) que pode servir de ponto de partida (mas não é obrigatório);
- Use boas práticas de programação;
- Modele os dados com cuidado;
- Se preocupe com arquitetura e qualidade de código, não se preocupe com estética (dica: bootstrap é seu amigo).

**Divirta-se!**
