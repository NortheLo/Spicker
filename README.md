# Spicker
Kleiner Spickzettel

LVM: externes LVM-Volume scannen und mounten
# vgscan
# vgchange -a y
# mount /dev/<VolGroup00>/xxx /mnt/yyy
—
Sun Java Plugin in Firefox aktivieren (64Bit)
# jre rpm von Sun downloaden und installieren
# cd /usr/lib64/mozilla/plugins
# ln -s /usr/java/default/lib/amd64/libnpjp2.so .
—
Postfix postcat & postsuper Befehle:
# postcat -q mailid (Mailinhalt ansehen)
# postsuper -d mailid  (löschen)
# postsuper -h mailid – (halten)
# postsuper -H mailid (wieder loslassen)
# postusper -r mailid (wieder einstellen – u.U. mit neuen Parametern)
# postsuper -p (alte temp Dateien purgen)
# postsuper -s (System check)

Fedora und NVIDIA (Nouveau deaktivieren)
# yum localinstall –nogpgcheck http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-stable.noarch.rpm
# yum localinstall –nogpgcheck http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-stable.noarch.rpm

# yum install kmod-nvidia xorg-x11-drv-nvidia-libs
# mv /boot/initramfs-$(uname -r).img /boot/initramfs-$(uname -r)-nouveau.img
# dracut /boot/initramfs-$(uname -r).img $(uname -r)

Windows 7, Explorer / Netzwerkumgebung: den Beschreibungstext der Computer wieder anzeigen
%systemroot%\explorer.exe /n,::{208D2C60-3AEA-1069-A2D7-08002B30309D}

Mit netcat und dd über das Netzwerk kopieren
Server 2 hört auf TCP 12345:
Server2# nc -l -p 12345 | dd of=/dev/sda
Server2# nc -l -p 12345 | dd of=/dev/sda1
Server2# nc -l -p 12345 | dd of=image.of.sda1.img

Server 1 schickt die Platte/Partition/Datei zum Server 2
Server1# dd if=/dev/sda  | nc server2 12345
Server1# dd if=/dev/sda1 | nc server2 12345
Server1# cat ./datei.iso | nc server2 12334

– oder mittels ssh Port Forwarding:
[server2]# ssh -l remoteuser -L 12345:localhost:12345 server1

Server1# dd if=/dev/sda  | nc localhost 12345
Server1# dd if=/dev/sda1 | nc localhost 12345
Server1# cat ./datei.iso | nc localhost 12334

-das gleiche Prinzip mit ntfsclone:
Server2 #netcat -l -p 1234 | ntfsclone -r -O /dev/sda1 –
Server1#ntfsclone -s -o – /dev/sda1 | netcat ZielIP 1234

HP Proliant mit integriertem RAID Controller (slot=0)
Bsp: Erzeugt aus zwei hinzugefügten Platten ein neues Array (RAID1). Es gibt keine weiteren Platten, die nicht zugeordnet sind.

#hpacucli
==> ctrl slot=0 show config
==> ctrl slot=0 create type=ld drives=allunassigned raid=1
==> ctrl slot=0 show config
==> quit

weitere Bsp
==> ctrl slot=0 create type=ld drives=1:1,1:2,1:3,1:5 raid=5
==> ctrl slot=0 create type=ld drives=1:1,1:2 raid=1
