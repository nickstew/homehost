<p style="text-align: center;align="center;">
<img src="media/v1-homehost-logo-1.PNG" alt="homehost logo">

<p align="center">
	<a href="https://github.com/ridhwaans/homehost/issues"><img src="https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat" alt="contributions"></a>
	<a href="https://github.com/ridhwaans/homehost/releases/"><img src="https://img.shields.io/github/release/ridhwaans/homehost.svg" alt="release"></a>
	<a href="https://github.com/ridhwaans/homehost/tags/"><img src="https://img.shields.io/github/tag/ridhwaans/homehost.svg" alt="tag"></a>
	<a href="https://gitHub.com/ridhwaans/homehost/commit/"><img src="https://img.shields.io/github/commits-since/ridhwaans/homehost/v1.0.0-BETA.svg" alt="commits-since"></a>
	<a href="https://github.com/ridhwaans/homehost/blob/master/LICENSE"><img src="https://img.shields.io/github/license/ridhwaans/homehost.svg" alt="license"></a>
</p>

<h3 align="center"> homehost is made for streaming your media collection over the home network</h3>
<h4 align="center"> Features: 🎥 Movies, 🎵 Music, 📺 TV Shows, 📚 Books, 📒 Comics, 🎙️ Podcasts </h4>


# 🎥 Movies
![](media/v1-movies-1.PNG)
## Demo
![movies-gif](media/v1-movies-demo-min-1.gif)
# 🎵 Music
![](media/v1-music-1.PNG)
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
./movies.json & ./music.json
{
  "movies": [], "music": []
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


