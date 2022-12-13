# discord_export
A module that lets you export messages from a Discord channel into an HTML file that just looks like Discord.

## Usage
```py
import chat_exporter
import discord
from discord.ext import commands

bot = commands.Bot(command_prefix=("!",), intents=discord.Intents.all(), case_insensitive=True)

@commands.command()
async def save_chat(ctx):
    limit = 20 # or `None` if you want the whole chat to be saved
    favicon = bot.user.avatar_url # or `bot.user.avatar.url` if you're using discord.py>2.0
    timezone = ctx.guild.region # this can be any string you want
    
    transcript = await chat_exporter.export(ctx.channel, favicon, limit, timezone)
    transcript_file = discord.File(BytesIO(transcript.encode()), filename=f"{ctx.channel.name}-transcript.html")
    await ctx.author.send(file=transcript_file)
```

## Copyright Notice
Amazing thanks to [@muqshots](https://github.com/muqshots) for creating the original discord chat exporter. I've tweaked it here and there to make it slightly better in my opinion. Full credit goes to him!
