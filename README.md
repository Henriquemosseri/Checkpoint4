Performance Cache API
Resumo
API em C# com ASP.NET Core que busca usuários do MySQL e usa Redis para cache, melhorando a performance.
Foco em microserviços: serviço pequeno, independente e rápido, seguindo boas práticas de arquitetura moderna.

Estrutura
Model: User → Id, Name, Email, UltimoAcesso.
Controller: HomeController → Recebe requisições, verifica cache e consulta banco.

Funcionalidade
Ao receber GET /api/home:
Verifica se os usuários estão no Redis.
Se estiverem, retorna os dados do cache.
Se não, busca no MySQL, atualiza e salva no Redis.

Cache:
Expira em 15 minutos.
Reduz consultas repetidas ao banco, aumentando baixa latência.

Conceitos de Microserviço Aplicados:
Serviço único e focado:
Cada microserviço deve ter uma única responsabilidade. Neste caso, ele gerencia apenas os usuários. Isso facilita manutenção, testes e evolução do serviço sem impactar outros serviços.
Escalabilidade independente:
Microserviços podem ser escalados separadamente. Por exemplo, se o serviço de usuários estiver recebendo muitas requisições, podemos replicar apenas ele, sem precisar escalar outros serviços da aplicação.
Resiliência:
O uso de Redis como cache garante que o serviço continue respondendo mesmo que o banco de dados MySQL esteja lento ou temporariamente indisponível. Isso aumenta a tolerância a falhas.
Baixo acoplamento:
Cada microserviço funciona independentemente, sem depender diretamente de outros sistemas. Isso facilita atualizações e trocas de tecnologia.
Comunicação via API:
Microserviços se comunicam geralmente por HTTP/REST ou mensageria. Neste exemplo, o serviço fornece uma API REST simples que pode ser consumida por frontend, outros serviços ou aplicativos móveis.

