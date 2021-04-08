<template>
	<div>
		<h1>Playlist Genre Search</h1>
		<button v-on:click="getToken">Test</button>
		<form>
			<div class="container">
				<Dropdown
					:options="genres.listOfGenres"
					:selectedValue="genres.selectedGenre"
					:changed="genreChanged"
				/>
				<Dropdown
					:options="playlist.listOfPlaylists"
					:selectedValue="playlist.selectedPlaylist"
					:changed="playlistChanged"
				/>
				<button type="submit">Search</button>
			</div>
			<div class="list-container">
				<Listbox :items="tracks.listOfTracks" :clicked="listBoxClicked" />
				<Detail />
			</div>
		</form>
	</div>
</template>

<script>
	require("dotenv").config();

	import Detail from "./components/Detail";
	import Dropdown from "./components/Dropdown";
	import Listbox from "./components/Listbox";
	import axios from "axios";

	export default {
		name: "App",
		components: {
			Dropdown,
			Detail,
			Listbox,
		},
		data: () => ({
			credentials: {
				ClientId: process.env.VUE_APP_CLIENT_ID,
				ClientSecret: process.env.VUE_APP_CLIENT_SECRET,
			},
			token: "",
			genres: {
				selectedGenre: "",
				listOfGenres: [],
			},
			playlist: {
				selectedPlaylist: "",
				listOfPlaylists: [],
			},
			tracks: {
				selectedTrack: "",
				listOfTracks: [],
			},
			trackDetail: null,
		}),
		methods: {
			getToken() {
				axios("https://accounts.spotify.com/api/token", {
					headers: {
						"Content-Type": "application/x-www-form-urlencoded",
						Authorization:
							"Basic " +
							btoa(
								this.credentials.ClientId + ":" + this.credentials.ClientSecret
							),
					},
					data: "grant_type=client_credentials",
					method: "POST",
				}).then((tokenResponse) => {
					this.token = tokenResponse.data.access_token;
					console.log("token", this.token);
					axios("https://api.spotify.com/v1/browse/categories?locale=sv_US", {
						method: "GET",
						headers: {
							Authorization: "Bearer " + tokenResponse.data.access_token,
						},
					}).then((genreResponse) => {
            console.log(genreResponse)
						// setGenres({
							// this.genres.selectedGenre = this.genres.selectedGenre,
							// this.genres.listOfGenres = genreResponse.data.categories.items,
						// });
					});
				});
			},
		},
	};
</script>

<style>
	#app {
		font-family: Avenir, Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		background-color: #2c3e50;
		margin-top: 60px;
	}
</style>
