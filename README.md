Sitevision mobilformulär
========================

<div style="float:right"><img width="220" src="https://raw.github.com/peterk/sitevision-geoform/master/screens/ios.png" alt="iPhone som visar ett formulär med en karta i. Koden använder telefonens GPS för att positionera användaren." width></div>

En miniguide för att skapa ett mobilformulär med geopositionering och bifoga
bild i Sitevision. Testat i Sitevision version 3.5.3 men bör fungera från 3.0.
Målet är att skapa ett formulär som fingerar i de flesta moderna mobiltelefoner
med stöd för positionering.

Innehåll:

1. Skapa en responsiv mall med ett fast flexibelt grid (om du inte redan har en)
2. Skapa en ny sida
3. Skapa ett e-postformulär med fält för positionering
4. Några småfixar


### <a id="h1"></a>1. Skapa en responsiv mall med ett grid

Om du inte redan har en responsiv mall skapar du en ny tom mall baserad på "Blank mall". Se till att du först har aktiverat grids på webbplatsen ([se manualen om grids](http://help.sitevision.se/SiteVision_3_0/gridConfigRepository.html) för mer info) och slagit på responsive design.

I denna mall har jag skapat en gridrad och två gridspalter om 6 kolumner vardera. Då kan man ha instruktioner eller liknande till höger om formuläret.

![Översikt över delarna i en mall i Sitevision](https://raw.github.com/peterk/sitevision-geoform/master/screens/00_grid-template.png)


### <a id="h2"></a>2. Skapa en sida

Skapa en ny sida baserad på föregående mall. Ställ in "Tillägg i head" på sidan och peka ut denna stilmallsfil: https://netdna.bootstrapcdn.com/bootswatch/2.3.2/cerulean/bootstrap.min.css - den gör knappar lite tydligare. Lägg till en logotyp och en inledande text på sidan.


### <a id="h3"></a>3. Skapa ett e-postformulär med fält för positionering

Först ska vi skapa ett skriptfält med namnet "Plats" och två delfält som ska lagra latitud och longitud. Dessa sätts automatiskt via GPS:en i användarens telefon. Lägg till skriptfältet så här:

![Skriptfält i modulen E-postformulär](https://raw.github.com/peterk/sitevision-geoform/master/screens/01_skript-plats.png)

Lägg till delfälten med namnet "lat" och "lon":

![Delfråga med namnet lat](https://raw.github.com/peterk/sitevision-geoform/master/screens/02_screen_lat.png)

Under fliken "Skript" för skriptfältet klickar du på "Velocity" och klistrar in [koden för fälten från denna fil](https://github.com/peterk/sitevision-geoform/blob/master/skriptfaltkod.vm). Koden anropar Google Maps API och ritar upp en liten karta med aktuell position.

Skapa de fält du vill ha utöver platsangivelsen. Förslagsvis skapar du ett beskrivningsfält, ett bifoga fil-fält samt namn och kontaktuppgifter till den som rapporterar med formuläret. Fält för att bifoga fil brukar öppna kameran eller galleriet på de flesta mobiler.

Ställ in övriga saker för formuläret (e-postmottagare etc).


### <a id="h4"></a>4. Några småfixar

För några sista fixar lägger vi en HTML-modul sist på sidan i vilken vi klistrar in följande kod:

```html
<script type="text/javascript">
  //Sätt lite stilar på Sitevisions standardknapp
  document.querySelector("input[type='submit']").setAttribute("class", "btn btn-large btn-primary");
</script>
```

Ange även lite CSS-tweaks för att snygga upp Sitevisions standardgenerering av formulärfält genom att i egenskaper på sidan ange följande CSS:

```css
textarea, input {
    width:97%;
}
form div br {
    display:none;
}
label {
    font-weight:bold;
    clear:both;
}
```

![Egen stil på sidan](https://raw.github.com/peterk/sitevision-geoform/master/screens/03_egen-stil.png)

Klart! Du har nu byggt ett mobilanpasat formulär med positionering som kan användas för t.ex. felrapportering.


