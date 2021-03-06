Octavian Torcea 324CA

* Programul incepe prin initializarea bazei de date:
	* pentru `GenreDatabase`:
		* se creeaza un hashmap
		* keys -> genurile
		* valori -> numarul de viewuri pentru fiecare gen (la inceput
			toate sunt 0, se vor actualiza pe parcurs)
	* pentru `VideoDatabase`:
		* se creeaza un linkedhashmap (pentru unele actiuni este necesara
			pastrarea ordinii in care au fost adaugate videourile)
		* keys -> titlurile videourilor
		* valori -> obiectul video
		* in aceeasi baza de date se retin si filmele si serialele
		* se creeaza si se pun mai intai toate obiectele "movie", apoi "show"	
	* pentru `UserDatabase`:
		* se creeaza un hashmap
		* keys -> username
		* valori -> obiectul user
		* pe langa informatiile specifice unui user, odata cu crearea unui
			obiect se citeste lista sa de filme favorite si filme vizionate si
			se actualizeaza baza de date de videouri (creste numarul de
			vizionari si de cate ori un video a fost adaugat intr-o lista de
			favorite)
			
	* pentru `ActorDatabase`:
		* se creeaza un hashmap
		* keys -> numele
		* valori -> obiectul actor
		* la crearea unui obiect actor se calculeaza si totalul premiilor
			castigate
			
	* pentru `ActionDatabase`: un simplu arraylist de actiuni (cu toate datele
		primite de la input)
		
### !!!metodele folosite sunt descrise mult mai detaliat in comentariile din cod!!!
		
* Se executa apoi actiunile in functie de tipul acesteia (command, query sau
recommendation):
	* command:
		* favorite -> adauga videoul in lista de favorite a unui user
		* view -> userul "vizioneaza" un video, incrementand numarul de
			vizionari a videoului si a genurilor	
		* rating -> userul ofera un rating videoului; dupa fiecare rating se
			actualizeaza nota medie a filmului		
	* query:
		* pentru actori (metodele se gasesc in ActorDatabase):
			* average -> intoarce o lista de nume de actori ordonati in functie
				de media tuturor filmelor in care au jucat; la fiecare apel de
				metoda se calculeaza iar fiecare medie pentru toti actorii
			* awards -> intoarce o lista de nume de actori ce au primit toate
			premiile date ca filtru, in ordinea numarului de premii totale
			obtinute
			* filter description -> intoarce o lista de nume de actori ce au in
				descrierea carierei toate cuvintele date ca filtru, sortata in
				ordine alfabetica
		* pentru videouri (metodele se gasesc in VideoDatabase):
			* rating -> intoarce o lista de titluri de filme sortate dupa rating
			* favorite -> intoarce o lista de titluri de filme sortate in
				functie de cate ori au fost adaugate in lista de favorite a
				unui user	
			* longest -> intoarce o lista de titluri de filme sortate dupa
				duarat lor	
			* most viewes -> intoarce o lista de titluri de filme sortate dupa
				numarul de vizionari
		* pentru useri:
			-> intoarce o lista de useri sortati in functie de numarul de
				ratinguri acordare		
	* recommend: pentru fiecare metoda se itereaza prin baza de date pana se
		gaseste videoul/videourile ce respecta cerinta; pentru recomandarile ce
		necesita ca utilizatorul sa fie premium, aceasta verificare se face la
		inceputul actiunii
		
De fapt, fiecare actiune intoarce un string ce reprezinta mesajul ce trebuie pus
in JSONArray, dar contin cate o metoda ce creeaza o lista (in functie de
cerinta) ce va fi concatenata cu measjul specific fiecarei actiuni.
