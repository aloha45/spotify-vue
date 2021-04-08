<template>
<h1>Playlist Genre Search</h1>
		<form onSubmit={handleSubmit}>
			<div className="container">
				<Dropdown
					options={genres.listOfGenres}
					selectedValue={genres.selectedGenre}
					changed={genreChanged}
				/>
				<Dropdown
					options={playlist.listofPlaylists}
					selectedValue={playlist.selectedPlaylist}
					changed={playlistChanged}
				/>
				<button type="submit">Search</button>
			</div>
			<div className="list-container">
				<Listbox items={tracks.listOfTracks} clicked={listBoxClicked} />
				{trackDetail && <Details {...trackDetail} />}
			</div>
		</form>
		</>
</template>

<script>
require('dotenv').config()

import Detail from './components/Detail'
import Dropdown from './components/Dropdown'
import Listbox from './components/Listbox'

export default {
  name: 'App',
  components: {
    Dropdown,
    Detail,
    Listbox
  },
  data: ()  => ({
    credentials: {
      ClientId: "",
      ClientSecret: "",
    },
    token: "",
    genres: {
      selectedGenre: "",
      listOfGenres: [],
    },
    playlist: {
      selectedPlaylist: "",
      listOfPlaylists: []
    },
    tracks: {
      selectedTrack: "",
      listOfTracks: []
    },
    trackDetail: null
  }),
  methods: {
    getToken() {
      
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
