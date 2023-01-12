<script>
	import { browser } from '$app/environment';
	import '../app.css';

	let video;
	let playing = false;
	let muted = false;
	let fullScreen = false;
	let showControls = false;

	function togglePlay() {
		if (playing) {
			video.pause();
		} else {
			video.play();
		}
		playing = !playing;
	}

	function toggleMute() {
		video.muted = !video.muted;
		muted = video.muted;
	}

	function setVideoProgress(e) {
		video.currentTime = (e.target.value * video.duration) / 100;
	}

	function toggleFullScreen() {
		if (!fullScreen) {
			document.documentElement.requestFullscreen();
		} else {
			document.exitFullscreen();
		}
		fullScreen = !fullScreen;
	}
</script>

<div class="flex justify-center items-center h-screen w-screen">
	<div
		class="container {fullScreen ? 'w-screen' : 'w-[700px]'} {fullScreen
			? 'h-screen'
			: 'h-auto'} border border-red-300 relative flex flex-col"
	>
		<video
			src="https://res.cloudinary.com/dvzkop7eh/video/upload/v1673052095/ad_mq7af1.mp4"
			bind:this={video}
			on:play={() => (playing = true)}
			on:pause={() => (playing = false)}
			on:timeupdate={() =>
				requestAnimationFrame(() => {
					const progress = (video.currentTime / video.duration) * 100;
					document.getElementById('progress').value = progress;
				})}
			on:volumechange={() => (muted = video.muted)}
			class="w-full absolute"
			controls={false}
		>
			<track kind="captions" />
			Sorry, your browser doesn't support embedded videos.
		</video>

		<div
			class="controls p-2 flex {fullScreen ? 'h-[100px]' : 'h-auto'}
		 {fullScreen ? 'bg-[#5a4e8647] mb-0 mt-auto' : 'bg-[#c6baf047] mt-[20.5em]'}"
			id="controls"
		>
			<button on:click={togglePlay}>
				{playing ? 'Pause' : 'Play'}
			</button>

			<button on:click={toggleMute}>
				{muted ? 'Unmute' : 'Mute'}
			</button>

			<button on:click={toggleFullScreen}>
				{!fullScreen ? 'FullScreen' : 'Exit FullScreen'}
			</button>

			<input type="range" min="0" max="100" id="progress" on:input={setVideoProgress} />
		</div>
	</div>
</div>

<style>
	video::-webkit-media-controls {
		display: none !important;
	}
	video::-webkit-media-controls-enclosure {
		display: none !important;
	}
	.controls {
		z-index: 3147483697 !important;
		align-items: center;
		justify-content: space-between !important;

		position: relative;
	}
	video {
		z-index: 0 !important;
	}
</style>
