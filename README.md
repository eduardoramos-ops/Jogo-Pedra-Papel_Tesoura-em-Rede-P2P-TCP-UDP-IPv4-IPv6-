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
   
    # Os protocolos que estarão futuramente no campo da GUI para escolha 
    if protocolo == "UDP":
   
      tipo = socket.SOCK_DGRAM # UDP
   
    else:
   
      tipo = socket.SOCK_STREAM # TCP

# Retorna o novo socket com Ip e protocolo 
    return socket.socket(familia, tipo)

# Finalizamos o commmon, salve o arquivo com CLTR + S. Agora iremos para o main

# Vamos a estrutura da nossa GUI (interface gráfica) do nosso projeto
# Nós importamos do próprio python comandos e a biblioteca tkinter, sendo ela quem gera os widgets.

```import tkinter as tk # Importamos a biblioteca do python e para menos texto chamamos o módulo de tk 
import threading  # Otimiza o código para não ocorrer travamento
import socket #  Importação do socket para criar as conexões de rede (Cliente/Servidor)
import time # Futuramente implementá-lo para fazer com que o código tenha pausas
from common import criar_socket  # Importa função para criar socket TCP/UDP
```

# Vamos as variáveis.
```Criamos variáveis globais, poid serão utilizadas por muitas partes do códigp

# Variáveis globais
# Nenhum nalor definido ainda, então o None indica isso. 
soquete = None
conexao = None
jogada_local = jogada_oponente = ""
placar = {"vitorias": 0, "derrotas": 0, "empates": 0}
```
# O primeiro método em seguida será o de criar o socket
```
def criar_socket(protocolo, ipversao):
    familia = socket.AF_INET6 if ipversao == "IPv6" else socket.AF_INET
    tipo = socket.SOCK_DGRAM if protocolo == "UDP" else socket.SOCK_STREAM
    return socket.socket(familia, tipo)
```
# A classe molde dos métodos
```
# ==== Interface GUI ====
# Uma classe que serve de molde para os métodos que criaremos
class JokenpoApp:
```
# O método para o início do código
```
# Self no primerio argumento para permitir o acesso as atributos e métodos da classe
def __init__(self, janela):
        self.janela = janela
        self.janela.title("Jokenpô em Rede")
        self.nome = "Você"
        self.oponente = "Oponente"
        self.setup_menu()
```
# Criamos o menu para as entradas
```
# O menu com todos os campos necessários para as entradas 
    def setup_menu(self):
        # Limpar toda a vez que reiniciar o widget
        self.limpar()
        self.ip = self.input("IP:", "localhost")
        self.porta = self.input("Porta:", "5000")

# Combobox, para o usuário clicar em itens do menu suspenso
        self.protocolo = self.combo("Protocolo:", ["TCP", "UDP"])
        self.ipversao = self.combo("Versão IP:", ["IPv4", "IPv6"])

# Botões para iniciar como servidor ou cliente 
  # Executa o inicio de servidor e do cliente
        # O command é extremamente util para a requisição de que se o botão foi clicado
        tk.Button(self.janela, text="Servidor", command=self.iniciar_servidor).pack(pady=5)
        tk.Button(self.janela, text="Cliente", command=self.iniciar_cliente).pack(pady=5)
```
# Campos de entrada na janela
```
def input(self, texto, padrao):
        tk.Label(self.janela, text=texto).pack()
        campo = tk.Entry(self.janela)
        campo.insert(0, padrao)
        campo.pack()
        return campo

def combo(self, texto, opcoes):
# Botão com label em menu de digitação
      
        tk.Label(self.janela, text=texto).pack()
        # Verificação de valores na lista sa StrinVar
        var = tk.StringVar(value=opcoes[0])
        tk.OptionMenu(self.janela, var, *opcoes).pack()
        return var

# !!! Nesta etapa preste muita atenção, trabalharemos o servidor/cliente

```
# Inicializando o servidor com um método
    def iniciar_servidor(self):
        global soquete
# Getter do ip digitado 
        ip = self.ip.get()

        # Receberá a entrada da porta no campo de porta 
        porta = int(self.porta.get())

        # Armazenando na variavel soquete o método criar_socket com valores digitados no campo
        soquete = criar_socket(self.protocolo.get(), self.ipversao.get())
        soquete.bind((ip, porta))
        soquete.listen()
        threading.Thread(target=self.aguardar_conexao, daemon=True).start()

        # Mensagem para saber se deu certo ele está aguardando
        self.info("Aguardando conexão...")

# Chama-se esse método quando queremos que apareça essa mensagem caso o botão de serviodor seja clicado
# Criando um camiho para a comunicaçõa do servidor para com o usuário
    def aguardar_conexao(self):
        
        # Variavel global usada pelo servidor
        global conexao
        conexao, _ = soquete.accept()
        self.mostrar_jogo()
        # Linha de execução paralela às execuções ja concebidas com threading

# Quando a threading pricipal encerrar essa encerra também(daemon tem essa função)
# Pesquise a fucionalidade para que você entenda bem a estrutura do código
```

threading.Thread(target=self.receber_jogada_servidor, daemon=True).start()
```
# Iniciando o cliente com a mesma lógica do servidor
# Método para iniciar o cliente 
    def iniciar_cliente(self):
       
        global soquete
        ip = self.ip.get()
        porta = int(self.porta.get())

        # Mesma coisa aqui (armazenando na variavel soquete o método criar_socket) 
        soquete = criar_socket(self.protocolo.get(), self.ipversao.get())
        try:
            soquete.connect((ip, porta))
# Método posterior para mostar as jogadas tanto ao cliente como ao servidor ao mesmo tempo
 self.mostrar_jogo()
 ```
# Quando a threading pricipal encerrar essa encerra também(daemon tem essa função)
 threading.Thread(target=self.receber_jogada_cliente, daemon=True).start()
# Como usamos as janelas, pode ocorrer que sobrecaregue a janela por isso usamos:
  except Exception as e:
# Com a implementação do try, qualquer erro é comunicado. 
  self.janela.after(0, lambda: self.info(f"Erro: {e}")
