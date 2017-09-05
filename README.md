# aplication_patch_oracle
How to application patch in Oracle 11G

Aplicando um Critical Patch Update (CPU) no Banco de Dados Oracle 11c

Antes de iniciar a instalação do PSU, é recomendado atualizar também o OPATCH, que está disponível através do Patch 6880880(Https://updates.oracle.com/download/6880880.html). 

Procedimento para instalação do OPATCH:

	Faça download da versão atual do OPATCH no link: Https://updates.oracle.com/download/6880880.html
	Envie o arquivo para maquina: Pode ser utilizado o aplicativo  WinSCP.exe 
		Link para download do aplicativo https://winscp.net/eng/download.php
		Manual para utlização do WinSCP.exe http://wiki.infolink.com.br/Como_usar_o_WinSCP
	Agora você vai precisar descompactar o arquivo:
		unzip p{Nome do arquivo}.zip
	Atualizando a pasta:
		mv $ORACLE_HOME/OPatch $ORACLE_HOME/OPatch1  #backup do opatch antigo
		mv OPatch  $ORACLE_HOME/OPatch
	Valido a nova versão:
		$ORACLE_HOME/OPatch/opatch lsinventory
