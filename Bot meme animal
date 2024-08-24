import discord
import random
import os

intents = discord.Intents.default()
intents.message_content = True

client = discord.Client(intents=intents)

# Directorio de memes por categoría
memes_directories = {
    'animales': r'C:/Users/User/OneDrive/Escritorio/Proyecto/Memes-animales',
    'divertidos': r'C:/Users/User/OneDrive/Escritorio/Proyecto/Memes-gracio'
}

@client.event
async def on_message(message):
    if message.author == client.user:
        return
    
    if message.content.startswith('/memea'):
        parts = message.content.split('/memea ', 1)
        if len(parts) < 2:
            await message.channel.send("Uso incorrecto del comando. Usa `/memea <categoría>`.")
            return

        categoria = parts[1].strip().lower()
        if categoria in memes_directories:
            meme_dir = memes_directories[categoria]
            if os.path.exists(meme_dir):
                meme_files = os.listdir(meme_dir)
                if meme_files:
                    meme_file = random.choice(meme_files)
                    meme_path = os.path.join(meme_dir, meme_file)
                    await message.channel.send(file=discord.File(meme_path))
                else:
                    await message.channel.send("La carpeta de memes está vacía.")
            else:
                await message.channel.send("La categoría no existe.")
        else:
            await message.channel.send("Categoría no encontrada. Usa una categoría válida como 'animales' o 'divertidos'.")

client.run('TOKEN')
