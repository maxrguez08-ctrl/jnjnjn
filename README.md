# Neocatcuamal Song Picker Bot

A small Discord bot for collecting songs, voting on them, and picking one for the Word or Eucharist. The picker is random, but votes make a song more likely to be chosen.

## Commands

- `/word theme` picks 4 songs for the Word. The theme can be a biblical theme name or number, like `Rock` or `1`. If you leave it blank, the bot picks a random theme.
- `/word-themes page` shows the biblical theme list by page.
- `/sunday-songs date` fetches Sunday readings from USCCB and suggests Eucharist songs that fit the readings. The date is optional and uses `YYYY-MM-DD`.
- `/songs season` suggests a Eucharist set: starting song, peace, bread, wine, and final song. The season is optional.
- `/song-practice song mp3` finds a local MP3 practice track by song name. You can also upload an MP3 to save a Discord link.
- If a matching sheet is listed in `data/song-sheets.json`, `/song-practice` also sends the sheet image.
- `/song-practice-search song` searches local MP3 practice tracks by song name.
- `/song-practice-list` shows saved practice tracks.
- `/song-add moment title url` adds a song for `Word` or `Eucharist`. The URL is optional.
- `/song-list moment` shows songs for the Word or Eucharist that have not been picked yet.
- `/song-vote id` toggles your vote for a song.
- `/song-pick moment` chooses one unpicked song for the Word or Eucharist, weighted by votes.
- `/song-clear` clears the pool. This requires the Discord `Manage Server` permission.

## Song Catalog JSON

The `/songs` command reads from `data/song-catalog.json`. Your imported catalog uses this format:

```json
[
  {
    "title": "A shoot springs from the stock of Jesse",
    "page": "123",
    "color": "White",
    "stage": 1
  }
]
```

The current Eucharist picker uses these stage rules:

- `starting`: stage 1
- `peace`: stage 1
- `bread`: stage 2
- `wine`: stage 3
- `final`: stage 1

The bot also still supports a category-based format if you decide to organize songs by part later:

```json
{
  "starting": ["Starting song"],
  "peace": ["Peace song"],
  "bread": ["Bread song"],
  "wine": ["Wine song"],
  "final": ["Final song"]
}
```

You can also use song objects:

```json
{
  "starting": [
    { "title": "Amazing Grace", "artist": "Traditional", "url": "https://example.com" }
  ],
  "peace": ["Peace Is Flowing Like a River"],
  "bread": ["One Bread One Body"],
  "wine": ["Take and Eat"],
  "final": ["Go Make a Difference"]
}
```

After changing slash commands, run:

```sh
npm run register
```

## Setup

1. Install Node.js 18 or newer.
2. Install dependencies:

   ```sh
   npm install
   ```

3. Copy the example environment file:

   ```sh
   cp .env.example .env
   ```

4. Fill in `.env`:

   ```sh
   DISCORD_TOKEN=your_bot_token_here
   DISCORD_CLIENT_ID=your_application_client_id_here
   DISCORD_GUILD_ID=your_test_server_id_here
   ```

5. Register slash commands in your server:

   ```sh
   npm run register
   ```

6. Start the bot:

   ```sh
   npm start
   ```

## Discord App Settings

Create a bot at the Discord Developer Portal:

1. Open <https://discord.com/developers/applications>.
2. Create an application.
3. Go to **Bot**, create/reset the token, and put it in `.env`.
4. Go to **OAuth2 > URL Generator**.
5. Select scopes: `bot` and `applications.commands`.
6. Select bot permissions: `Send Messages`, `Use Slash Commands`, and `Read Message History`.
7. Open the generated URL and invite the bot to your server.

For local testing, guild commands are used so changes appear quickly in one server.
# jnjnjn
