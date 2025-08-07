# Jogo-Pedra-Papel_Tesoura-em-Rede-P2P-TCP-UDP-IPv4-IPv6-
Nome do projeto: Pedra, Papel e Tesoura em Rede P2P (TCP/UDP, IPv4/IPv6)













# Importamos o socket para que tudo dê certo
import socket


def criar_socket(protocolo="TCP", versao_ip="IPv4"):
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



#Vamos a estrutura da nossa GUI (interface gráfica) do nosso projeto



#Nós importamos do próprio python comandos e a biblioteca tkinter, sendo ela quem gera os widgets.


# Importamos a biblioteca do python e para menos texto chamamos o módulo de tk
import tkinter as tk 

 # Importa do tkinter os widgets mais modernos

from tkinter import ttk

 # Otimiza o código para não ocorrer travamento

import threading

#  Importação do socket para criar as conexões de rede (Cliente/Servidor)
import socket

 # Futuramente implementá-lo para fazer com que o código tenha pausas

import time

 # Importa função para criar socket TCP/UDP

from common import criar_socket