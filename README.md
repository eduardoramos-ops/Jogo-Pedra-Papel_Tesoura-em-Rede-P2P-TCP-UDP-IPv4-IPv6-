# Jogo-Pedra-Papel_Tesoura-em-Rede-P2P-TCP-UDP-IPv4-IPv6-
Nome do projeto: Pedra, Papel e Tesoura em Rede P2P (TCP/UDP, IPv4/IPv6)
Esse projeto tem como objetivo atender ao critério de lógica e comunicação P2P implementado no python de forma simples, proporcionando uma maneira visual e interativa os conceitos de Redes de Computadores e programação back-end.É




# Importamos o socket para que tudo dê certo
import socket


```def criar_socket(protocolo="TCP", versao_ip="IPv4"):```
   
 """Cria e retorna um socket configurado com protocolo e versão IP."""

  # Aqui serve pra comparar usando if e else as escolhas de IP  
    if versao_ip == "IPv6":
        # Modos de Ip para escolher 
     
     familia = socket.AF_INET6 #Ipv6
    
    else:
    
     familia = socket.AF_INET #IPv4


 # Estrutura condicional pra comparar os tipos de protocolos escolhidos na GUI     
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

