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
