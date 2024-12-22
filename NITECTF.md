# BackTrack 

challenge-
- Kenji is a nice guy who lives in Tokyo. He is in a dilemma. In 2017, he was late to an important meeting and is now facing repercussions. To defend himself, he needs to prove that it was not his fault. His evidence? The train he boarded that day, traveling between Omotesando and Suitengumae, was delayed. However, his boss is not providing the specific details of the accusation. Kenji vividly remembers one key fact: the train was around 61 minutes late.

    Help him uncover the exact date of the incident and the start time of the delay. Justice for Kenji!

    Flag Format: nite{time_date}

    Example: nite{13:00_3January}

Allright the first thing i did was to check for line which goes between omotesando and suitengumae and found out that it was hanzomon line.

I also remembered that in japan they issue a delay certificate for every time the train is late.

so searched up website to find the delay certificate of this particular line.

https://www.tokyometro.jp/lang_en/delay/history/hanzomon.html

i used this website to find it.

well this website only showed the last 30 days of delay certificates and i have to find the delay certificate in 2017.

So loaded this website in wayback machine and set it 2017 instances.

after going thorugh some starting instances, I found a date in february which had the teain 61 mins dalayed.

![image](https://github.com/user-attachments/assets/3986e26f-b0d4-4669-b1ce-dae9aaac225d)

so the flag is 
```

nite{17:00_20February}

```


