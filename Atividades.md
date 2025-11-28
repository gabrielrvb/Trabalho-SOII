Markdown
# Projeto Final - Capítulos 6, 7 e 9
## RELATÓRIO DE PRÁTICAS E CÓDIGOS
**Nome do Aluno:** Gabriel Rodrigues Vieira Brandão
**Turno:** Noite
**Data do Último Commit:** 28/11/2025
---
## ATIVIDADE 1: Relatório das Práticas de Aula

Registros das tarefas de administração básica do sistema executadas na máquina virtual, apresentados apenas com descrições e retornos textuais do terminal, como exigido na disciplina.

---

### Capítulo 6: Práticas de Discos e Montagem

#### Prática 8b65b431 01 (Livro-Texto p. 171)

* *Resumo da Prática:* Configurei um novo disco na VM, preparei uma partição primária, formatei no padrão ext4 e realizei a montagem no diretório /backup, incluindo a regra no arquivo de montagem automática do sistema.

* *Evidência de Validação:*

Saída do comando 'cat /etc/fstab'

# /etc/fstab: static file system information.

#

# Use 'blkid' to print the universally unique identifier for a

# device; this may be used with UUID= as a more robust way to name devices

# that works even if disks are added and removed. See fstab(5).

#

# systemd generates mount units based on this file, see systemd.mount(5).

# Please run 'systemctl daemon-reload' after making changes here.

#

# <file system> <mount point>   <type>  <options>       <dump>  <pass>

# / was on /dev/sda1 during installation

UUID=27f24091-457e-4618-875a-ee63af523bde /               ext4    errors=remount-ro 0       1

# swap was on /dev/sda5 during installation

UUID=4b560669-0b76-486d-8989-3f026d6193ca none            swap    sw              0       0
/dev/sr0        /media/cdrom0   udf,iso9660 user,noauto     0       0
UUID=c7431955-d3e1-4a51-8df4-0aa285029fe8 /backup ext4 defaults 0 0

Saída do comando 'df -h'
Filesystem      Size  Used Avail Use% Mounted on
udev            959M     0  959M   0% /dev
tmpfs           197M  576K  197M   1% /run
/dev/sda1        19G  2.3G   16G  13% /
tmpfs           984M     0  984M   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
/dev/sdb1       2.0G   24K  1.9G   1% /backup
tmpfs           197M     0  197M   0% /run/user/1000

---

#### Prática 8b65b431 02 (Livro-Texto p. 172)

* *Resumo da Prática:* Preparei um ponto de montagem em /home/usuario/cdrom para acessar a mídia óptica virtual e montei manualmente o dispositivo do drive para testar a leitura do arquivo presente na ISO.

* *Evidência de Validação:*

Saída do comando 'df -h'
Filesystem      Size  Used Avail Use% Mounted on
udev            959M     0  959M   0% /dev
tmpfs           197M  576K  197M   1% /run
/dev/sda1        19G  2.3G   16G  13% /
tmpfs           984M     0  984M   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
/dev/sdb1       2.0G   24K  1.9G   1% /backup
tmpfs           197M     0  197M   0% /run/user/1000
/dev/sr0        364K  364K     0 100% /home/userlinux/cdrom

Saída do comando 'cat /home/usuario/cdrom/arquivo.txt'
AIED VIVO

---

### Capítulo 7: Práticas de Processos

#### Prática prc0001 01 (Livro-Texto p. 233)

* *Resumo da Prática:* Ajustei o locale do sistema para UTF-8, iniciei a gravação do terminal com script e executei a listagem de processos, usando filtro para localizar apenas entradas referentes ao Python dentro da sessão capturada.

* *Evidência de Validação:*

Saída do comando 'cat /home/usuario/typescript' (após filtrar por 'python')
Script started on 2025-11-24 23:11:38-03:00 [TERM="xterm-256color" TTY="/dev/pts/0" COLUMNS="120" LINES="30"]
userlinux@debian:~$ ps aux | grep python
userlin+     634  0.0  0.1   6336  2072 pts/1    S+   23:11   0:00 grep python
userlinux@debian:~$ exit
exit

Script done on 2025-11-24 23:12:02-03:00 [COMMAND_EXIT_CODE="0"]

---

### Capítulo 9: Práticas de Redes

#### Prática 0002 checkpoint03 (Livro-Texto p. 286)

* *Resumo da Prática:* Configurei um IP estático na interface de rede da VM e usei os comandos de inspeção para confirmar o endereço atribuído e a rota padrão definida.

* *Evidência de Validação:*

Saída do comando 'ip address show enp0s3'
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
link/ether 08:00:27:1f:1d:52 brd ff:ff:ff:ff:ff:ff
inet 10.0.2.3/24 brd 10.0.2.255 scope global enp0s3
valid_lft forever preferred_lft forever
inet6 f000::a00:27ff:fe1f:1d52/64 scope global dynamic mngtmpaddr
valid_lft 86245sec preferred_lft 14245sec
inet6 fe80::a00:27ff:fe1f:1d52/64 scope link
valid_lft forever preferred_lft forever

Saída do comando 'ip route'
default via 10.0.2.2 dev enp0s3 onlink
10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.3
169.254.0.0/16 dev enp0s3 scope link metric 1000

Saída do comando 'cat /etc/network/interfaces'
auto lo
iface lo inet loopback

auto enp0s3
iface enp0s3 inet static
address 10.0.2.3
netmask 255.255.255.0
gateway 10.0.2.2
dns-nameservers 8.8.8.8

---

#### Prática 0002 checkpoint04 (Livro-Texto p. 287)

* *Resumo da Prática:* Alterei o arquivo de interfaces para usar DHCP como método de IP principal. Também apliquei novamente o IP estático como secundário apenas para estudo, verificando ambas as configurações ativas e suas rotas correspondentes.

* *Evidência de Validação:*

Saída do comando 'ip address show enp0s3'
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
link/ether 08:00:27:1f:1d:52 brd ff:ff:ff:ff:ff:ff
inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic enp0s3
valid_lft 85859sec preferred_lft 85859sec
inet 10.0.2.3/24 scope global secondary enp0s3
valid_lft forever preferred_lft forever
inet6 fd00::a00:27ff:fe1f:1d52/64 scope global dynamic mngtmpaddr
valid_lft 86349sec preferred_lft 14349sec
inet6 fe80::a00:27ff:fe1f:1d52/64 scope link
valid_lft forever preferred_lft forever

Saída do comando 'ip route'
default via 10.0.2.2 dev enp0s3
10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.15
169.254.0.0/16 dev enp0s3 scope link metric 1000

Saída do comando 'cat /etc/network/interfaces'
auto lo
iface lo inet loopback

auto enp0s3
iface enp0s3 inet dhcp

---

#### Prática 0002 checkpoint05 (Livro-Texto p. 288)

* *Resumo da Prática:* Utilizei a ferramenta wget para baixar o arquivo de instalação na pasta temporária da VM, confirmando o conteúdo do script após o download.

* *Evidência de Validação:*

Saída do comando 'cat /tmp/install.py'
#!/usr/bin/python3
import os;
import sys
import platform
machine2bits = {'AMD64': 64, 'x86_64': 64, 'i386': 32, 'x86': 32, 'i686' : 32, 'armv7l': 32};
os_version = machine2bits.get(platform.machine(), None);

os.system("apt update");
os.system("wget -O /tmp/install.py [https://www.aiedonline.com.br/install.py](https://www.aiedonline.com.br/install.py)");
os.system("chmod +800 /tmp/install.py");

# Saída do comando cat esperada (conteúdo do script)

#OK, será usado para instalação do aied.com.br

---
## ATIVIDADE 2: Mapa Mental (Conceitos Chave)
* **Instrução:** Esta atividade é **física** e **manual**.
* **Tarefa:** Crie um Mapa Mental em uma **única folha A4**, feito à mão, conectando os
conceitos centrais dos Capítulos 6, 7 e 9. Não pode ser feito a lápis.
* **Entrega:** Entregar a folha A4 fisicamente ao professor antes da prova, até o dia
**28/11/2025**.
---
