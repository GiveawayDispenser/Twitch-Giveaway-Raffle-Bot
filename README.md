# GiveawayDispenser #

This bot actually dispenses giveaways that give better luck each time you lose!
>Some people equate this to a raffle; however raffles by definition require payment to enter, so we use the correct word instead (giveaway) since it's free to enter.  Wouldn't want any "small indi companies" to ban us just because they saw the word raffle and assumed RMT without even investigating.  English is hard.

This bot uses a system that has been called many things.  Some examples would be bad luck protection, good luck guarantee, lucky scuff protection, or pity (think Genshin Impact).  To make things as customizable as possible, the term for this "luck", is defined as a currency which can be named anything the streamer chooses.  Default is Token(s).

Simply put, each giveaway a user enters and does not win, they receive currency.  When someone wins, they lose all of their currency.

##### What does this currency do?
- Each currency you have will increase the minimum size of the dice you roll.  The dice starts out rolling 0-1000.  So for example, lets say you entered a giveaway and did not win, you get 1 currency.  The next giveaway that you enter, instead of rolling a 0-1000 dice to determine if you win (by getting the highest roll), you would roll a 10-1000 sided dice.  This effectively increases your odds of getting a higher roll.  This effect stacks.  So lets say you had 2 currency, you would then roll a 20-1000 sided dice, so on and so forth.


## Features

#### Discord Integration
- Upon finalizing a giveaway, all the rolls will be outputted to a designated discord channel.
- Streamer can request a log of all bot commands/history sent through discord in a private channel.

#### Multi Winner giveaways
- Option to pick multiple winners for a single giveaway.  Maybe you want to carry TWO or more people in a key!

#### Overflow
- Users retain any excess currency after winning a giveaway.  As an example, a user has 220 currency, and wins a giveaway.  Only 100 of that was actually used to win the giveaway (to make your minimum roll the same as the maximum roll - 1000-1000).  With overflow ON, this user would end up with 120 currency after winning.  With overflow OFF, this user would end up with 0 currency after winning.

#### Winner cooldown
- Prevents winners from entering/winning multiple raffles in a row.  Setting this to 1 makes it so no one can win back to back giveaways.

#### Tiered or Untiered Subluck
- Subluck is enabled by default and can be set per tier level (1, 2 or 3).  Think of this as permanent currency that can be used every time you enter a giveaway.  Default is 30, 35, 40.

#### Anti-Currency Farming AKA afkreroll penalty
- Imagine yourself in a stream that does giveaways for key carries and you are actively watching the stream from your computer at home.  You have been trying all day to get into a Dungeon Finder key, but no one is inviting you.  You should be rewarded for watching the stream and earning more currency to earn your next win.
- Now, imagine someone at work who hasn't even been trying to get into dungeon finder groups (because they can't even play the game from work), and not even watching the stream who keeps entering every giveaway KNOWING that you cannot accept the free key.  They are only trying to "farm" extra luck aka currency for when they get home hours later and enter.
- Now imagine everyone at work entering every single giveaway.  Every winner would have to be passed over, and everyone would get free currency.  The streamer is now wasting their time having to wait for you to respond and then roll off another winner.  How many people will pass on their win?  This is not fair for the people who are actually entering the giveaways to WIN now, not try and farm it for later.
- This feature works by penalizing anyone who wins but fails to claim their winnings either because they choose not to accept or if they are afk/do not respond.

## Bot Commands

### **Running a Giveaway**

 ##### Start a giveaway
- - <kbd>!sg _keyword or phrase_</kbd> - Short for Start Giveaway. This command will start a giveaway using the keyword or phrase (yes, you can even use the !) given as the method of entering the giveaway.  If no keyword or phrase is provided, then it will use the default one stored in the DB.  If a keyword or phrase is provided, then it both starts a giveaway AND sets the new default keyword or phrase to that. Viewers enter the giveaway by typing just the keyword or phrase into chat.
  - <kbd>!sgnoluck _keyword or phrase_</kbd> - Short for Start Giveaway that doesn't take luck into consideration (disabled). This command will start a giveaway using the keyword or phrase (yes, you can even use the !) given as the method of entering the giveaway.  If no keyword or phrase is provided, then it will use the default one stored in the DB.  If a keyword or phrase is provided, then it both starts a giveaway AND sets the new default keyword or phrase to that. Viewers enter the giveaway by typing just the keyword or phrase into chat.

#### Selecting a winner
- <kbd>!winner _pardon_</kbd> - Select one winner and stop accepting new entrants.  This will announce the viewer that had the highest roll.  Appending the word "pardon" after !winner will "pardon" the previous winner.  A pardoned viewer will be entirely removed from the giveaway and will not incur any afkreroll penalties if they are enabled.  If a winner is unable to accept the prize, simply issue another !winner command to get the next highest roll.

#### Finalizing the giveaway
-  <kbd>!lock</kbd> - Finalize the giveaway.  This will lock in the last winner announced and finalize the giveaway, distributing all luck to those involved and updating the DB.
-  <kbd>!lock _1_</kbd> - Lock in the last winner announced, but NOT finalize the giveaway.  Use this if you wish to have multiple winners in one giveaway.
-  <kbd>!lock _2_</kbd> - Finalize the giveaway ONLY.  This will not lock in any winners, use !lock 1 to do that.  For example, this would be used after issuing <kbd>!winner</kbd> -> <kbd>!lock 1</kbd> -> - <kbd>!endgiveaway</kbd> - End the current giveaway.  No luck or stats will result from the giveaway.  Useful if you start a giveaway on accident, as a test, or use the wrong keyword.

>A typical single winner giveaway will look something like this:
  ```
!sg freekey - Starts the giveaway with keyword freekey.
    Users would then enter the keyword to enter.
!winner - Announces the winner.
    The winner acknowledges that they can and will accept the free key.
!lock - Locks in the winner, finalizes the giveaway, disperses any currency, and reports the giveaway rolls to discord (if configured).
  ```

**Giveaway Utility Commands**

- <kbd>!gcount</kbd> - Giveaway Count.  This will announce in chat how many viewers are currently entered in the giveaway.
- <kbd>!add _targetuser_</kbd> - Add targetuser to the current giveaway if they are not entered already.  This might be useful if someone asks you to enter them in the raffle while they are on discord but unable to type for example.

**Giveaway Settings**
- <kbd>!setsubluck</kbd> - This will aloow you to see what the values are set to as well as let you change them.  Default tier values are 30 for t1, 35 for t2. 40 for t3.  If you are a Tier 1 subscriber, then every giveaway entered will increase the floor (minimum) of your roll.  For example instead of rolling 0-1000, you would roll 300-1000, thus increasing your odds of getting a higher roll.  Example: <kbd>!setsubluck 30 35 40</kbd>
- <kbd>!afk% _percent_</kbd> - Announces to chat the current afkreroll penalty percent.  Specify a percent to change it.  Example: <kbd>!afk% 50</kbd>
- <kbd>!afk$ _amount_</kbd> - Announces to chat the current afkreroll penalty amount.  Specify an amount to change it.  Example: <kbd>!afk$ 1</kbd>
- <kbd>!setcurrency _name_</kbd>- Announces the name of the currency. The term for luck granted by this bot is referenced as a currency, which is something you hold on to and can be named anything you want with this command. The default name for this currency is Token(s).  Example: <kbd>!setcurrency Stripper Cash</kbd>
- <kbd>!confirmentry _phrase_</kbd> - Gets or sets if the bot responds when someone enters a giveaway with the specified phrase.  Entering phrase as 0 will stop the bot from confirming entries.  Default is OFF.
- <kbd>!followeronly _0 or 1_</kbd> Enables(1) or disables(0) follower only mode for giveaways. Use without an option to display if it's on or off.
- <kbd>!winnercooldown _amount_</kbd> - Gets or sets the winner cooldown.  Setting amount to 0 will disable this feature.  For example, if this is set to 1, then people are unable to enter the giveaway immediatley after winning.  Setting to 2, will make it so winners are unable to enter giveaway until 2 giveaways have happened since winning.  Default is OFF (0).





**User Info/Settings**
- <kbd>!report _targetuser_</kbd> - Report to chat stats for the user issuing the command.  If targetuser is specified, then it will report the stats for that user instead.
- <kbd>!substatus _targetuser_</kbd> - Announces in chat if targetuser is a sub, and if they are, which tier.
- <kbd>!addone _targetuser amount_</kbd> - Adds an amount of currency to targetuser.  An amount of 0 will reset that users currency to 0. Example: <kbd>!addone scymplex 1</kbd> to give scymplex 1 currency.
- <kbd>!addchat _amount_</kbd> - Adds an amount of currency to everyone currently in chat (watching the stream). Example: <kbd>!addchat 1</kbd> adds 1 currency to all users in chat.

**Information**
- <kbd>!giveaway</kbd> - Announces information about how giveaways work with this bot.
- <kbd>!math</kbd> - Describes how the math works with the diminishing returns for those who just want to know.
- <kbd>!overflow</kbd> - Describes how the overflow system works and if it is enabled.
- <kbd>!botversion</kbd> - Announces the current bot version along with some contact information for the author.
- <kbd>!giveawaysettings</kbd> - Spits out which features are enabled.

**Misc. Commands**
- <kbd>!randomwinner</kbd> - Picks a random person currently watching the stream and announces it.
- <kbd>!randint</kbd> - Picks a random number from 0-1000
- <kbd>!roll _targetuser_</kbd> - Emulates rolling the dice as if the user was in a giveaway (with currency).

**Private Settings/Commands**
>These commands must be whispered directly to the bot, and do not provide responses via whisper if any.  Only streamers can access these commands.

- <kbd>setoauth _oauthkey_</kbd> - Sets the oauth key that the bot will need in order to fetch certain information about the stream and users in it.
- <kbd>setclientid _clientid_</kbd> - Sets the client id that the bot will need in order to fetch certain information about the stream and users in it.
- <kbd>setdiscordkey _discordwebhook_</kbd> - Sets the discord webhook which is required in order for the bot to output all the rolls upon a giveaway being finalized.
- <kbd>setdiscordkey2 _discordwebhook2_</kbd> - Sets the discord webhook #2 which is required in order for the bot to output bot log files.  Probably make this discord channel private.
- <kbd>setoverflow _amount_</kbd> Entering an amount will make it so when someone wins a giveaway and their currency amount was over 100, the amount over 100 is kept, otherwise all currency is lost after u win. Setting the amount to 0 disables this feature.
- <kbd>setgiveawaymsg _giveaway message_</kbd> Changes what you are giving away upon starting the giveaway. What are you giving away? Default: a FREE KEY
- <kbd>settimermsg _msg_</kbd>  This is the chat message that announces that the giveaway is still open. Default: a FREE KEY!
- <kbd>settimerdelay _delay_in_seconds_</kbd> Use this to change the delay between the announcement that there is still a gvieaway in progress. Default: 45
- <kbd>settimerenabled _0 or 1_</kbd> This will enable (1) or disable (0) the announcement of a giveaway in progress. Default: enabled (1)
- <kbd>enablebot _0 or 1_</kbd> This will enable(1) or disable(0) the bot from accepting commands or keywords from chat.  Default: enabled(1)
- <kbd>sendlog</kbd>  This will send the current bot log file to discord webhook #2.  This can be helpful for example in determining if someones claim to not getting their currency has any merrit, or just basic troubleshooting/analysis.

## Possible Future Features
 [ ] Raffles that work across multiple Twitch Channels.

 [ ] Settings configurable via discord buttons in addition to the already existant chat commands.

 [ ] Twitch built-in Channel Redepmptions that grant currency.

 [ ] Gifting subs or giving X bits gives temporary one-time use currency (with a cap).

 [ ] Redeem a prize that steals currency from another random person in chat.

 [X] Giveaways that don't use any luck. _Addded on 6/23/2021_

 [X] Prevent people from winning a giveaway a second time until X giveaways have passed.  Winning giveaways back to back is usually bad. _Added 6/21/2021_

 [X] WoW Weakaura that shows in game for viewers to see all the keys currently in the group (helpfull for KSM etc.).

## Contact Info

Scymplex on https://discord.gg/7z3NEyu72n
