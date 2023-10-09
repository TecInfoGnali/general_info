
# Aplicações Linux

Editor Dconf: - Velocidade de minimização de janelas:
`sudo apt-get install dconf-tools`

## Configurações sugeridas para Otimizar e Reparar Sistema

Atualização de Sistema
`sudo apt update && sudo apt full-upgrade -y`

Repararando Pacotes com Falhas
`sudo apt-get check && sudo apt-get install -f -y`

Reparando dpkg
`sudo dpkg -configure -a`

Reparando Pacotes com Falha
`sudo apt-get clean -y && sudo apt-get autoremove -y && sudo apt-get autoclean -y && sudo apt-get remove -f -y`

### [Lista de comando do Howto APT APT-GET do ubuntu](ubuntuhelp_AptGet.md)


**Salve os valores anteriores antes de fazer qualquer alteração**

---

## Configurações sugeridas para `Sysctl.conf`

As modificações do sysctl englobam configurações de sistema que ocorrem ao modificar o arquivo /etc/sysctl.conf como root.
Ao final dele, adicione estas linhas:

vm.swappiness=10 # Define o Swap para ser usado somente quando o sistema tiver 90% de RAM ocupada.
net.ipv4.tcp_syncookies=1 # Tweaks de redes TCP/IP, sincronia de cookis
net.ipv4.ip_forward=1 # Tweaks de redes TCP/IP, gerenciamento de IP
net.ipv4.tcp_dsack=0 # Tweaks de redes TCP/IP
#net.ipv4.tcp_sack=0 # Tweaks de redes TCP/IP
fs.file-max=100000 # Máximo de descritores de arquivos, pode não funcionar para alguns
kernel.sched_migration_cost_ns=5000000 # Altera o tempo que o kernel demora antes de migrar um processo de núcleo. Isso otimiza a máquina caso muitos processos saltem entre núcleos desnecessariamente.
kernel.sched_autogroup_enabled=0
vm.dirty_background_bytes=16777216 # Altera o cache de transferencia USB – Pode piorar em alguns sistemas.
vm.dirty_bytes=50331648 # Altera o cache de transferencia USB – Pode piorar em alguns sistemas.
kernel.pid_max=4194304 #Valor máximo de PID para o kernel

**Salve os valores anteriores antes de fazer qualquer alteração**

---

## Configurações sugeridas para `Limits.conf`
As modificações do Limits.conf englobam configurações de sistema que ocorrem ao modificar o arquivo /etc/security/limits.conf como root. Ao final dele, adicione estas linhas:

hard stack unlimited #
nproc unlimited
nofile 1048576 #
as unlimited #
cpu unlimited #
fsize unlimited #
msgqueue unlimited #
locks unlimited #
* hard nofile 1048576 #
SEUUSUARIO soft nofile 8192 # Modifica o máximo de descritores de arquivos por usuário
SEUUSUARIO hard nofile 16384 # Modifica o máximo de descritores de arquivos por usuário

Todas as linhas acima reajustam como o sistema otimiza e utiliza a memória RAM.

OBS: Fiquem atentos que, em programas bugados, principalmente Java e/ou Wine, poderá haver um grande consumo de memória RAM com estes ajustes.

**Salve os valores anteriores antes de fazer qualquer alteração**

---

## Configurações sugeridas para `GRUB`
Desligue as correções das falhas da Intel e da AMD!

Por já ter abordado isso anteriormente, serei conciso.

Os processadores Intel possuem graves falhas de hardware, corrigidas com software. Porém, pro software corrigir, há uma grande perda de desempenho de processamento. Desabilitar essas correções pode ajudar a melhorar o desempenho! Claro, se você é um usuário que segue bem á risca estas dicas de segurança, não terá problemas caso desabilite isso. – Eu mesmo só uso desabilitado.

Ao terminar de modificar, salve e reinicie o sistema.
Caso dê o erro de initramfs, basta editar novamente o arquivo removendo os parâmetros citados acima.

**Salve os valores anteriores antes de fazer qualquer alteração**

---

## Configurações sugeridas para `FSTAB`
Você certamente vai querer desativar a opção atime em seus sistemas de arquivos.

Com isso desabilitado, a última vez que um arquivo foi acessado não será constantemente atualizado toda vez que você ler um arquivo, uma vez que essas informações geralmente não são úteis e causam acessos extras ao disco.

Para desabilitar, edite seu /etc/fstab como root e adicione o parâmetro noatime ao sistema de arquivos, ficando assim no exemplo:

UUID=1997b70f-990b-48e8-a141-7294f4e20a07 /home ext4 defaults,noatime 0 2

Pra quem usa SSD, adicione a opção discard, que vai habilitar o TRIM independente do sistema de arquivos em uso.
O TRIM libera espaço de arquivos já apagados, evitando sobrescritas desnecessárias e aumentando a vida útil do SSD. Ficará semelhante a:

UUID=1997b70f-990b-48e8-a141-7294f4e20a07 /home ext4 defaults,noatime,discard 0 2

Ao terminar de modificar, salve e reinicie o sistema.
Caso dê o erro de initramfs, basta editar novamente o arquivo removendo os parâmetros citados acima.


---

## Dicas Rápidas

Mantenha sua distro sempre atualizada. Correções e otimizações sempre chegam via update.
Use EXT4 como sistema de arquivos.
Se deseja desempenho de verdade, pode arriscar usar BTRFS. Porém mantendo o bom desempenho e estabilidade, recomendo o EXT4. Motivos? Ele é mais maduro, possui suporte nativo a SSD’s, gera pouca fragmentação nos discos caso você não possua SSD e é mais fácil de recuperar em caso de pane.

**Salve os valores anteriores antes de fazer qualquer alteração**

## Configurações sugeridas para 

**Salve os valores anteriores antes de fazer qualquer alteração**
## Configurações sugeridas para 

**Salve os valores anteriores antes de fazer qualquer alteração**
## Configurações sugeridas para 

**Salve os valores anteriores antes de fazer qualquer alteração**