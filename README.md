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

Procedimento para aplicação do PATH.
	Faça download do PATH ou PSU
	Envie o arquivo para maquina: Pode ser utilizado o aplicativo  WinSCP.exe 
		Link para download do aplicativo https://winscp.net/eng/download.php
		Manual para utlização do WinSCP.exe http://wiki.infolink.com.br/Como_usar_o_WinSCP
	Agora você vai precisar descompactar o arquivo:
		unzip p{Nome do arquivo}.zip
		cd {Nome do arquivo}
	Validação prerequisitos:
		$ORACLE_HOME/OPatch/opatch prereq CheckConflictAgainstOHWithDetail -ph ./
	Aplicação do patch:		
		$ORACLE_HOME/OPatch/opatch apply # Pode existir a necessidade desligar a instancia, LISTENER, sqlplus e dbcontrol.
			Se a instancia apresentar necessidade shutdown completo
				sqlplus / as sysdba
					shutdown immediate;
				exit
				lsnrctl stop
				emctl stop dbconsole
			Executar novamento o comando
				$ORACLE_HOME/OPatch/opatch apply			
	Aplicação na instancia:
		sqlplus / as sysdba
			STARTUP # se a instancia foi desativada			
		exit;
		lsnrctl start # se a instancia foi desativada
		emctl start dbconsole # se a instancia foi desativada
		sqlplus / as sysdba
			@?/rdbms/admin/catbundle.sql psu apply
			@?/rdbms/admin/utlrp.sql
		exit
	Verificar se o patch foi aplicado:
		sqlplus / as sysdba
			COL ACTION_TIME FORMAT A40
			COL COMMENTS FORMAT A40
			COL VERSION FORMAT A20
			SELECT ACTION_TIME, VERSION, COMMENTS FROM DBA_REGISTRY_HISTORY;
		exit;
Procedimento finalizado.
