##
## Configurar o Jupyter

Gerar arquivo de configurações: `jupyter notebook --generate-config`

Crie seu password:

`ipython -c "from notebook.auth import passwd;passwd()"`
**(guarde a chave gerada)**

Abra o arquivo de configurações:

`sudo nano /home/ubuntu/.jupyter/jupyter_notebook_config.py`

Copie o conteúdo do anexo configNote.txt, substitua acima do Application
1. Alterar Notebook.app_password: Chave que você salvou
2. Alterar Notebook.allow_origin: IP4 Publico

Para entrar pelo Jupyter no navegador acesse: HTTP + IPV4 + 8888

### Configurar de forma mais pratica para o acesso
`cd /etc/nginx/`

`cd sites-available/`

`sudo nano jupyter_app.conf`

Coloque o conteúdo do arquivo nginx.txt

`cd sites-enabled/`

`sudo rm default`

`cd`

`sudo systemctl reload nginx`

`sudo ln -s /etc/nginx/sites-available/jupyter_app.conf /etc/nginx/sites-enabled/jupyter_app.conf`

`systemctl daemon-reload`

`sudo systemctl reload nginx`

`cd /etc/supervisor/`

`cd conf.d/`

`sudo nano my_jupyter.conf`

Cole o conteúdo do arquivo my_jupyter

`cd`

`sudo mkdir /var/log/my_jupyter`

`sudo supervisorctl status`

`sudo systemctl daemon-reload`

`sudo supervisorctl reread`

`sudo supervisorctl update`

`sudo supervisorctl status my_jupyter`

`sudo nano /home/ubuntu/.jupyter/jupyter_notebook_config.py`

Tirar o IP e colocar um *

Agora você pode acessar o Jupyter apenas pelo IPV4
