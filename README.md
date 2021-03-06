<!--
  Title: SpotifyNoDupes
  Description: The smart Spotify duplicate remover
  Author: stavlocker
-->
<meta name='keywords' content='spotify, playlist, duplicate'>
<p align="center"><img alt="SpotifyNoDupes - The Spotify duplicate remover" src="SpotifyNoDupes.png" width="350"/></p> <!-- Gross HTML because of GitHub's markdown flavour -->

Detect and remove possible duplicates in your playlists.
This program can detect possible duplicates in your playlists and remove them for you. The program suspects that two songs are the same ones if:
 1. They have the same ID (meaning they are the exact same song), making it a 100% sure case
 2. They have the same name and they are from the same artist (which isn't for 100% but is very likely)
 3. They are from the same artist and they have the exact same duration (which again can't be 100% sure but it is very likely)
The program finds those duplicates in your playlist and presents them to you. If you'd like, you can remove those suspected duplicates and you can even choose which songs out of the possible duplicates to remove.

_Why?_ Because...
 1. Some songs on spotify are released multiple times under different albums / names / languages which causes Spotify to not notice they are in fact the same song.
 2. A collaborative playlist is very hard to keep clean from duplicates, and this plugin helps prevent them - even the ones Spotify doesn't notice.
 3. Keep your playlists clean with zero duplicates - even the ones that Spotify doesn't notice.

## Screenshots
![image](https://user-images.githubusercontent.com/30472563/39255472-4c0c4f20-48b5-11e8-9d36-3adc0bed5f0a.png)
<sup>*\* The web server after authenticating. This only needs to be done once (per user).*</sup>

![image](https://user-images.githubusercontent.com/30472563/39919348-fe84c430-551b-11e8-85b5-0398e4b461e5.png)
![image](https://user-images.githubusercontent.com/30472563/40512222-d1c96b00-5faa-11e8-9aba-78cc123d7104.png)
<sup>*\* The program output for the following playlist "My Playlist".</sup>

## Run
### Regular running from the release file
The only requirements to run the release files are a Windows computer with Python 3.x installed.
1. Download the `SpotifyNoDupes.exe` release file from the [release section](https://github.com/stavlocker/SpotifyNoDupes/releases)
2. Put the file in a directory of your choice (Notice that it will create cache files in the folder that it's in)
3. You'll need to create a spotify application to use the program. You can do this at the [Spotify developer website](https://developer.spotify.com/my-applications/). In the Spotify developer website, remember to put `http://localhost:14523` as your redirect URI (Under Edit Settings).
4. Export your client ID and client secret as environment variables as `SPOTIPY_CLIENT_ID` and `SPOTIPY_CLIENT_SECRET`, respectively. Here's how to do that on Windows' `cmd`:
    ```
    SET SPOTIPY_CLIENT_ID=ClientIDGoesHere
    SET SPOTIPY_CLIENT_SECRET=ClientSecretGoesHere
    ```

5. Open the command prompt and run the file (using `SpotifyNoDupes.exe`) or simply double click on the file to open it.
---
### Running from source code
You can optionally clone this repository and run the source code directly, which is basically the same as running the   `.exe` file.

This program uses Python 3. To use SpotifyNoDupes, you need [spotipy](https://github.com/plamere/spotipy). You can install it using `pip`: `pip install spotipy`
If you know how to use `virtualenv`s it is recommended you use one. They're pretty easy to use & learn.

1. Clone the repository (*or download as zip & extract*, cloning is recommended)
2. Navigate to the repository's folder and install the required packages:
```
mkvirtualenv spotifynodupes # Optional but recommended
pip3 install spotipy
```

3. Create a spotify application so you can use `spotipy`. You can do this at the [Spotify developer website](https://developer.spotify.com/my-applications/).
4. You have two options for inputting your client ID & secret:
    1. Put your client ID & client secret into `spotifyauth.py` by uncommenting (by removing the # in the beginning of the line) the following lines and inserting your ID & secret:
    ```
    # os.environ["SPOTIPY_CLIENT_ID"] = ""
    # os.environ["SPOTIPY_CLIENT_SECRET"] = ""
    ```
    2. Export your client ID and client secret as environment variables as `SPOTIPY_CLIENT_ID` and `SPOTIPY_CLIENT_SECRET`, respectively. Here's how to do that on Windows' `cmd`:
        ```
        SET SPOTIPY_CLIENT_ID=ClientIDGoesHere
        SET SPOTIPY_CLIENT_SECRET=ClientSecretGoesHere
        ```
        On linux:
        ```
        export SPOTIPY_CLIENT_ID=ClientIDGoesHere
        export SPOTIPY_CLIENT_SECRET=ClientSecretGoesHere
        ```
5. You're done - you can basically change anything else you'd like.

---
When running from command prompt, the usage for the program is `main.py [username] [Playlist1 Playlist2 Playlist3...]` where the two arguments are optional. _Note that you can't enter playlists without a username - the first argument has to be the username._
 - `Username`: Your username
 - `Playlist1, Playlist2, Playlist3...` - As many playlists as you like, as the playlist's ID or name. Notice that these playlists must be owned by you
 
For every user that uses the program for the first time, authorization through the Spotify website is required. A window will open, asking you to copy the redirected URL back to the program. After you've done this for the first time for that specific user, the program will save your credentials.

***Note**: The program does not have access to your Spotify account password. It is simply storing the authorization key you gave to Spotify in order to communicate with the Spotify web API.*

## FAQ
**Q:** Which permissions do I need to give the program access on Spotify to, and why?

**A:** The program requests five permissions:
* [`playlist-read-private`](https://beta.developer.spotify.com/documentation/general/guides/scopes/#playlist-read-private) - Read access to user's private playlists, to check for duplicates.
* [`playlist-read-collaborative`](https://beta.developer.spotify.com/documentation/general/guides/scopes/#playlist-read-collaborative) - A permission to allow the program to also view collaborative playlists, which it can't access by default.
* [`playlist-modify-public`](https://beta.developer.spotify.com/documentation/general/guides/scopes/#playlist-modify-public) - Write access to a user's public playlists, to remove duplicates in the user's public playlists.
* [`playlist-modify-private`](https://beta.developer.spotify.com/documentation/general/guides/scopes/#playlist-modify-private) - Write access to a user's private playlists, to remove duplicates in the user's private playlists.
* [`playlist-read-collaborative`](https://beta.developer.spotify.com/documentation/general/guides/scopes/#playlist-read-collaborative) - Access the user's collaborative playlists. 

**Q:** I'm getting a `UnicodeEncodeError: 'charmap' codec can't encode characters`...

**A:** This error is because you have unicode characters in your songs/playlists. Before running the program, run the command `chcp 65001` before running the program. Some consoles won't display unicode characters, like the default `cmd.exe` on windows. [Cmder](http://cmder.net/) for example can display unicode characters with this command.

## Contributing
There's a reason this repository is open source. You are very welcome to contribute - if you want to squash a bug, make an improvement, or anything - feel free to fork the repository and create a pull request. Just make sure that your code is clean, and matches the rest of the code in the repository syntax-wise.

You are also very welcome to submit issues about bugs, improvements, ideas, questions and anything you'd like about this repository.

In order to issue pull requests, you'll need to make a fork of this repository, commit to that fork, and then open PRs from your fork:
1. Create a fork of the repository (Use the fork button in the top right corner in github)
2. Clone your fork in a directory of your choice, and keep the upstream updated:
```
git clone https://github.com/you/SpotifyNoDupes.git`
git remote add upstream git://github.com/nonamesl/SpotifyNoDupes.git
git fetch upstream
```
3. Use `git pull upstream master` to keep up with changes from this repository. Most GUI git clients will work as expected and some might offer you to submit PRs to the original repo.

## See also
If you liked SpotifyNoDupes, you'll love [`SpotifyRandomizer`](https://github.com/DanielsWrath/SpotifyRandomizer), a python script to finally truly randomize your playlists (which I contributed a lot to :wink:). Thanks [@DanielsWrath](https://github.com/DanielsWrath) for inspiration from the [`SpotifyRandomizer`](https://github.com/DanielsWrath/SpotifyRandomizer) repository.

---
<i><sup>This program is not affiliated with Spotify<sup>®</sup> in any way (other than using their awesome API to provide you this service).</sup></i>
