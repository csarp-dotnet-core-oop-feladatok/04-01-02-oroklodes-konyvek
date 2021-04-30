# 04-01-02-oroklodes-konyvek
## Öröklődés számítással és kivétel kezeléssel
A feladata a könyvkereskedéssel foglalkozó „Könyv Nagykereskedés”. számára fejlesztendő program adatmodelljének kifejlesztése és tesztelése. A könyvkereskedés papír könyveket vesz és elad. Ezen kívül a weboldalukon elektronikus könyvek érhetők el, amelyeket le lehet tölteni.  
A projektvezetője a következő modell alapján kéri a fejlesztést:  

![image](https://user-images.githubusercontent.com/6060514/116676160-ee250180-a9a6-11eb-8842-a185c7e6214c.png)

Elvárások:  
1.  
a)  
A Konyv osztály ToString metódusa pl. a következő kimenetet adja:  

Könyv szerzője:Andrew Troelsen  
Könyv címe:Pro C# 7  
Könyv oldalszama:155  

2.  
Az EKonyv Letolt() metódusa a letöltésszámot növeli egyel. A letöltésszám kezdeti értéke nulla.  
Az EKönyv ToString() metódusa pl. a következő kimenetet adja:  
```
Könyv szerzője:Reiter István  
Könyv címe:C# programozás lépésről lépésre  
Könyv oldalszama:340  
Könyv letöltésszám:3  
```
3.  
a)  
A Papír könyv Elad() metódusa a készletet növeli a megadott mennyiséggel. Az Elad() metódusa a készletet csökkenti a megadott mennyiséggel.  
b)  
Az Vesz() metódus a MennyisegNegativKivetel kivételt dobja!  
Az Elad() metódus a MennyisegNegativKivetel és EladottMennyisegNagyobbKeszletnelKivetel kivételt dobja.  

Pl.  
```
-10 mennyiségű könyvet nem lehet sem eladni, sem venni.  
```
```
50 könyv van a készleten,100 könyvet így nem lehet eladni.  
```
c)  
A PapírKönyv ToString metódusa a következő kimenetet adja:  
```
Könyv szerzője:Andrew Troelsen  
Könyv címe:Pro C# 7  
Könyv oldalszama:155  
Könyv készlet:50  
```
Teszt kód
```
            PapirKonyv k1 = new PapirKonyv("Andrew Troelsen", "Pro C# 7",155,100);
            PapirKonyv k2 = new PapirKonyv("Matthew MacDonald", "Pro WPF in C# 2008",110,25);
            EKonyv ek = new EKonyv("Reiter István", "C# programozás lépésről lépésre",340);
            Console.WriteLine(k1);
            k1.Elad(50);
            try
            {
                k1.Vesz(-10);
            } catch(MennyisegNegativKivetel e)
            {
                Console.WriteLine(e.Message);
            }
            try
            {
                k1.Elad(-20);
            }
            catch (MennyisegNegativKivetel e)
            {
                Console.WriteLine(e.Message);
            }
            
            try
            {
                k1.Elad(100);
            }
            catch (EladottMennyisegNagyobbKeszletnelKivetel e)
            {
                Console.WriteLine(e.Message);
            }
            ek.Letolt();
            ek.Letolt();
            ek.Letolt();
            Console.WriteLine(k1);
            Console.WriteLine(k2);
            Console.WriteLine(ek);
            Console.ReadKey();
            
   ```



