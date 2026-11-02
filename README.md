# NSSP_project_1    
Our project is organized in multiple files that can be find inside the folder called "notebooks".  
In this folder the files that can be find are:  
- mettere qui nomi finali file, magari togliamo il vecchio part1 ed il file che si chiama part1_NSSP_new lo chiamiamo part1_preprocessing
- poi possiamo togliere report doc e quel dataset description più altre cose che non servono più e che non devono essere valutate  

Io propongo:  
- togliere cartella .ipynb_checkpoints che contiene solo un readme vuoto  
- mantenere solo versione finale di PCA
- restare solo con:  
    - README
    - utils.py that is used in the notebooks  
    - folder "GroupAI_code" that contains:  
        - 01_preprocessing where the code relative to the structural and functional preprocessing can be find  
        - 02_GLM where the code relative to the GLM question of part 1 can be find  
        - 03_PCA where the code relative to the second part (PCA version) can be find 

## How to run the code  
In order to run the code you should upload the dataset in ____ 

RICCARDO PER FAVORE QUANDO FAI LA COSA DELLE PATH CONTROLLA CHE RINOMINANDO I FILE E FOLDER NO HO FATTO CASINO GRAZIE!


## modifiche che farei:  --> PER LUCA 
- levare "path per luca che sono pigro" da GLM code  
- inserire in GLM la versione corretta per i path come aveva proposto Riccardo  
- mettere commento "Verifica che la cartella NSSP sia condivisa nella VM" in inglese o togliere proprio se non più necessario  
- Mettere in generale i commenti di GLM in inglese (tipo "Mettiamo i noi delle variabili usati nelle cartelle successive) 
- QUESTO è giusto: ma lo commenterei così:
    Search recursively for T1w image
t1_files = glob.glob(
    os.path.join(data_dir, "**", "*T1*.nii.gz"),
    recursive=True
)  
- sistemare fmri_path
- sistemare i commenti su registration --> toglierei tutta la parte che dice "trying two different modality costs" e metti subito la parte normcorr perché è quello che abbiamo visto nella parte di preprocesisng quindi è inutile ripeterlo anche qui direi  
    - quindi magari fai solo affine registration con normcorr e poi quella non lineare con FNIRT e così alla fine ottieni quello che dicevamo essere la scelta migliore nella parte 1 del preprocessing  
- anche tutta la parte del motion correction la semplidicherei molto --> togli subito volume senza fare tutti i grafici etc --> già spiegato nella parte 1 
- quindi io scriverei: "preprocessing data as done in part 1" 

