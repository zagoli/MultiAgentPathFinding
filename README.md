# MultiAgentPathFinding
Progetto per l'esame di fondamenti di intelligenza artificiale, A.A. 2021/2022.
http://idm-lab.org/project-p/project.html  
## Space time A*
L'implementazione corrente di A* cerca un percorso solo nelle celle, tralasciando 
di considerare la posizione di un agente ad un determinato timestamp.  
Dobbiamo quindi modificare l'algoritmo in modo che cerchi un percorso nell'insieme di 
coppie (posizione, timestamp), e che consideri i constraint.
- Task 1.1: modificato A* in modo che i nodi generati ed esplorati mantengano un timestamp aggiornato.
