#Primeiro Passo é a coleta da evidência. Essa pode ser uma imagem forense, gerada por meio do ftk por exemplo, ou uma imagem de máquina virtual
##Por exemplo: vdi;vmdk;vmdkx, qcow, qcow2, etc..

#Tutorial para verificação de arquivo de máquina virtual infectada.

##Arquivo: SRV01TS.vhdx
##Tipo de Vitualização: Windows hyper-v

#Existem duas formas de explorar o arquivo no linux. Pode montar diretamente por meio do "mount", ou montar por meio de um hypervisor, por exemplo VirtualBox

##Para montar direto no linux:
## guestmount --add Caminho/arquivo/SRV01TS.vhdx --inspector --ro /ponto de montagem

<img src="/home/dantesouza/incidente_resposta/captura1.png">



