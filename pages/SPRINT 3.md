- ### ANALISI DEL PROBLEMA
	- la command console per come viene concepita nello step 2 non è riusabile in ambiente remoto in quanto
		- la console deve comunicare delle informazioni via rete, non è piu possibile effettuare una procedure call
		- la command console deve essere indipendente dal protocollo di comunicazione utilizzato
			- necessario creare un layer di astrazione
	- appl1
		- per evitare di reimplementare la logica applicativa si decide di inglobare il POJO appl1Core in un adapter in grado di ricevere comandi dalla command console
		- l'adapter deve essere indipendente dal protocollo di comunicazione utilizzato
	- #### supporto di comunicazione
		- necessario sviluppare un astrazione al supporto di comunicazione
		- sia per la command console che per appl1 si può sfruttare il pattern strategy per il supporto di comunicazione
			- ![Strategy pattern - Wikipedia](data:image/png;base64,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)
			- interfaccia per le funzionalità necessarie al supporto di comunicazione client
				- `sendCommand(String cmd);`
				- `connectToServer(String address);`
			- definire interfaccia per il supporto di comunicazione lato server
				- possibile sfruttare il pattern observer
					- il componente wrapper Appl1 diventa observer del supporto di comunicazione
					- il supporto di comunicazione alla ricezione di un comando lo interpreta e notifica il componente appl1
				- interfaccia supporto di comunicazione lato server deve essere un oggetto observable
				-
				-
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
	- le due fasi ((6419b3e0-6e09-4ab1-afbf-01aa506ecb44)) e ((6419b2af-7f44-44e9-a934-aa788055c0bc)) possono essere sviluppate in parallelo da team indipendenti che hanno come vincolo il linguaggio definito in ((6419b507-442e-4455-8a2e-b521439e7fa5))
	-