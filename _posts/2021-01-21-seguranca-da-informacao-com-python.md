---
layout: post
title:  "Segurança da Informação com Python"
date:   2021-01-21 03:30:00 -0300
categories: [linux, python, segurança da informação]
---

## Segurança da Informação com Python

<sub>Página gerada de um arquivo do Jupyter Notebook, [este aqui](https://github.com/evttenorio/infosec-py).</sub>

>Área que tem como objetivo asssegurar que todos os dados de uma ou mais informações 
estejam sempre CONFIDENCIAIS, INTEGROS E DISPONIVEIS em qualquer meio de comunicação.

### Princípios da Segurança da Informação

- **Integridade**: Proteger a informação de alterações indevidas.
- **Confidencialidade**: Manter informação confidencial.
- **Disponibilidade**: Garantir que um recurso e/ou informação esteja disponível.

Alguns especialistam também falam destes como princípios:

- **Identificação**: Identificar uma entidade.
- **Autenticação**: Verificar a entidade e suas credenciais.
- **Autorização**: Verificar se autoriza ou não a entidade dentro de um sistema.
- **Não Repudio**: Evitar que uma entidade negue/manipule suas ações em um sistema. Monitorar ações desta entidade.


### Bibliotecas Python

- **os**: Fornece uma maneira simples de usar funcionalidades que são dependentes do SO, como por exemplo o ping.
- **time**: Fornece várias funçoes relacionadas ao tempo, como por exemplo tempo de execução de um código.
- **socket**: Fornece acesso de baixo nível a interface de rede. Controlar abertura, fechamento e sincronização de conexões.
O S.O fornece a API socket que relaciona o programa com a rede, assim é possivel criar um relacionamento com o programa, S.O e a placa de rede.
- **sys**: Fornece acesso a algumas variáveis e funções que tem forte interação com interpretador Python.
- **pyfiglet**: Banners para os scripts.


```python
import os, time, socket, sys 
from pyfiglet import Figlet
```

### ICMP
Internet Control Message Protocol, protocolo integrante do protocolo IP utilizado para fornecer relatórios de erros à fonte original. O ICMP está na camada de rede.

o **Ping** é a ferramenta que utiliza o ICMP para verificar se um determinado host está ativo, enviando mensagens *requests* e recebendo *replys*(respostas) dos hots/nós da rede. Contemplando assim o princípio de **DISPONIBILIDADE**.


```python
with open('hosts.txt') as file:
    dump = file.read()
    dump = dump.splitlines()

    for ip in dump:
        print('\n\U0001F310' + ip)
        x=str(os.popen('ping -n 2 '+ip+'').read())
        print(x)
        print('-' * 65)
        time.sleep(5)
```

### TCP

Transmisson Control Protocol é um dos protocolos de comunicação, que dão suporte a rede global de internet, verificando se os dados são enviados na sequência correta e sem erros - envio de dados de maneira íntegra. 
Contemplando assim o princípio de **INTEGRIDADE**. 

### UDP

User Datagram Protocol, é um protocolo simples da camada de transporte que permite que a aplicação envie um datagrama dentro de um pacote ipv4 ou ipv6 a um destino, porém sem qualquer tipo de garantia que o pacote chegue corretamente.

Não há fidelidade que o pacote chegue(sem integridade) mas irá verificar se o host está recebendo dados, logo contempla o princípio de **DISPONIBILIDADE**. 

UDP e TCP estão na camada de transporte.


```python
banner = Figlet(font='cybersmall')
print('\x1b[1;36m'+ banner.renderText('TCP Client') +'\x1b[0m')

def main():
    try:
        s = socket.socket(socket.AF_INET, socket.SOCK_STREAM, 0)
    except socket.error as err:
        print("\U0000274C Fail!")
        print("Erro: {}".format(err))
        sys.exit()
        
    host = input('\n\U0001F310 Host/IP: ')
    port = input('\U0001F6AA Port: ')
    
    try:
        s.connect((host, int(port)))
        print("\n\U00002714 \x1b[1;32mTCP Client successfully connected in: \x1b[0m" + host + ":" + port)
        print ('\U00002796' * 50)
        s.shutdown(2)
    except socket.error as err:
        print("\n\U0000274C No connection: " + host + ":" + port)
        print("Erro: {}".format(err))
              
if __name__ == "__main__":
    main()
```


```python
banner = Figlet(font='cybersmall')
print('\x1b[1;36m'+ banner.renderText('UDP Server') +'\x1b[0m')

s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

print("\n\U00002714 Socket ok!\n\n")

host = 'localhost'
port = 5432

s.bind((host, port))
message = '\nServer: Hi client!'

while 1:    
    server_data, destiny = s.recvfrom(4096)
    
    if server_data:
        print("Server sending message...")
        s.sendto(server_data + (message.encode()), destiny)
```

```python
banner = Figlet(font='cybersmall')
print('\x1b[1;36m'+ banner.renderText('UDP Client') +'\x1b[0m')

s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
print("\n\U00002714 Socket ok!\n\n")

host = 'localhost'
port = 5433
message = 'Hello server!'

try:
    print("Client say: " + message)
    s.sendto(message.encode(), (host, 5432))
    
    data, server = s.recvfrom(4096)
    data = data.decode()
    print("Client: " + data)
finally:
    print("Client: closed connection")
    s.close()
```

### Bibliotecas Python

- **random**: Implementa geradores de números pseudoaleatórios para várias distribuições.
- **string**:
- **hashlib**: Implementa uma interface comum para muitos algoritmos de hash seguro como SHA1, SHA256, MD5 entre outros.
- **threading**:
- **ipaddress**:


```python
import random, string, hashlib, ipaddress, time
from threading import Thread
```

A biblioteca random é utilizada na ferramenta Pwd Generator para randomizar letras e números para que a cada execução gere resultados aleatórios. 

Contemplando os princípios de **AUTENTICAÇÃO** na medida que há um crendenciamento via senha e **CONFIDENCIALIDADE** por manter uma informação confidencial através de uma autenticação.


```python
banner = Figlet(font='cybersmall')
print('\U0001F511\n'+'\x1b[1;36m'+ banner.renderText('Pwd Generator') +'\x1b[0m')

t = int(input('\U0001F4AC Password length: '))

chars = string.ascii_letters + string.digits + '@#,.,#@'
rnd = random.SystemRandom()

print("\n\n" + ''.join(rnd.choice(chars) for i in range(t)))
print('\U00002796' * 40)
```

    
                                 🔑
     ___  _  _ ___    ____ ____ __ _ ____ ____ ____ ___ ____ ____
     |--' |/\| |__>   |__, |=== | \| |=== |--< |--|  |  [__] |--<

    💬 **Password length:** 8
    
    
    rEpO,OA@
    ➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖
    

### Hash

Funciona como um identificador único gerado através de algoritmo que vai analisar byte/byte de determinado dado para gerar de forma única, um determinado código que só aquele arquivo terá. Se neste mesmo arquivo um bit for alterado, o hash será outro.

Por ser uma espécie de proteção à informações, contempla o princípio de **INTEGRIDADE**.


```python
banner = Figlet(font='cybersmall')
print('\U0001F511\n'+'\x1b[1;36m'+ banner.renderText('Hash Compare') +'\x1b[0m')

arquivo1 = 'a.txt'
arquivo2 = 'b.txt'

hash1 = hashlib.new('ripemd160')
hash2 = hashlib.new('ripemd160')

hash1.update(open(arquivo1, 'rb').read())
hash2.update(open(arquivo2, 'rb').read())

if hash1.digest() != hash2.digest():
    print (f'O arquivo: {arquivo1} é diferente do {arquivo2}')
    print()
    print('O hash do arquivo a.txt é ', hash1.hexdigest())
    print('O hash do arquivo b.txt é ', hash2.hexdigest())
else:
    print (f'O arquivo: {arquivo1} é igual ao {arquivo2}')
    print()
    print('O hash do arquivo a.txt é ', hash1.hexdigest())
    print('O hash do arquivo b.txt é ', hash2.hexdigest())
```

                                 🔑
     _  _ ____ ____ _  _   ____ ____ _  _ ___  ____ ____ ____
     |--| |--| ==== |--|   |___ [__] |\/| |--' |--| |--< |===
 
    **O arquivo:** a.txt **é igual ao** b.txt
    
    **O hash do arquivo a.txt é**  0eb141a158107ab1396b50dd9be97e4cdb1b2514
    **O hash do arquivo b.txt é**  0eb141a158107ab1396b50dd9be97e4cdb1b2514
    


```python
banner = Figlet(font='cybersmall')
print('\x1b[1;31m'+ banner.renderText('Hash Generator') +'\x1b[0m')

#md5r = hashlib.md5(b'Python')
#print ('-- ',md5r.hexdigest()+ ' --')

string = input('\x1b[0;33m'+ 'Digite o texto a ser gerado: '+'\x1b[0m')

resultado = hashlib.md5(string.encode('utf-8'))
print('\x1b[0;36m'+ "\nMD5 de", string, '->'+'\x1b[0m', resultado.hexdigest())

resultado = hashlib.sha1(string.encode('utf-8'))
print('\x1b[0;36m'+ "\nSHA1 de", string, '->'+'\x1b[0m', resultado.hexdigest())

resultado = hashlib.sha256(string.encode('utf-8'))
print('\x1b[0;36m'+ "\nSHA25 de", string, '->'+'\x1b[0m', resultado.hexdigest())

resultado = hashlib.sha512(string.encode('utf-8'))
print('\x1b[0;36m'+ "\nSHA512 de", string, '->'+'\x1b[0m', resultado.hexdigest())
```

     _  _ ____ ____ _  _   ____ ____ __ _ ____ ____ ____ ___ ____ ____
     |--| |--| ==== |--|   |__, |=== | \| |=== |--< |--|  |  [__] |--<
    
    **Digite o texto a ser gerado:** Este é o Curso de Python para Segurança
   
    **MD5 de Este é o Curso de Python para Segurança ->** 17601d464793445d7403a095da523c16
    
    **SHA1 de Este é o Curso de Python para Segurança ->** ad5ba5453ba968a350fce77e25bc6d0607af1c06
    
    **SHA25 de Este é o Curso de Python para Segurança ->** ebff39ad58567f11fd75f0eed158854207ca4d0a5e140c08607f71910f86c3bf
    
    **SHA512 de Este é o Curso de Python para Segurança ->** 38fd01dba0c893355ecccf958504f632a9a8a97c41ec9912a8b2da692c0f335f4137d99bb7b7093bcc48868bba51cf7552a7a6ffc31fec3863d124b191ca9a15
    

```python
ip = "172.16.17.0/24"

rede = ipaddress.ip_network(ip)

for ip in rede:
    print(ip)
```

    172.16.17.0
    172.16.17.1
    172.16.17.2
    172.16.17.3
    172.16.17.4
    172.16.17.5
        ...
    172.16.17.255
    


```python
ports = [21,22,23,443,80,8080]

for port in ports:
    client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    client.settimeout(0.5)
    codigo = client.connect_ex(('xxxxx.com.br', port))
    
    if codigo == 0:
        print (port, "OPEN")
```

    21 OPEN
    22 OPEN
    443 OPEN
    80 OPEN
    

```python
import phonenumbers
from phonenumbers import geocoder

phone = input('Digite o telefone no formato +551140028922: ')

phone_number = phonenumbers.parse(phone)
print(geocoder.description_for_number(phone_number, 'pt'))
```

`Output:`
    Digite o telefone no formato +551140028922: +558240028922
    Maceió - AL
    

