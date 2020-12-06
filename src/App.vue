<template>
	<div class="container">
		<SearchBar @termChange="onTermChange"></SearchBar>
		<div class="row">
			<VideoDetail v-bind:video="selectedVideo" />
			<VideoList
				@videoSelect="onVideoSelect"
				v-bind:videos="videos"
			></VideoList>

			<!-- V-bind, anytime the video property updates in the parent, it should automatically update the video list and provides the child with the new videos-->
			<!-- The right hand side video is the property we want to share as it is in the parent -->
			<!-- The left video is the property we want to have show up inside the child -->
		</div>
	</div>
</template>

<script>
	import axios from 'axios';
	import SearchBar from './components/SearchBar';
	import VideoList from './components/VideoList';
	import VideoDetail from './components/VideoDetail';
	const API_KEY = 'AIzaSyCRg-5pU4WAuXZ6zWI5x4FFqFN8ZPUMUVQ';

	export default {
		name: 'App',
		components: {
			SearchBar,
			VideoList,
			VideoDetail,
		},
		data: function() {
			return {
				videos: [],
				selectedVideo: null,
			};
		},
		methods: {
			onVideoSelect(video) {
				// console.log(video);
				this.selectedVideo = video;
			},
			onTermChange(searchTerm) {
				axios
					.get('https://www.googleapis.com/youtube/v3/search', {
						params: {
							key: API_KEY,
							type: 'video',
							part: 'snippet',
							q: searchTerm,
						},
					})
					.then((response) => {
						this.videos = response.data.items;
					});
			},
		},
	};
</script>
