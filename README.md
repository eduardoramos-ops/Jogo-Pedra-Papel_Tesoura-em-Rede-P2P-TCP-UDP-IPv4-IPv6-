# Jogo-Pedra-Papel_Tesoura-em-Rede-P2P-TCP-UDP-IPv4-IPv6-
Nome do projeto: Pedra, Papel e Tesoura em Rede P2P (TCP/UDP, IPv4/IPv6).
Esse projeto tem como objetivo atender ao critério de lógica e comunicação P2P implementado no python de forma simples, proporcionando uma maneira visual e interativa os conceitos de Redes de Computadores e programação back-end.
É importante ressaltar que se uma das etapas não forem efetuadas, é provável que o projeto não execute de forma eficiente e/ou agradável. 



# Vamos iniciar com a documentação para que você acompanhe bem o projeto
No gerenciador do seu Pc, crie uma pasta chamada JOGOPPT.
Salve preferencialmente no seu drive.

# Usaremos o editor de código Visual Code Studio

Instale ele caso não tenha em seu Pc.
<br>
Instale o python no seu Pc caso não o tenha instalado.
<br>
Abra o code studio e instale o python 3.15 e sua extensão.
<br>
Após efetuar essas etapas, vá em file e clique em open folder e abra o arquivo criado (JOGOPPT).
<br>
Dentro dele crie dois file, um chamado common e outro chamado main. Use a terminação .py após o nome do arquivos sem espaço.
<br>
Concluído! Salve e use o código-fonte que estará na raiz do repositório para o projeto funcionar.
<br>

# Vamos iniciar o projeto
# Iniciando pelo common 

# Importamos o socket da bilbioteca do python com esse comando
```import socket```

  #  Usando if e else para as escolhas de IP  
  ```# Versoes de Ip com AF_INET e AF_INET
    if versao_ip == "IPv6":

     familia = socket.AF_INET6 #Ipv6
    
    else:
    
     familia = socket.AF_INET #IPv4

```
 # Estrutura condicional pra comparar os tipos de protocolos escolhidos na GUI     
   
    ```# Os protocolos que estarão futuramente no campo da GUI para escolha ```
    if protocolo == "UDP":
   
      tipo = socket.SOCK_DGRAM # UDP
   
    else:
   
      tipo = socket.SOCK_STREAM # TCP

# Retorna o novo socket com Ip e protocolo 
    return socket.socket(familia, tipo)



# Vamos a estrutura da nossa GUI (interface gráfica) do nosso projeto


```import tkinter as tk # Importamos a biblioteca do python e para menos texto chamamos o módulo de tk 
from tkinter import ttk # Importa do tkinter os wWdgets mais modernos
import threading  # Otimiza o código para não ocorrer travamento
import socket #  Importação do socket para criar as conexões de rede (Cliente/Servidor)
import time # Futuramente implementá-lo para fazer com que o código tenha pausas
from common import criar_socket  # Importa função para criar socket TCP/UDP
```

# Nós importamos do próprio python comandos e a biblioteca tkinter, sendo ela quem gera os widgets.

