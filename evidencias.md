# Montagem de imagem de Disco Virtual para Análise de Incidente

## Escopo

Esse Documento mostra como fazer montagem de uma imgem de disco virtual direto em um Desktop Linux, ou em uma Estação Forense Virtual, baseada no Sans-Sift

Primeiro Passo para realização de uma análise de Incidente é a coleta da evidência. Essa pode ser uma imagem forense, gerada por meio do ftk por exemplo, ou uma imagem de Máquina virtual que podem ter os seguintes formatos: vdi, vmdk, vmdkx, qcow, qcow2, etc..

# Tutorial para verificação de arquivo de máquina virtual infectada.

## Arquivo: 
imgem.vhdx
## Tipo de Vitualização:
 Windows Hyper-V

Existem duas formas de explorar o arquivo no linux. Pode montar diretamente por meio do "mount", ou montar por meio de um hypervisor, por exemplo VirtualBox.

# Para montar imagem de disco direto no Desktop linux:
 guestmount --add Caminho/arquivo/ imagem.vhdx --inspector --ro /ponto de montagem

<img src="captura.png">

Mas se você estiver usando uma estação virtual forense, tipo Sans-Sift, no virtualbox, precisará montar esse disco como disco virtual adicionando á máquina virtual. Para isso será necessário seguir alguns passos.

## Montagem de Disco virtual em estação Linux Forense Virtual - Virtualbox

1 - Converter o arquivo. Para isso, pode utilizar o comando vboxmanage

        vboxmanage clonehd inputFileName.vhdx outputFileName.vdi --format vdi


Obs. Ele não gera hash automaticamente. Precisará combinar esse comando com outros comandos através do " | " para gerar um arquivo de hash na hora da conversão do arquivo de disco.

        vboxmanage clonehd Virtual\ Hard\ Disks/imagem.vhdx imagem.vdi --format vdi | sha256sum >sha256sum.txt

2 - Adicionar o disco a vm do virtualbox.

    Para adicionar o dico a vm (no meu caso o sans-sift da Sans. Mas pode ser qualquer Linux), seguir o seguinte caminho:

        Vitualbox/ VM/ (Menu) Configurações/ Armazenamento/ Controlador Sata/ Acrescentar Disco rígido/ procurar disco virtual/ Depois do disco adicionado, clicar em "ok" pra salvar

<img src="virtualbox2.2.png">
<img src="virtualbox2.1.png">
<img src="virtualbox2.3.png">
<img src="virtualbox2.4.png">
<img src="virtualbox2.5.png">
<img src="virtualbox2.6.png">

Obs: Talvez seja  necessário alterar a ordem do boot da máquina virtual durante a inicialização.

3 - Montar o Disco como somente leitura na Estação Forenese virtual.

    Quando a máquina virtual sans iniciar, entre como sudo e dê o seguinte comando para verificar se ele está encontrando o Disco virtual adicionado.

        # fidisk -l
    
    Lembrando que se esse disco estiver em primero, ele irá inverter a ordem dos discos. O Disco do da máquina virtual sans ele irá atribuir como sdb e o disco virtual adicionado ele irá atribuir como sda

<img src="sans1.png">
<img src="sans2.png">
<img src="sans4.png">


        









