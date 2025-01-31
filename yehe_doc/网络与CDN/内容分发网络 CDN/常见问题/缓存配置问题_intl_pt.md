[](id:q1)

### O que é a configuração da validade do cache?
A configuração da validade do cache refere-se a um conjunto de políticas de validade que os nós de cache do CDN devem seguir ao armazenar em cache o conteúdo da sua empresa.
Todos os recursos armazenados em cache nos nós do CDN têm uma validade. Para os recursos não expirados, quando uma solicitação chegar ao nó, ele retornará diretamente o recurso solicitado ao usuário, de modo a agilizar a aquisição do recurso. Para os recursos expirados, o nó encaminhará a solicitação do usuário ao servidor de origem, readquirirá o recurso e o armazenará em cache no nó, e depois o retornará ao usuário. Uma validade de cache adequada pode melhorar efetivamente a taxa de acertos de recursos e diminuir a taxa de pull de origem, reduzindo o uso de largura de banda.


[](id:q2)
### Como posso controlar a validade do cache de arquivos em um navegador?
É possível configurar a validade do cache do navegador no console. Para obter mais informações, consulte [Configuração da validade do cache do navegador](https://intl.cloud.tencent.com/document/product/228/38932).

[](id:q3)
### Eu uso meu próprio servidor como o servidor de origem do CDN. Posso configurar o CDN para não armazenar em cache um tipo específico de arquivos? Posso definir a validade do cache para "0" para desabilitar o armazenamento em cache?
É possível configurar períodos diferentes de validade do cache para tipos de diretórios e arquivos diferentes. Se a validade do cache for configurada como "0", o nó do CDN não armazenará o recurso em cache. Assim, o nó do CDN precisará efetuar pull dos recursos relacionados do servidor de origem toda vez que os usuários enviarem solicitações de acesso ao nó. Para obter mais informações sobre as configurações de cache, consulte [Configuração da validade do cache do nó (herdada)](https://intl.cloud.tencent.com/document/product/228/35317).

[](id:q4)
### Quais configurações de validade de cache são aceitas pelo Tencent Cloud?
O CDN do Tencent Cloud aceita a configuração de ações de cache e regras de validade de cache para vários tipos de arquivo, além de ser possível ajustar a prioridade das regras de cache personalizadas. Regras de validade de cache adequadas podem melhorar efetivamente a taxa de acertos de recursos e diminuir a taxa de pull de origem, reduzindo o uso de largura de banda. Para obter mais informações, consulte [Configuração do cache](https://intl.cloud.tencent.com/document/product/228/35315).

[](id:q5)
### Qual é a configuração de cache padrão do CDN?
Ao adicionar um nome de domínio de aceleração, regras de validade de cache de nó padrão são adicionadas com base em tipos diferentes de serviço de aceleração e podem ser modificadas conforme necessário.
- Se a aceleração estática for selecionada, os arquivos dinâmicos gerais (como arquivos PHP, JSP, ASP e ASPX) não serão armazenados em cache por padrão e outros arquivos serão configurados para seguir o servidor de origem por padrão.
- Se a aceleração de download ou de streaming de VOD for selecionada, a validade do cache padrão de todos os arquivos será de 30 dias.


[](id:q6)
### O que são as regras de correspondência de cache?
Quando várias regras de cache são definidas, as que estão na parte inferior da lista têm prioridade mais alta. Por exemplo, se um nome de domínio for configurado da seguinte maneira:
```
Todos os arquivos - 30 dias
.php .jsp .aspx - 0 segundo
.jpg .png .gif - 300 segundos
/test/*.jpg - 400 segundos
/test/abc.jpg - 200 segundos
```

Se o nome do domínio for `www.test.com` e o recurso for `www.test.com/test/abc.jpg`, a regra correspondente será a seguinte:
1. Corresponde com a primeira regra. É atingido, então a validade do cache é de 30 dias.
2. Corresponde com a segunda regra. Não é atingido.
3. Corresponde com a terceira regra. É atingido, então a validade do cache é de 300 segundos.
4. Corresponde com a quarta regra. É atingido, então a validade do cache é de 400 segundos.
5. Corresponde com a quinta regra. É atingido, então a validade do cache é de 200 segundos.

A validade final do cache está sujeita ao último resultado correspondente; portanto, será de 200 segundos.
