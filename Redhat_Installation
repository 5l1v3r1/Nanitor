#!/bin/sh
#Auther AbedAlqaderSwedan From CYSTACK 
#Usage ./script 192.168.1.1 nanitor.bank.com
#Please make sure to put the signup-key.txt in the current (Redhat_Install_Nanitor) . 
#Please make sure to put the ca root in the current folder and make sure the file name is CA-Nanitor.cer
#Note Nanitor agent 64/32 , CA root , and my script in the same folder. 
#cp * /root

ip=$1
domain=$2
if [ $# -eq 0 ]
  then
    echo "Usage $0 192.168.1.1 nanitor.exampleBank.com"
else
	MACHINE_TYPE=`uname -m`
	if [ ${MACHINE_TYPE} == 'x86_64' ]; then
	  rpm -ivh nanitor-agent-1.5.0.4825-1325.x86_64.rpm #Install Nanitor agent 64 bit.
	else
	  rpm -ivh nanitor-agent-1.5.0.4825-1325.i386.rpm   #Install Nanitor agent 32 bit.
	fi

	rpm -ivh ca-certificates-2015.2.6-65.0.1.el6_7.noarch.rpm  #Install CA-certificates packege  .
	echo "$ip $domain" >> /etc/hosts 
	sleep 3
	cp CA-Nanitor.cer /etc/pki/ca-trust/source/anchors
	update-ca-trust
	sleep 1
	update-ca-trust force-enable /etc/pki/ca-trust/source/anchors/CA-Nanitor.cer
	sleep 2
	/usr/lib/nanitor-agent/bin/nanitor-agent signup --keyfile=signup-key.txt
	sleep 2 
	/etc/init.d/nanitor-agent start
fi 
