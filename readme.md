# quick.eco
A simple & easy to use economy package for discord bots using quick.db

[![NPM](https://nodei.co/npm/quick.eco.png?downloads=true&downloadRank=true&stars=true)](https://nodei.co/npm/quick.eco/)

[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2FINEX07%2Fquick.eco.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2FINEX07%2Fquick.eco?ref=badge_shield)


# Installing
`npm i --save quick.eco`

> Note: This package uses `quick.db` to run. Please install it before using this package.

**[Join Our Discord Server](https://discord.gg/uqB8kxh)**

# Getting Started

```js
const Eco = require("quick.eco");
const eco = new Eco.Manager();
```

# Example

```js
const Discord = require("discord.js");
const client = new Discord.Client();
const Eco = require("quick.eco")
const eco = new Eco.Manager();

client.on("ready", () => {
    console.log("Bot has started!");
});

client.on("message", async (message) => {
    if (!message.guild || message.author.bot) return;
    if (message.content === "daily") {
        let add = eco.daily(message.author.id, 500);
        if (add.onCooldown) return message.reply(`You already claimed your daily coins. Come back after ${add.time.days} days, ${add.time.hours} hours, ${add.time.minutes} minutes & ${add.time.seconds} seconds.`);
        else return message.reply(`you claimed ${add.amount} as your daily coins and now you have total ${add.after} coins.`);
    }
    if (message.content === "bal") {
        let money = eco.fetchMoney(message.author.id);
        return message.channel.send(`<@${money.user}> has ${money.amount} coins.`);
    }
    if (message.content === "leaderboard") {
        let lb = eco.leaderboard({ limit: 10, raw: false });
        const embed = new Discord.RichEmbed()
        .setAuthor("Leaderboard")
        .setColor("BLURPLE");
        lb.forEach(u => {
            embed.addField(`${u.position}. ${client.users.get(u.id).tag}`, `Money: ${u.money} 💸`);
        });
        return message.channel.send(embed);
    }
});

client.login("NjU3OTUwNjk2NDAyMDU5Mjc5.XjgRXA.uS-OspxdjqXoxEQa59xVIsZvt5g");

```

# Documentaion
## [Snowflake107/quick.eco](https://quickeco.cf)


# Manager Functions

```js
addMoney(userid, amount); // adds money & returns object
fetchMoney(userid); // returns object
setMoney(userid, amount); // sets new money value & returns object
deleteUser(userid); // Deletes a user from the database
removeMoney(userid, amount); // removes certain amount from user
daily(userid, amount); // Adds daily balance & returns object with 24h cooldown
weekly(userid, amount); // adds weekly balance & returns object with cooldown
work(userid, amount, { options }); // Work function, returns object | options: { cooldown: time_in_ms, jobs: ["job name", "another job"] }
beg(userid, amount, { options }); // beg function, returns object | options: { canLose: false, cooldown: time_in_ms, customName} | [ can be used in "search" command ]
transfer(userid1, userid2, amount); // transfer balance from a user to another, returns object | [ Can be used in "rob" command ]
leaderboard({ options }); // returns leaderboard | options: { raw: false, limit: 10 }
```

# GuildManager Functions

```js
addMoney(userid, guildid, amount); // adds money & returns object
fetchMoney(userid, guildid); // returns object
setMoney(userid, guildid, amount); // sets new money value & returns object
deleteUser(userid, guuldid); // Deletes a user from the database
removeMoney(userid, guildid, amount); // removes certain amount from user
daily(userid, guildid, amount); // Adds daily balance & returns object with 24h cooldown
weekly(userid, guildid, amount); // adds weekly balance & returns object with cooldown
work(userid, guildid, amount, { options }); // Work function, returns object | options: { cooldown: time_in_ms, jobs: ["job name", "another job"] }
beg(userid, guildid, amount, { options }); // beg function, returns object | options: { canLose: false, cooldown: time_in_ms, customName} | [ can be used in "search" command ]
transfer(userid1, userid2, guildid, amount); // transfer balance from a user to another, returns object | [ Can be used in "rob" command ]
leaderboard(guildid, { options }); // returns leaderboard | options: { raw: false, limit: 10 }
```


# Making Other Commands
You can make some other commands like `rob`, `gamble` & more using above mentioned functions.

# ShopManager
This class can be used to create shop. Please check the **[documentation](https://ecodocs.cf)** for info. You can join our **[discord server](https://discord.gg/uqB8kxh)** for help.

# **Need help in quick.eco?**
- Join **[discord.gg/uqB8kxh](https://discord.gg/uqB8kxh)**.

# **Need help in quick.db?**
- Join **[discord.gg/plexidev](https://discord.gg/plexidev)**.

## License
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2FINEX07%2Fquick.eco.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2FINEX07%2Fquick.eco?ref=badge_large)
