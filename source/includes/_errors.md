# Erros

A nossa API funciona com os seguintes códigos de erro:


Código do erro | Descrição
---------- | -------
400 | Bad Request -- Algo está errado nas informações enviadas
401 | Unauthorized -- O Token usado é inválido ou está incorreto
403 | Forbidden -- O endpoint acessado não está disponível para o seu nível de autorização
404 | Not Found -- O item requisitado não foi encontrado, verifique a URL e tente novamente
405 | Method Not Allowed -- O método usado não é suportado
406 | Not Acceptable -- Você requisitou um formato diferente de JSON, nossa API só funciona com JSON :(
500 | Internal Server Error -- Nosso servidor apresentou algum problema, entre em contato conosco por e-mail: contato@newinfotech.com.br.
503 | Service Unavailable -- O nosso servidor pode estar em manutenção ou muito ocupado no momento.
