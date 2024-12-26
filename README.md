# Horoskooppi App

## Riku Ruotsalainen

### Kuvaus

Harjoitustyöni on horoskooppi-sovellus, joka tarjoaa käyttäjälle mahdollisuuden tarkastella päivän horoskooppia.
Sovelluksen aloitusnäkymässä käyttäjä valitsee oman horoskooppinsa, joka korostetaan selkeästi. Halutessaan käyttäjä voi kuitenkin lukea myös muiden horoskoop-pimerkkien ennustuksia.
Sovelluksen sisältämät horoskoopit saadaan fetchistä ja ne päivittyvät päivittäin.

### Materiaalit

Hyödynsin työssä Tikorporatessa aiemmin tehtyä Amethyst projektia.
https://github.com/jamktiko/Amethyst
Etenkin siinä tehtyä horoskooppi toiminnallisuutta joka toimii saman tyylisesti kuin tämä sovellus mutta React Nativella tehtynä puhelimelle.
Harjoitustyön kuvat ja värimaailma on otettu myös Amethyst projektista.
Api josta päivittäiset horoskoopit haetaan: https://horoscope-app-api.vercel.app/

### Tekoäly

Käytin tekoälyä fetchin luomisessa koska en osannut itse ohittaa CORS erroria minkä fetch muuten antoi

    > // AI käytti api.allorigins.win proxya joka ohtti CORS errorin
    > const  proxyUrl = 'https://api.allorigins.win/get?url=';
    > //halutun fetchin URL
    > const  targetUrl =`https://horoscope-app-api.vercel.app/api/v1/get-horoscope/daily?sign=${itemId}&day=TODAY`;
    > // Muuten normaali fetch mutta siinä yhdistetään proxyUrl ja targetUrl
    > const  response = await  fetch(proxyUrl +encodeURIComponent(targetUrl));

Muuten käytin tekoälyä vähän tyylitteluun koska olin laiska
