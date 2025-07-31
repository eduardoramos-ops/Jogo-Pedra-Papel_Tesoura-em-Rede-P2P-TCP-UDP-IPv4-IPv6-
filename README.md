# Jogo-Pedra-Papel_Tesoura-em-Rede-P2P-TCP-UDP-IPv4-IPv6-
Nome do projeto: Pedra, Papel e Tesoura em Rede P2P (TCP/UDP, IPv4/IPv6)

import socket

def create_socket(protocolo, versao_ip):
    if versao_ip.upper() == 'IPv6':
        familia = socket.AF_INET6
    else:
        familia = socket.AF_INET

    if protocolo.upper() == 'TCP':
        tipo_socket = socket.SOCK_STREAM
    elif protocolo.upper() == 'UDP':
        tipo_socket = socket.SOCK_DGRAM
    else:
        raise ValueError("Protocolo inválido. Use TCP ou UDP.")

    return socket.socket(familia, tipo_socket)

