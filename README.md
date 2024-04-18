python 
import discord 
import requests 

class TeraBoxDownloader(discord.Client): 

    def __init__(self): 
        super().__init__() 
        self.token = "YOUR_TOKEN" 

    async def on_ready(self): 
        print("Logged in as {}".format(self.user)) 

    async def on_message(self, message): 
        if message.author == self.user: 
            return 

        if message.content.startswith("!download"): 
            url = message.content[7:] 
            try: 
                video_path = download_video(url) 
            except Exception as e: 
                print(e) 
                return 

            await message.channel.send("Downloaded video to {}".format(video_path)) 

    def run(self): 
        discord.login(self.token) 
        while True: 
            await self.process_events() 

if __name__ == "__main__": 
    TeraBoxDownloader().run()
