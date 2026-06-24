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
> * Om nu inte du kan redigera bilderna ser jag gärna att bildtexter skickas in som datorskriven text, *inte* bilder på skrift på papper då det innebär merjobb för mig för att transkribrera.


Alla bilder i ett album namnges enligt följande struktur för att de ska komma i ordning på hemsidan: 
* [A-Z].jpg, Z[A-Z].jpg, ZZ[A-Z] e.t.c. Se struktur i [https://klattorp.se/historia.zip](https://klattorp.se/historia.zip)*


<details>
<summary> Bra exiftool kommandon: </summary>


### Arbeta med bilders metadata: 
Bra hemsida för att se metadata strukturerat: https://getpmd.iptc.org/


```
./exiftool "C:/{Sökväg till filen/mappen}"
```

#####  ExifTool Google Image IPTC metadata Tags:

``-r`` är rekursivt genom alla mappar.
``-overwrite_original`` tar bort de kopiorna som exiftool skapar.


[Copyright Notice:](https://iptc.org/std/photometadata/specification/IPTC-PhotoMetadata#copyright-notice)
```
./exiftool -r -xmp-dc:rights='Copyright © Klättorps Byalag & XXXX' "C:\XXXXX" -overwrite_original

```

[Web Statement of Rights:](https://www.iptc.org/std/photometadata/specification/IPTC-PhotoMetadata#web-statement-of-rights) till CC BY-NC 4.0:
```
./exiftool -r -xmp-xmprights:WebStatement='https://creativecommons.org/licenses/by-nc/4.0/' "C:\PATH" -overwrite_original
```


[Licensor URL:](https://ns.useplus.org/LDF/ldf-XMPSpecification#LicensorURL)
```
./exiftool -r -xmp:LicensorURL='https://klattorp.se' "C:\XXXX" -overwrite_original
```


[Credit Line:](https://iptc.org/std/photometadata/specification/IPTC-PhotoMetadata#credit-line)
```
./exiftool -r -xmp-photoshop:Credit='Klättorps Byalag' "C:\XXXXX" -overwrite_original
```


[Description Writer:](https://iptc.org/std/photometadata/specification/IPTC-PhotoMetadata#description-writer)
```
./exiftool -r -xmp-photoshop:CaptionWriter='Person, Person' "C:\XXXXX" -overwrite_original
```


[Creator:](https://iptc.org/std/photometadata/specification/IPTC-PhotoMetadata#creator)
```
./exiftool -r -xmp-dc:Creator='CREATOR NAME "C:\XXXXX" -overwrite_original
```

&nbsp;

Sammansatt:
```
./exiftool -r -xmp-dc:rights='Copyright © Klättorps Byalag & XXXX' -xmp:LicensorURL='https://klattorp.se' -xmp-photoshop:Credit='Klättorps Byalag' -xmp-photoshop:CaptionWriter='Person, Person' -xmp-xmprights:WebStatement='[C:\XXXXX](https://creativecommons.org/licenses/by-nc/4.0/)" "C:\XXXXX" -overwrite_original
```

Kopiera metadata till [A-Z]*\_filter\_*.jpg:
```
./exiftool -tagsFromFile -if -p "$directory/$filename" -ext jpg -all:all './public/bilder_sent_1800-tal_tidigt_1900-tal/${filename:tr/ s/ .jpg//}*_filter_*.jpg' DIR > "./public/bilder_sent_1800-tal_tidigt_1900-tal"
```

Hur gör jag så att jag kan referera till nuvarande fil när programmet går igenom den i srcfile? dvs $filename ger t.e.x. ZZ.jpg. hur får jag bort .jpg ifrån filnamnet för att kunna lägga in wildcard söken på \*\_filter\_\*?
Se https://exiftool.org/exiftool_pod.html#Advanced-formatting-feature.

Perl Expression: https://stackoverflow.com/a/6863515/18008722

Stack Overflow lösning där det kopierars _compressed filer. https://stackoverflow.com/a/67521876/18008722
 * Problemet men den lösningen är att Hugo spottar ut två filer, en som är 70 karaktärer utanpå filnamnet och en som är 69. 
   * Använda flera if-satser?

```
exiftool -if "$Filename=~/_compressed/i" -r -TagsFromFile %d%-.11f.%e -All:All C:\photo
```

Då regexen är [A-Z] får man köra det 5 ggr med -execute men ändra till Z[A-Z] e.t.c.

* TODO: Fixa [A-Z] regex på srcfile.
</details>
&nbsp;

## Bygga hemsidan lokalt

Hemsidan byggs med [Hugo](https://gohugo.io/). Det enklaste sättet är att
installera **Hugo Extended** direkt — då behöver du varken Go eller en
C-kompilator. (Hugo självt finns också som git-submodul under `Hugo/bin/hugo`
om du hellre vill bygga binären från källkod, se *Alternativ* längst ned. Själva
`hugo.exe` checkas inte längre in i repot; tidigare låg en 88 MB stor sådan här.)

### 1. Installera Hugo **Extended**

Temat (`gallery`) använder SCSS/Sass, så du **måste** ha **Extended-utgåvan** av
Hugo — den vanliga (icke-extended) räcker inte. Kontrollera efteråt att versionen
innehåller ordet `extended`:

```bash
hugo version
# t.ex. hugo v0.163.3+extended windows/amd64 ...
```

Temat kräver minst **Hugo Extended 0.121.2**; senast verifierad med **0.163.3**.

Installation per operativsystem:

```bash
# Windows (winget)
winget install Hugo.Hugo.Extended

# Windows (Chocolatey)
choco install hugo-extended

# macOS / Linux (Homebrew) – Homebrews "hugo" är redan Extended
brew install hugo

# Linux (Debian/Ubuntu via apt – kontrollera att paketet är extended)
sudo apt install hugo
```

Saknar din pakethanterare en Extended-utgåva kan du ladda ner en färdig
`hugo_extended_…`-binär från <https://github.com/gohugoio/hugo/releases> eller
följa <https://gohugo.io/installation/>.

### 2. Hämta temat (submodul)

Temat ligger som git-submodul under
`Hugo/Sites/klattorp.se/themes/gallery` och måste hämtas efter kloning:

```bash
git submodule update --init Hugo/Sites/klattorp.se/themes/gallery
```

Klonar du för första gången kan du ta allt på en gång med:

```bash
git clone --recurse-submodules <repo-url>
```

### 3. Bygg hemsidan

Stå i sajtens katalog `Hugo/Sites/klattorp.se` (där `hugo.toml` ligger) när du
kör Hugo — annars hittar inte Hugo konfigurationen:

```bash
cd Hugo/Sites/klattorp.se
hugo --gc --minify
```

* `--gc` städar bort oanvända cachade resurser (t.ex. gamla nedskalade bilder).
* `--minify` minifierar HTML/CSS/JS i resultatet.

Det färdiga statiska resultatet hamnar i `Hugo/Sites/klattorp.se/public/`.
Första bygget tar en stund eftersom Hugo skalar ner alla bilder i galleriet.

För lokal förhandsvisning med live-uppdatering (öppna <http://localhost:1313/>):

```bash
hugo server
```

> **Obs:** kör du en nyare Hugo kan du se varningar av typen *"languageCode … was
> deprecated"*. De är ofarliga och stoppar inte bygget.

### Alternativ: bygg Hugo Extended från submodulen

Vill du inte installera Hugo kan du i stället bygga binären från källkoden i
submodulen `Hugo/bin/hugo`. Det kräver [Go](https://go.dev/) (>= 1.22) och en
C-kompilator (t.ex. `gcc`), eftersom Extended-utgåvan använder CGO för SCSS/Sass:

```bash
git submodule update --init Hugo/bin/hugo
cd Hugo/bin/hugo
CGO_ENABLED=1 go build -tags extended -o ../hugo-bin .   # ger Hugo/bin/hugo-bin (gitignorerad)
cd ../../..
```

Använd sedan `../../bin/hugo-bin` i stället för `hugo` i kommandona ovan, t.ex.:

```bash
cd Hugo/Sites/klattorp.se
../../bin/hugo-bin --gc --minify
../../bin/hugo-bin server
```
