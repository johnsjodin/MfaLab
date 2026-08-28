# Motiveringar – MfaLab (övning 5.3)

## 1. Varför TOTP och inte SMS i den här applikationen?

TOTP räknas fram lokalt i authenticator-appen på telefonen och skickas aldrig över nätet, så koden kan inte fångas via SIM-kapning eller SMS-avlyssning – attacker som SMS-koder ligger öppna för. Båda kan visserligen luras vidare av en realtids-phishing-proxy, så TOTP är inte immunt, men det tar bort en hel klass av billiga attacker som SMS är sårbart för. I den här applikationen, utan budget för hårdvarunycklar eller passkeys, är TOTP det starkaste realistiska förstahandsvalet. SMS är ändå bättre än ingen andra faktor alls, så för en användare utan smartphone kan det få finnas kvar som reserv.

## 2. Hur landade jag i antal försök och låsningstid?

Jag valde fem försök och femton minuters låsning. Fem ger utrymme att slå fel någon gång (fel tangentbordslayout, gammalt lösenord) utan att låsas ute, men stoppar en ordlisteattack långt innan den hinner igenom. Femton minuter gör automatiserade försök oanvändbart långsamma samtidigt som en riktig användare inte stängs ute halva dagen. Baksidan är att kontolåsning kan missbrukas för att medvetet spärra ute riktiga användare, så en tidsbegränsad låsning är bättre än en permanent, och i skarp drift skulle jag komplettera med rate limiting per IP och nyckla låsningen så att en angripare inte trivialt kan låsa andras konton.
