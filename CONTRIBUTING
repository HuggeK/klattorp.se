Hej och välkommen till instruktioner hur du hjälper till att lägga till ett nytt album på hemsidan.

Alla bilder är tillgänliga i källkvalité genom att ladda ner individuella kort på hemsidan eller alla genom [https://klattorp.se/historia.zip](https://klattorp.se/historia.zip). Vi skalar sedan ner kvalitén på alla bilder på hemsidan 50% med hjälp av [Hugos inbyggda stöd för skalning](https://gohugo.io/content-management/image-processing/) för att det inte ska gå åt så mycket mobildata när gemene bybor går in på hemsidan. Om nu bilder skulle skänkas till samlingen som inte har lika stor upplösning på bilderna kommer dessa bli skalade 50% vilket kommer resultera i dåliga kvalité på bilder.

&nbsp;

För de bilderna som är inskannade är minimumkraven följande: 
* **Upplösning 600 dpi.**

&nbsp;

Varje bild på hemsidan har metadata, där en beskrivning av bilden finns. Denna beskrivning hänger med om man laddar ner bilden genom nerladdningsknappen eller laddar ner alla bilder på [https://klattorp.se/historia.zip](https://klattorp.se/historia.zip). Denna beskrivning används också till skärmläsare genom alt-atributen för att webben ska vara mer tillgänglig för synnedsatta. 

Det finns många verktyg för att redigera metadata, det går tex att använda Photoshop, Windows Explorer/Utforskaren eller gratisverktyget exiftool. [exiftool](https://github.com/exiftool/exiftool) (https://exiftool.org/) är ett verktyg för att genom terminalen redigera metadata till filer. För att lägga till en bildtext genom Windows utforskaren är det fälten ``Titel`` och ``Ämne`` (Eng. ``Title`` och ``Subject``) som ska fyllas i. De hittar du om du högerklickar på filen och klickar på ``Egenskaper>Detaljer``.

> * Om ni ska bidra med bilder ser jag gärna att ni själva fyller i metadata i filerna då detta gör det mycket enklare för mig att bygga hemsidan, och ladda upp de nya bilderna. 
> 
> * Om nu inte du kan redigera bilderna ser jag gärna att bildtexter skickas in som datorskriven text, *inte* bilder på skrift på papper då det innebär merjobb för mig för att transkribrera


Alla bilder i ett album namnges enligt följande struktur för att de ska komma i ordning på hemsidan: 
* *A-Z*.jpg, Z *A-Z*.jpg
*Se struktur i [https://klattorp.se/historia.zip](https://klattorp.se/historia.zip)*


### Arbeta med bilders metadata: 
Bra hemsida för att se metadata strukturerat: https://getpmd.iptc.org/


<details>
<summary> Bra exiftool kommandon: </summary>

```
./exiftool "C:/{Sökväg till filen/mappen}"
```


Sätt licens / *Web Statement of Rights* till CC BY-NC 4.0:
```
./exiftool -r -xmp-xmprights:WebStatement='https://creativecommons.org/licenses/by-nc/4.0/' "C:\Users\hugok\Downloads\Beskärda foton till hemsidan" -overwrite_original
```
där ``-r`` är rekursivt genom alla mappar.
``-overwrite_original`` tar bort de kopiorna som exiftool skapar.
</details>