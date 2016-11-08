# ELKFree201611
NetAcademia ElasticSearch (+RabbitMQ) ingyenes tanfolyami oldal

A virtuális gépeket [innen lehet letölteni](https://mega.nz/#F!7kpAECpb!Tl_a6DBqiwDfo7InEtox_Q). Itt egy Windows és egy Linux (Ubuntu64) virtuális gép található. A Windows-ból majd kettőt fogunk használni, illetve egy Ubuntu szervert.

Alternatív letöltési lehetőség az Azure-ról: [Ubuntu64](https://vidibitstorage.blob.core.windows.net/elsfree/UbuntuBase64.rar) és [Widows](https://vidibitstorage.blob.core.windows.net/elsfree/w2k12r2-1.rar)

A használathoz a VMWare ingyenes Player kell, amit [innen lehet letölteni](http://www.vmware.com/products/player/playerpro-evaluation.html)

A VMWare Windows 10-re telepítéséhez lehet, hogy  [le kell tiltani a Credential Guard/Device Guard](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2146361) nevű szolgáltatást. Részletes leírás a linken.

Délelőtt még erről itt egy részletes leírást készítek, hogy a 13:00-as kezdésre mindenki fel tudjon készülni.

1. A letöltött virtuális gépeket kicsomagoljuk, és a Windows-osból másolunk egy másodikat. A .vmx állományra kattintunk mindegyik könyvtárban (w2k12r2-1, w2k12r2-2, UbuntuBase64), így elindul a három virtuális gép. (A VMWare player telepítve kell, hogy legyen a gépen)

Belépés a windows szerverekbe: Administrator jelszó: Windows2012
Belépés a Ubuntu szerverre: név: netacademia, jelszó: neta

2. Csomagkezelőt telepítünk: [chocolatey.org](https://chocolatey.org/)

Telepítéshez ezt másoljuk a vágólapra az oldalról: 
@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"

3. telepítünk [elasticsearch](https://www.elastic.co/) szervert az ELK szerverünkre.
Az elasticsearch [nyílt forráskódú](https://github.com/elastic/elasticsearch) java-ban készült document szerver. [Lucene-re épül az adatbázis](http://lucene.apache.org/core/), a teljes szöveges keresésre optimalizálva.

[GitHub teljes szöveges keresése ebben zajlik](http://www.elasticsearch.org/case-study/github/)

[A Legnépszerűbb teljes szöveges keresésre használt adatbázismotor](http://db-engines.com/en/blog_post//55)

[A Microsoft is használja az MSN-en, másodpercenként 24.000 kérést szolgál ki](https://www.elastic.co/elasticon/2015/sf/powering-real-time-search-at-microsoft)

[Egy cikk a .NET-es alkalmazásfejlesztésről ElasticSearch alapokon](https://www.simple-talk.com/dotnet/net-development/how-to-build-a-search-page-with-elasticsearch-and-net/)

[A NetAcademia blogon meg találhatók ezek linkek is](http://netacademia.blog.hu/tags/ElasticSearch)

A telepítés a chocolatey csomagkezelővel a következő (Adminisztrátori parancssorból): **cinst elasticsearch**

Telepítés után be kell állítani a **JAVA_HOME** környezeti változót, admin paracssorból pl. így: **setx JAVA_HOME "C:\Program Files\Java\jre1.8.0_111" /M**

Amit még érdemes elmondani: mivel java, fut windowson, linuxon, osx-en. Nagyon jól skálázható: több száz gépes fürtöket is használnak probléma nélkül. Alapértelmezésben elindul, és kiszolgál minket a localhost:9200-on.

A beállításai itt találhatóak: C:\ProgramData\chocolatey\lib\elasticsearch\tools\elasticsearch-2.3.1\config\elasticsearch.yml és logging.yml.

ezt megnyitni leginkább notepad++-ból érdemes: **cinst notepadplusplus**

A [YAML](http://www.yaml.org/) egy emberi fogyasztásra alkalmas, a JSON formázás kiváltására készült formázónyelv. [Wikipédia](https://en.wikipedia.org/wiki/YAML)

telepítjük a curl-t: **cinst curl** majd: **curl http://localhost:9200** és válaszol:

´´´json
{
  "name" : "Vindaloo",
  "cluster_name" : "elasticsearch",
  "version" : {
    "number" : "2.3.1",
    "build_hash" : "bd980929010aef404e7cb0843e61d0665269fc39",
    "build_timestamp" : "2016-04-04T12:25:05Z",
    "build_snapshot" : false,
    "lucene_version" : "5.5.0"
  },
  "tagline" : "You Know, for Search"
}
´´´

Az ElasticSearch egy 2.3.1, amit a chocolatey feltesz. A [legújabb itt most az 5.0](https://www.elastic.co/downloads/elasticsearch), letölt, kicsomagol, futtat. Kell neki JAVA, JAVA_HOME beállítás és ennyi.

A kezeléséhez plugin-t lehet telepíteni. Például a [kopf](https://github.com/lmenezes/elasticsearch-kopf) és a [HQ](http://www.elastichq.org/).

Telepítésük: 

Elnavigálunk az Elasticsearch bin könyvtárába: C:\ProgramData\chocolatey\lib\elasticsearch\tools\elasticsearch-2.3.1\bin majd kérünk egy cmd-t. Itt pedig: **plugin install lmenezes/elasticsearch-kopf** telepíti a Kopf-ot, a **plugin -install royrusso/elasticsearch-HQ** telepíti a HQ-t. Elérni itt lehet őket: [kopf](http://localhost:9200/_plugin/kopf) illetve [HQ](http://localhost:9200/_plugin/HQ)






