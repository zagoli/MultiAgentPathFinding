# MultiAgentPathFinding
Progetto per l'esame di fondamenti di intelligenza artificiale, A.A. 2021/2022.
http://idm-lab.org/project-p/project.html  
## Space time A*
L'implementazione corrente di A* cerca un percorso solo nelle celle, tralasciando 
di considerare la posizione di un agente ad un determinato timestamp.  
Dobbiamo quindi modificare l'algoritmo in modo che cerchi un percorso nell'insieme di 
coppie (posizione, timestamp), e che consideri i constraint.
#### Task 1.1 
Modificato A* in modo che i nodi generati ed esplorati mantengano
un timestamp aggiornato.
#### Task 1.2
L'insieme di constraint dati in input viene filtrato per agente e
indicizzato per timestamp nella funzione build_constraint_table.  
Implementata la funzione is_constrained, che dati i parametri di un 
nodo e del parent, controlla se viene violato un constraint presente
nella tabella costruita sopra.
Per ora gli unici tipi di constraint considerati sono vertex constraints.
#### Task 1.3
