# Modeling and rendering with boxes 

Progetto di Avanzato Thomas e Castellano Astrid

![Immagine dal progetto](C:\Users\Astrid\Documents\UNI\Interactive Graphics 3D\GITHUB_RANON\cubes-2019-avanzato-castellano\screenshots\6.png)

## Pre-requisiti

- Letto attentamente la consegna e le linee guida dettate dal docente.
- Tramite gli opportuni link consigliati, abbiamo appreso come muoverci su GitHub, abbiamo inoltre creato il gruppo per il progetto e clonato la repository.
- Prima di iniziare a programmare, abbiamo raccolto le proposte e pensato che scena ricreare.

## Goals 
In questo progetto è stata creata un'ambientazione fatta di soli cubi, che sono stati traslati, scalati e ruotati.

La consegna prevedeva di aggiungere delle animazioni che son state implementate per far ruotare e spostare i cubi fluttuanti e l'interazione con l'utente tramite i comandi da tastiera e mouse. Di creare, inoltre, un oggetto fatto interamente di cubi con il quale abbiamo ideato una scala a chiocciola con la base più grande ripetto alla cima e scalato in proporzione all'altezza e alla posizione gli scalini.

Un'altro obiettivo da raggiungere è stato quello di disegnare una heightmap in forma di immagine in scala di grigi per lo sviluppo irregolare del terreno della scena.

## Starting code

Per l'implementazione del progetto siamo partiti guardando e analizzando il codice dato dal docente il partenza. 

Abbiamo deciso di utilizzare come schema base iniziale il file "StartingCode-withLights" e poi adattarlo alla nostra scena ideata. 

Per ricreare il terreno, invece, si siamo basati sul codice "StartingCode-heightmap" che ci ha permesso, tramite l'importazione input dell'immagine in scala di grigio nel formato png da noi creata, di produrre un terreno irregolare di diverse altezze.

## Steps 

1. Abbiamo clonato il progetto di partenza della repository "Progetto" del docente.
2. Abbiamo analizzato e compreso i file di codice che ci ha fornito il docente come base di partenza e valutato come appocciarci al problema.
3. Abbiamo aggiunto alla nostra repository il nostro diario "journal.md", nel quale ogni volta in cui sono state apportate modifiche o aggiunte è stato scritto un commento con la relativa data.
4. Prima di iniziare l'implementazione, abbiamo raccolto le idee per l'ambientazione e utilizzato l'[editor](https://threejs.org/editor/) di Three.js per ricrearla andando a modificare le luci e le proprietà dei cubi. Abbiamo fatto delle ricerche, inoltre, per la valutazione della fattibilità su codice già pre-esistente online.
5. Dopo aver scelto quale idea implementare, abbiamo iniziato il lavoro creando n cubi fluttuanti che ruotano attorno ad un perno, detto "pivot". Abbiamo inoltre iniziato ad implementare i materiali da applicare agli oggetti volanti e le luci alla scena e abbiamo aggiunto un effetto "foschia" alla scena tramite la funzione di Three.js "Fog()".
6. Prima dell'aggiunta di altri oggetti nella scena, sono state aggiunte le interazioni con l'utente e sono stati testati i comandi. 
   Per l'implementazione del codice, abbiamo cercato e consultato la dispensa della [documentazione online di threejs](<https://threejs.org/docs/index.html#api/en/core/EventDispatcher>).
7. Successivamente abbiamo creato il terreno utilizzando il codice di partenza "StartingCode-heightmap". 
   Abbiamo creato tramite l'utilizzo del programma Photoshop, un immagine (30x30) a scala di grigio in png da passare in input al codice [vedi il sottocapitolo "Terreno"].
   Sono state implementate anche le direttive per il meccanismo di limitazione della mappa, tramite il quale l'utente utilizzando i tasti non può uscire dalla planimetria.
8. In seguito, abbiamo creato un oggetto fatto di cubi. 
   In centro alla scena abbiamo disegnato una scala avviluppata su se stessa composta solo da scalini. 
   Ogni scalino in base alla sua posizione (altezza rispetto alla scena) è scalato proporzionalmente in modo da creare un effetto ottico.
9. In cima alla scala sono stati creati, un cubo fermo in wireframe composto da più cubi ruotati e una serie di piccoli cubi (sempre in wireframe) che ruotano attorno ad esso.
10. Infine, come ultima miglioria è stato implementato il suono per rendere l'atmosfera più misteriosa-magica.

### Materiali

I materiali utilizzati in questo progetto sono:

- [MeshPhysicalMaterial](<http://www.inf.u-szeged.hu/~tanacs/threejs/docs/#api/en/materials/MeshPhysicalMaterial>)
- [MeshBasicMaterial](<http://www.inf.u-szeged.hu/~tanacs/threejs/docs/#api/en/materials/MeshBasicMaterial>)
- [MeshPhongMaterial](<http://www.inf.u-szeged.hu/~tanacs/threejs/docs/#api/en/materials/MeshPhongMaterial>)

#### Cubi

I materiali per i cubi fluttuanti sono stati implementati nella variabile "boxMaterial". 
Essi sono delle MeshPhysicalMaterial con le proprietà:

- Colore = 0x0000ff

- Metallo = 0.5

- Rugosità = 0.15

- Trasparente con opacità 0.15

- Riempimento FrontSide

- Intensità della texture = 5

- PremultipliedAlpha = true

- Texture = ![crystalTexture](C:\Users\Astrid\Documents\UNI\Interactive Graphics 3D\GITHUB_RANON\cubes-2019-avanzato-castellano\textures\crystal.JPG)


#### Terreno

Il materiale utilizzato per il terreno "groundMaterial" è una MeshPhysicalMaterial con le seguenti proprietà:

- Riflettività = 1
- Colore =  0xbbaaf0
- Metallo = 1
- Rugosità = 0.5 
- Trasparenza con opacità di 0.9
- Riempimento FrontSide
- Texture = ![groundTexture](C:\Users\Astrid\Documents\UNI\Interactive Graphics 3D\GITHUB_RANON\cubes-2019-avanzato-castellano\textures\rock.jpg)

#### Scala

Anche le scale sono dello stesso tipo di materiale dei, ovvero MeshPhysicalMaterial in modo da poterci salire.

Le sue proprietà a differenza dei cubi sono:

- Niente trasparenza

- Metallo = 0

- Texture = ![crystalTexture](C:\Users\Astrid\Documents\UNI\Interactive Graphics 3D\GITHUB_RANON\cubes-2019-avanzato-castellano\textures\crystal.JPG)

#### Globo

?????????????

#### Anello 

?????????????????

### Luci

Per il nostro ambiente, abbiamo utilizzato:

- una "[HemisphereLight](<https://threejs.org/docs/index.html#api/en/lights/HemisphereLight>)", chiamata "light" per l'illuminazione posizionata in centro alla scena nelle coordinate (0, 1, 0) con attributi: 

  - 0xeeeeff: colore del cielo
  - 0x777788: colore del terreno
  - 0.1: valore dell'intensità della luce sprigionata

- quattro "[SpotLight](<https://threejs.org/docs/index.html#api/en/lights/SpotLight>)", chiamati "spotLight1, spotLight2, spotLight3, spotLight4" per ricreare un illuminazione emessa come fascio di luce da una singola direzione.
  Hanno tutte e quattro l'intensità pari al valore 2.
  - spotLight1 è posta nella posizione con coordinate (100, 30, -10) che sprigina il colore 0x333333. 
    Ha inoltre la proprietà di emettere le ombre con i relativi settaggi della camera:
    - Aspetto della mapSize con le relative ombre in altezza e larghezza:
      spotLight1.shadow.mapSize.width = 1024;
      spotLight1.shadow.mapSize.height = 1024;
    - Piano di ritaglio vicino alla camera:
      spotLight1.shadow.camera.near = 500;
    - Piano di ritaglio lontano dalla camera: 
      spotLight1.shadow.camera.far = 4000;
    - Settaggio dell'angolo:
      spotLight1.shadow.camera.fov = 30;
  - spotLight2 è posta nelle coordinate (-160, 80, -20) con corrispondenza opposta troviamo spotLight3 con coordinate (160, 80, 20) e infine spotLight4 in coordinate (-160, 80, 20). 
    Queste tre luci emettono la tonalità 0xd966ff.


### Terreno

Per la creazione del terreno è stato utilizzato il codice di partenza dato dal docente "StartingCode-heightmap", in particolar modo il metodo "getHeightData()" al quale vengono passati in input l'immagine heightmap e la scala e ritorna in output un array "data" contenente le altezze.

Per l'immagine heightmap abbiamo creato è un immagine png 30x30 nella scala di grigio. 

![heightmap_img](C:\Users\Astrid\Documents\UNI\Interactive Graphics 3D\GITHUB_RANON\cubes-2019-avanzato-castellano\textures\heightmap.png)

Il terreno è stato settato nel metodo "setGound()", il quale richiama la funzione appena descritta passandogli l'immagine (heightmap.png) e la scalatura (0.1).

### Animazioni



## Aggiunte extra

Come aggiunta finale, si è voluto inserire una traccia audio. 

Per la comprensione dell'utilizzo ci siamo basati sulla documentazione online di three.js sulle tecniche di audio: [AudioLoader](<https://threejs.org/docs/index.html#api/en/loaders/AudioLoader>) e [AudioListener](<https://threejs.org/docs/index.html#api/en/audio/AudioListener>)

## Supporto

Per l'implementazione del codice, ci siamo appoggiati alla guida della [documentazione di three.js](<https://threejs.org/docs/index.html#manual/en/introduction/Creating-a-scene>); all'[three.js editor](https://threejs.org/editor/) per l'implementazione primitiva degli oggetti come prova e studio di fattibilità; al codice di partenza e suggerimenti dati dal docente e al supporto di internet per il reperimento delle immagini, del suono e delle informazioni su errori o chiarimenti del codice.

