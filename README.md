##
## Configuração VPC

**Criando VPC** - Create VPC:
1. Somente VPC
2. Nome: projeto-vpc
3. IPV4: 10.0.0.0/16
4. **Criar VPC**

**Criando Sub-rede** - Create sub-rede:
1. Seleciona a rede privada criada (VPC)
2. 10.0.1.0/28
3. Nome: projeto-sub
4.  **Criar Sub-rede**
5.  Edita a Sub-rede criada
6.  Habilitar IPV4 público

**Criar Gateway da internet** - Criar gateway da internet:
1. Nome: projeto-gw
2. **Criar**
3. Ações > associar a VPC

**Configurar tabela de rotas**:
1. Seleciona a rota do VPC que você criou (utilize a coluna VPC para identificar)
2. No menu de baixo vá para aba **Rotas**
3. Editar rotas
4. Alvo: local
5. Destino: 0.0.0.0/0
6. Alvo: internet gateway
##
## Criar Servidor Ubuntu (EC2)

1. Executar Instância
2. Nome: projeto-EC2
3. Servidor Ubuntu 22/04
4. t2.micro
5. Firewall: Criar grupo de segurança
6. Key: Criar > RSA .pem (guardar essa chave em uma pasta, de preferencia crie uma pasta para os arquivos)
7. Configuração de rede: **Editar**
    * VPC criado
    * Sub-rede criada
    * Nome do gurpo de segurança: projeto-GS
    * Adicionar nova regra de grupo de segurança:
        1. HTTP, personalizado, 0.0.0.0/00, HTTP1
        2. HTTP, personalizado, ::0, HTTP2
        3. HTTPS, personalizado, 0.0.0.0/00, HTTPS1
        4. HTTPS, personalizado, ::0, HTTPS2
        5. TCP, personalizado, 8888, 0.0.0.0/00, Jupyter1
        6. TCP, personalizado, 8888, ::00, Jupyter2
8. Detalhes avançados: ultimo campo de texto > colar conteúdo do arquivo install.txt
9. **Criar**
* Seleciona EC2 criado > Conectar > Copiar conteudo **Exemplo** (contem o ssh que seŕa utilizado)
* Dê permissão para a chave criada com o comando:
  `chmod 400 nomedachave`
* Crie um arquivo de excução rapida: `nano connect.sh`, coleque o conteúdo **Exemplo** copiado (que contem ssh)
* Deixe ele como script: `chmod +x connect.sh`
* Para abrir o servido basta usar `./connect.sh`
* No servidor aberto no CMD, passe novamente o conteúdo de install.txt
* Para abrir no navegador utilize o IPV4 com HTTP
