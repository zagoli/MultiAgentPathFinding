# MultiAgentPathFinding
**Jacopo Zagoli**\
Progetto per l'esame di fondamenti di intelligenza artificiale, *A.A. 2021/2022.*\
http://idm-lab.org/project-p/project.html  

## Space-time A*
L'implementazione corrente di A* cerca un percorso solo nello spazio, non considerando
il tempo.  
Dobbiamo quindi modificare l'algoritmo in modo che cerchi un percorso nell'insieme di 
coppie (posizione, timestamp), e che consideri i vincoli.
#### Task 1.1 
Modificato A* in modo che i nodi generati ed esplorati mantengano
un timestamp aggiornato. Inoltre ora viene generato un nodo in cui l'agente rimane nella
posizione corrente.
#### Task 1.2
L'insieme di vincoli dati in ingresso viene filtrato per agente e
indicizzato per timestamp nella funzione build_constraint_table.  
Implementata la funzione is_constrained, che dati i parametri di un 
nodo e del parent, controlla se viene violato un vincolo presente
nella tabella costruita sopra.
Per ora gli unici tipi di vincoli considerati sono vertex constraints.
#### Task 1.3
Aggiunto il support per gli edge constraint: l'unica funzione modificata
è is_constrained, che data la posizione corrente, futura e il timestamp
verifica se il nodo viola almeno uno dei due tipi di vincoli.
#### Task 1.4
Viene aggiunto un controllo per verificare se il nodo raggiunto è di goal: 
ora non basta raggiungere la posizione finale, è anche necessario che la posizione
finale raggiunta non compaia in nessun vincolo dal timestamp corrente in poi.
Per verificarlo viene creata la funzione is_goal_constrained, che verifica tutti i
vincoli dei timestamp futuri.

## Prioritized Planning
Lo scopo dei task seguenti è quello di modificare il codice corrente in modo
da implementare correttamente l'algoritmo di Prioritized Planning.
### Task 2.1
Grazie all'algoritmo space-time A* implementato prima, possiamo trovare un percorso
per ogni agente. In questo task, partendo da un percorso, dobbiamo generare tutti i 
vertex constraint richiesti: iteriamo quindi il percorso e per ogni locazione aggiungiamo 
a tutti gli agenti (tranne quello corrente) un vincolo che impedisce di essere in 
quella locazione in quel momento.
### Task 2.2
Piccola modifica che aggiunge, per ogni coppia locazione-momento, un edge constraint:
per fare questo, è necessario ottenere anche la prossima locazione nel percorso a ogni iterazione
(tranne l'ultima).
### *Opzionale:* Task 2.3
Il codice finora implementato non rileva collisioni fra agenti se un agente ha già raggiunto
il suo obiettivo: questo perchè viene aggiunto un vincolo per ogni locazione presente
nel percorso, ma finito il percorso, non vengono aggiunti altri vincoli.  
Per ovviare a questo problema, ho modificato la struttura dei vincoli, aggiungendo un campo
*'final'*. Un vincolo con il campo final impostato a True è chiamato *final constraint*, 
e indica che nessun agente potrà trovarsi nella locazione indicata dal vincolo in un
momento successivo a quello indicato nel vincolo.  
Il codice è quindi così modificato:
- quando itero un percorso per generare un vincolo, controllo se sono nella posizione finale
(l'ultima del percorso). Se sì, imposto il campo final a True.
- nell'algoritmo space-tima A*, quando controllo se un nodo generato è soggetto a vincoli,
ora controllo anche se in qualche momento precedente la posizione corrente compare in un final constraint.

## Conflict-Based Search
