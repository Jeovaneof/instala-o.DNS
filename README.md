## INSTALAÇÃO DO SERVIDOR DNS
- ### PASSO 1:
### Atualização de pacotes:
`$ apt-get update`

`$ apt-get upgrade`

## INÍCIO DAS CONFIGURAÇÕES DE REDE:
`$sudo ifconfig`

- ### OBS: o comando a cima indicará as configurações da máquina atual,como ip,broadcast e máscara.

`$sudo nano /etc/network interfaces`

- ### OBS: O comando a cima indica a abertura e edição de uma interface de edição, a fim de inserir os endereços fixos que o servidor irá utilizar.

- ## PASSO 02
### Configurações de domínio:

`$ sudo nano  /etc/hosts`

- ### OBS: Ao acessar o comando a cima,deve-se inserir um domínio válido,além do nome da máquina do usuário logado:

### Após a ação ser executada, é necessário salvar e  fechar a página de edição usando:

- ### CRTL+ O + ENTER + CRTL X

### Após isso é necessário reiniciar o sistema, para isso é utilizado o comando: 

`$ sudo reboot`

### Após a reinicialização do sistema é necessário fazer um teste de resolvimento,para isso testaremos o endereço de DNS do Google:

`$ sudo nano /etc/resolv.conf`

- ### Ao acessar o editor, insira o endereço: nameserver + 8.8.8.8., após isso, salve o arquivo e saia do editor.

# INSTALAÇÃO DO DNS

## Utilize os comandos a baixo:

`$ sudo apt-get install bind9`

## O bind9 foi o tipo de DNS que foi utilizado na instalação.

`$ sudo /etc/init.d/bind9 status`

- ## O comando a cima irá indicar se a configuração de rede e a instalação foi efetivada com sucesso.

- ## CRIAÇÃO DE ZONAS DIRETAS E INVERSAS:

`$sudo nano named.conf.local`

- ### Após a abertura serão adicionados a zona o endereça,emto de domínio que já foi inserido anteriormente e o caminho para onde será salva essa zona, que no caso é /etc/bind.

- ### DA mesma forma será adicionada a zona inversa, que corresponde as mesmas informações da zona direta, a diferença é o endereçamento do ip que estará na ordem inversa.

## Agora é hora de configurar as zonas que foram criadas para isso, utilize:

` sudo nano named.conf.options`

### OBS: Ao abrir a tela de edição, descomente o FORWARDERS e adicione o endereço de seu roteador,e também um endereço de DNS válido,o do Google por exemplo. Após isso, salve e feche o editor.

- ### Alteração de nomes de configuração para a edição usando:

`$ sudo cp db.local novonome`

`$sudo cp db.127 novonome`

- ### Início das alterações das zonas diretas: usam-se os comandos;

`$sudo nano db.novonome`

### Após aberto o editor ,insere-se o nome do domínio e da máquina que está sendo feita a configuração e são adiconados registros pelos quais o DNS irá buscar.

### O comando a cima serve tanto para a zona direta,quanto para a zona inversa.

- ## Após inseridos os dados das permissões, salve usando o mesmo método aplicado anteriormente e feche o editor.

### Após isso deve-se reiniciar o Bind utilizando o comando:

`$ sudo /etc/init.d/bind restart
`

- ## Vistoria nos arquivos a fim de verificar erros.

`$ named-checkzone db.nomeusado /etc/bind/db.nomeusado`

### Deve-se fazer a checagem tanto da zona direta como da zona inversa,utilizando o mesmo comando,alterando apenas o nome que foi utilizado pelo usuário.

- ### TESTES:

`$ host - l nomedodominio`

`$ dig nome do domínio`

`$ ping nome de qualquer domínio válido`

### OS comandos a cima verificam respectivamente, os hosts ativos na rede, a seção de resposta e autorizativos e se o DNS encontra um endereço válido na internet.
