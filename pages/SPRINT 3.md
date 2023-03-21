- ### ANALISI DEL PROBLEMA
	- la command console per come viene concepita nello step 2 non è replicabile in ambiente remoto in quanto
		- la console deve comunicare delle informazioni via rete, non è piu possibile effettuare una procedure call
		- la command console deve essere indipendente dal protocollo di comunicazione utilizzato
			- necessario creare un layer di astrazione
	- appl1
		- per evitare di reimplementare la logica applicativa si decide di inglobare il POJO appl1Core in un adapter in grado di ricevere comandi dalla command console
		- l'adapter deve essere indipendente dal protocollo di comunicazione utilizzato
	- sia per la command console che per appl1 si può sfruttare il pattern strategy per il supporto di comunicazione
		- definire interfaccia per le funzionalità necessarie al supporto di comunicazione
			- `sendCommand(String cmd);`
			- `connectToServer(String address);`
		- definire interfaccia per il supporto di comunicazione lato server
			- possibile sfruttare il pattern observer
				- il componente wrapper Appl1 diventa observer del supporto di comunicazione
				- il supporto di comunicazione alla ricezione di un comando lo interpreta e notifica il componente appl1
		- configurazione mediante file
			- sfruttare pattern factory per fornire alle classi la corretta implementazione
			- necessarie due classi factory
		- linguaggio di comunicazione
		  id:: 6419b507-442e-4455-8a2e-b521439e7fa5
			- necessario definire in maniera formale il linguaggio di comunicazione tra console e componente Appl1
			- la comunicazione avviene tramite stringhe in formato json
			- `{command:CMD}`
			- `CMD= start|stop|resume`
			-
- ### PIANO DI LAVORO
  :LOGBOOK:
  CLOCK: [2023-03-21 Tue 14:36:31]
  :END:
	- #### command console (client)
	  id:: 6419b2af-7f44-44e9-a934-aa788055c0bc
		- sviluppo interfaccia supporto di comunicazione client
		- sviluppo di implementazione pilota su protocollo di esempio (HTTP)
		- sviluppo di factory per interfaccia di comunicazione client
		- sviluppo di classe di integrazione per la comunicazione della command console
	- #### componente Appl1
	  id:: 6419b3e0-6e09-4ab1-afbf-01aa506ecb44
		- sviluppo interfaccia per supporto di comunicazione server
		- sviluppo di implementazione pilota su protocollo di esempio (HTTP)
		- sviluppo di factory per interfaccia di comunicazione server
		- sviluppo del componente appl1 come observer del supporto di comunicazione
	- le due fasi ((6419b3e0-6e09-4ab1-afbf-01aa506ecb44)) e ((6419b2af-7f44-44e9-a934-aa788055c0bc)) possono essere sviluppate in parallelo da team indipendenti che hanno come vincolo il linguaggio definito in ((6419b507-442e-4455-8a2e-b521439e7fa5))
	-