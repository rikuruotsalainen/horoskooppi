# Horoskooppi App

## Riku Ruotsalainen

### Kuvaus

Harjoitustyö on horoskooppi app josta käyttäjä voi käydä katsomassa päivän horoskoopin.
Soveluksessa käyttäjä valitsee ensin oman horoskooppinsa jonka jälkeen sovellus korostaa sen mutta käyttäjä voi myös lukea muiden horoskooppien ennustuksia.
Horoskoopit vaihtuvat päivittäin.

### Materiaalit

Hyödynsin työssä Tikorporatessa aiemmin tehtyä Amethyst projektia.
https://github.com/jamktiko/Amethyst
Etenkin siinä tehtyä horoskooppi toiminnallisuutta joka toimii saman tyylisesti kuin tämä sovellus mutta React Nativella tehtynä puhelimelle.
Harjoitustyön kuvat ja värimaailma on otettu myös Amethyst projektista.

### Tekoäly

Käytin tekoälyä fetchin luomisessa koska en osannut itse ohittaa CORS erroria minkä fetch muuten antoi

    > // AI käytti api.allorigins.win proxya joka ohtti CORS errorin
    > const  proxyUrl = 'https://api.allorigins.win/get?url=';
    > //halutun fetchin URL
    > const  targetUrl =`https://horoscope-app-api.vercel.app/api/v1/get-horoscope/daily?sign=${itemId}&day=TODAY`;
    > // Muuten normaali fetch mutta siinä yhdistetään proxyUrl ja targetUrl
    > const  response = await  fetch(proxyUrl +encodeURIComponent(targetUrl));

Muuten käytin tekoälyä vähän tyylitteluun koska olin laiska
