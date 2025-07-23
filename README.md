# 🔄 Converter VDI (VirtualBox) para VMDK (VMware)

Este guia demonstra como converter uma imagem `.vdi` (VirtualBox) para `.vmdk` (VMware), além de mostrar como importar, configurar e instalar o VMware Tools para uso da VM convertida.

---

## 🧰 Requisitos

- VirtualBox instalado
- VMware Workstation ou VMware Player
- Acesso ao terminal (CMD/PowerShell) com permissões administrativas
- VM desligada antes da conversão

---

## ⚙️ Modo CLI (PowerShell ou CMD)

### 1. Acesse a pasta do VBoxManage
```powershell
cd "C:\Program Files\Oracle\VirtualBox"
```

### 2. Execute o comando de conversão
```powershell
.\VBoxManage.exe clonehd `
'C:\CAMINHO\ORIGEM\arquivo.vdi' `
'C:\CAMINHO\DESTINO\novo.vmdk' `
-format VMDK
```

---

## 🖱️ Modo Gráfico (VirtualBox)

1. Vá em **File > Virtual Media Manager** (`Ctrl+D`)  
2. Selecione o disco `.vdi` e clique em **Copy** (`Ctrl+Shift+C`)  
3. Escolha o formato `VMDK`  
4. Defina nome, local de salvamento e tipo de alocação (dinâmico ou fixo)

---

## 📦 Importando no VMware

1. Abra o VMware e clique em **"Create a New Virtual Machine"**  
2. Escolha **"I will install the operating system later"**  
3. Selecione o SO (ex: Kali Linux)  
4. Defina nome da VM e local de instalação  
5. Marque **"Split virtual disk into multiple files"**  
6. Clique em **"Customize Hardware"** e configure como era no VirtualBox  
7. Finalize o assistente

> Substitua o disco `.vmdk` criado automaticamente pelo que foi convertido, mantendo o mesmo nome

---

## 🧹 Desinstalando VirtualBox Tools

Dentro da VM Linux:
```bash
sudo apt purge virtualbox*
cd /opt/VBoxGuestAdditions-*/ && sudo ./uninstall.sh
```

---

## 🛠️ Instalando VMware Tools (em Linux)

### 1. Monte o CD-ROM
```bash
sudo mkdir /mnt/cdrom
sudo mount /dev/cdrom /mnt/cdrom
```

### 2. Copie e extraia o pacote
```bash
cp /mnt/cdrom/VMwareTools-<versao>.tar.gz /tmp/
cd /tmp
tar -zxvf VMwareTools-<versao>.tar.gz
cd vmware-tools-distrib
sudo ./vmware-install.pl
```

> Requer `gcc` e headers do kernel para compilação correta

---

## 📌 Finalizando

- Reinicie a VM
- Use `umount /mnt/cdrom` para desmontar o CD
- Remova arquivos temporários:
```bash
rm /tmp/VMwareTools-<versao>.tar.gz
rm -rf /tmp/vmware-tools-distrib
```

---

## 🔗 Referências

- https://kb.vmware.com/s/article/1018414
- https://pswalia2u.medium.com/converting-vdi-to-vmdk-vmware-4369f8ad7b8f
- https://superuser.com/questions/73470/how-do-i-convert-a-virtualbox-vdi-file-to-a-vmware-vdmk
- https://forums.virtualbox.org/viewtopic.php?p=504864
