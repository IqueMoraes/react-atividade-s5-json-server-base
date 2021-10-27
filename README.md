1- json-server-base a API.

Essa API é proposta para aplicações de compartilhamento de informações. As informações produzidas e repassadas poderão ser compartilhadas de forma pública ou restrita aos usuários cadastrados. Uma ferramenta de compartilhamento de ideia e propostas.

2- Endpoints

Esta API cont a com 6 Endpoints.
USUÁRIO:
-Cadastro
-Login

ESPAÇO ABERTO:
-Envio de opiniões
-Acesso às opiniões

ESPAÇO RESTRITO:
-Envio de opiniões
-Acesso às opiniões




a) Cadastro

O endpoint de cadastro fica acessível com:
POST /signup

Onde no corpo do cadastro devem conter as informações de nome do usuário, função, email e senha.
O nome do usuário pode ser escrito com letras maíusculas e minúsculas, números e espaços.
A função deve ser escrita apenas em letras.
O email deve ter formatação própria de e-mail.
A senha podem conter números e letras.

Exemplo:
            { "name": "Machado de Assis",
            "role": "Presidente da Academia Brasileira de Letras",
            "email": "machado.da@abl.com.br",
            "senha": "benculpado",
            }

e deve retornar:

            {
            "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im1hY2hhZG8uZGFAYWJsLmNvbS5iciIsImlhdCI6MTYzNTI2MDMyMiwiZXhwIjoxNjM1MjYzOTIyLCJzdWIiOiIzIn0.B6byz7WgpWmEfi6ZCsCixmKDkKyhjkwb9mARNClrWz4",
            "user": {
                "email": "machado.da@abl.com.br",
                "name": "Machado de Assis",
                "role": "Presidente da Academia Brasileira de Letras",
                "id": 3
            }
            }




b) Login

O endpoint de login fica acessível com:
POST /signin

Para o Login devem conter no corpo da requisição o e-mail e senha.

Exemplo:
            {
            "email": "machado.da@abl.com.br",
            "senha": "benculpado",
            }

Deve retornar:
            {
            "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im1hY2hhZG8uZGFAYWJsLmNvbS5iciIsImlhdCI6MTYzNTI2MDQ2NSwiZXhwIjoxNjM1MjY0MDY1LCJzdWIiOiIzIn0.7XlndFvlVKgjp5fJoObGKXZAqccouLRoeJggEKbPic4",
            "user": {
            "email": "machado.da@abl.com.br",
            "name": "Machado de Assis",
            "role": "Presidente da Academia Brasileira de Letras",
            "id": 3
            }
            }




c)Espaço aberto - envio

Área de opiniões assinadas e anônimas.
Usuários logados e não logados poderão enviar informações para esse endpoint.

Para requisição:
POST /plazza

No corpo da requisição deve conter a informação no campo "myopinion" e o campo "speaker" é opcional.

Exemplo:
            {
            "myopinion": "Viva o Império!",
            "speaker": ""
            }

Deve retornar a informação enviada com o número de id atribuído:

            {
            "myopinion": "Viva o Império!",
            "speaker": "",
            "id": 7
            }




d)Espaço aberto - acesso

Área de opiniões emitidas por usuários inscritos ou não.
Usuários logados e sem cadastro podem acessar as informações.

Para requisição:
GET /plazza

Não é necessário informação no corpo da requisição.

Deve retornar:
            [
            {
            "myopinion": "Viva a República!!",
            "speaker": "Lúcio Mendonça",
            "id": 6
            },
            {
            "myopinion": "Viva o Império!",
            "speaker": "Anônimo",
            "id": 7
            }
            ]




e)Espaço restrito - envio

Área de opiniões assinadas.
Usuários logados poderão enviar informações para esse endpoint.

Para requisição:
POST /congress

No header da requisição deve conter o token de acesso do usuário logado no portador

Bearer *acess token* 

e no corpo da requisição as informações no campo "myopinion" e o número do id do usuário em "userId".

Exemplo: 
            {
                "myopinion": "Temos que promover o alistamento militar obrigatório",
                "userId": 4
                
            }

Deve retornar:

            {
            "myopinion": "Temos que promover o alistamento militar obrigatório",
            "userId": 4,
            "id": 2
            }




f)Espaço restrito - acesso

Área de opiniões emitidas por usuários inscritos.
Somente usuários logados podem acessar as informações.

Para requisição:
GET /congress

No header da requisição deve conter o token de acesso do usuário logado no portador

Bearer *acess token* 


Não é necessário informação no corpo da requisição.

Deve retornar:
            [
            {
                "myopinion": "Temos que promover o alistamento militar obrigatório",
                "userId": 4,
                "id": 1
            }
            ]
