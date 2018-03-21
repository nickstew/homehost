<center><p align="center"><img src="media/v1-homehost-logo-1.png" alt="homehost logo"></p></center>
<center>
	[![contributions](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/ridhwaans/homehost/issues)
	[![release](https://img.shields.io/github/release/ridhwaans/homehost.svg)](https://gitHub.com/ridhwaans/homehost/releases/)
	[![tag](https://img.shields.io/github/tag/ridhwaans/homehost.svg)](https://gitHub.com/ridhwaans/homehost/tags/)
	[![commits-since](https://img.shields.io/github/commits-since/ridhwaans/homehost/v1.0.0-beta.svg)](https://gitHub.com/ridhwaans/homehost/commit/)
	[![license](https://img.shields.io/github/license/ridhwaans/homehost.svg)](https://github.com/ridhwaans/homehost/blob/master/LICENSE)
</center>

<center><h3>`homehost` is made for streaming your media collection over the home network</h3>
	<h4>Features: 🎥 Movies, 🎵 Music, 📺 TV Shows, 📚 Books, 📒 Comics, 🎙️ Podcasts</h4></center>

# 🎥 Movies
![](media/v1-movies-1.png)
## Demo
![movies-gif](media/v1-movies-demo-min-1.gif)
# 🎵 Music
![](media/v1-music-1.png)
## Demo
![music-gif](media/v1-music-demo-min-1.gif)

# Setup

In `./config.yml`, set the media paths, and specify a working API key for TMDB and Spotify Web API
```yaml
# Server-side configs
movies:
  path  : '/path/to/directory'
  api   : 'api.themoviedb.org/3'
  key   : '<api_key>'
music:
  path  : '/path/to/directory'
  api   : 'api.spotify.com/v1'
  key   : '<auth_token>'
```

## Naming conventions

Your media must appear in the path set by `config.yml`  
🎥 **Movies**  
```
<movies path>  
 - (subdirectory)?  
   - (movie_file_name <TMDB-movie-ID>) (.mp4|.mkv)
```
🎵 **Music**  
```
<music_path>  
 - (album_directory_name <Spotify_albumID>)  
   - ((<disc_number>-)?<track_number> track_file_name) (.mp3)
```

## Generating metadata

Server requires `<media>.json` file data at startup. Initial json state should be empty
```json
./movies.json or ./music.json
{
  "movies" or "music": []
}
```
Start homehost by running `yarn homehost` from the base directory. Server should open at `http://localhost:5000/`  
On the server, call `/api/generate` **once**. Wait for the async operation to finish and save  
**NOTE:** `nodemon` interrupts async data generation upon file save. Use `node server` instead for generating metadata  
By default, `5000` is the nodejs server port, `3000` is the react client port

## Routes

### Server-side

**GET** `/api/hello`  
**GET** `/api/generate`  
**GET** `/api/movies`  
**GET** `/api/movies/<id>`  
**GET** `/movies/<id>`  
**GET** `/api/music/`  
**GET** `/api/music/albums/<id>`  
**GET** `/music/albums/:album_id/tracks/:track_id`

### Client-side

`/movies` and `/music` are scheduled for v1.0 release. `/books`, `/comics`, `/podcasts`, `/tv` are TODO

# License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

# Powered by
<p><img src="media/spotify_green.svg"  width="200" height="150">&emsp;<img src="media/tmdb_green.svg"  width="150" height="150"></p>


