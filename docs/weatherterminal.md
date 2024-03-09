---
title: Weather Terminal
layout: default
---

# Weather Terminal

This script reports the real time weather on a given area, it can be integrated with other scripts and applications.


## Basic Usage

weather.sh city region (e.g: weather.sh buenos aires argentina)


## Configuring

### Getting an API Key

register an account at [weatherapi.com](https://weatherapi.com) The free plan allows for one million hits a day. 

Obtain your assigned API key, edit weather.sh and change the value of the variable API_KEY="" for your newly assigned key
```
API_KEY="YOUR-API-KEY-GOES-HERE"
```

### Changing the language of the output

By default, the output is in English. If you'd like the output to be in Spanish, edit the weather.sh script 
and comment the two printf lines and uncomment the two printf lines that are commented by default.

```
## If you want the output in spanish, uncomment the two commented lines and comment the two in English. 
## Otherwise leave it as it is.

    printf "Weather Report for: %s, %s\n" "$City" "$Region"
#    printf "Clima para: %s, %s\n" "$City" "$Region"
#    printf "Temp Actual: %s°C | ST: %s°C | Nubosidad: %s%% | Humedad: %s%% | Viento: %s km/h, %s\n" \
    printf "Temperature: %s°C | Feels Like: %s°C | Cloud Index: %s%% | Humidity: %s%% | Wind Spd.: %s km/h, %s\n" \
```


## Integration with Discord Bots (python)

In this example, the discord bot, written in python, will trigger a response when someone in a discord channel excecutes the command !clima city region (e.g: !clima buenos aires argentina)

```
@bot.command(name='clima')
async def get_clima(ctx, *args):
    location = ' '.join(args)
    try:
        clima_output = subprocess.check_output(['/bin/bash', clima_path, *args], text=True)
        await ctx.send(f'{clima_output}')
    except subprocess.CalledProcessError as e:
        print(e)
        await ctx.send('Alexia se debe haber mandado alguna cagada pq esto no funca')
```

For this to work, you need to create a variable in your bot's script called clima_path including the path to your bash weather.sh script.
if you are planning on making this portable, e.g: including the script in the same directory where your bot runs, make sure you have ```import os``` in your python script.
 
