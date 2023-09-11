# RandomPfp
This bot displays random member avatars in an embed.

# index.js
```js
const Discord = require('discord.js');
const fs = require('fs');
const config = require('./config.js');

const intents = new Discord.Intents([
  Discord.Intents.FLAGS.GUILDS,
  Discord.Intents.FLAGS.GUILD_MESSAGES,
  Discord.Intents.FLAGS.GUILD_MEMBERS,
  Discord.Intents.FLAGS.GUILD_PRESENCES,
]);

const client = new Discord.Client({ intents });

client.once('ready', () => {
    console.log(`Logged in as ${client.user.tag}`);

    setInterval(() => {
        const channel = client.channels.cache.get(config.channelId);

        if (!channel) {
            return console.error("The channel specified in the configuration does not exist.");
        }

        const randomUser = channel.guild.members.cache.random();
        const userAvatar = randomUser.user.displayAvatarURL({ format: 'png', size: 1024, dynamic: true });

        const embed = new Discord.MessageEmbed()
            .setTitle(`Avatar of ${randomUser.displayName}`)
            .setImage(userAvatar)
            .setColor(config.embedColor)
            .setFooter(config.embedFooter);

        channel.send({ embeds: [embed] });
    }, 10000); // 10 seconds (milliseconds)
});

client.login(config.token);
```

# config.js
```js
module.exports = {
    token: 'MTE1MDc2OTY4NzU0Njg0MzIzNg.GTe6-o.N8qUxBAmGvYCSjD8d0jauWAW5paa_fweLZCMdM',
    channelId: '1150770151285850132',
    embedColor: '#2b2d31',
    embedFooter: 'RandomPfp by 93cz'
};
```
