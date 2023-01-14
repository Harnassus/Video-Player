<script>
	import { browser } from '$app/environment';
	import '../app.css';
	let video;
	let playing = false;
	let muted = false;
	let fullScreen = false;
	let showControls = false;
	let fullscreenchange =
		'fullscreenchange' || 'webkitfullscreenchange' || 'mozfullscreenchange' || 'MSFullscreenChange';
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
			document.documentElement.requestFullscreen() ||
				document.documentElement.webkitRequestFullscreen() ||
				document.documentElement.mozRequestFullScreen();
		} else {
			document.exitFullscreen();
		}
		fullScreen = !fullScreen;
	}
	if (browser) {
		const fullscreenElement =
			document.fullscreenElement ||
			document.webkitIsFullScreen ||
			document.mozFullScreen ||
			document.msFullscreenElement;
		document.addEventListener('fullscreenchange', (e) => {
			if (!document.fullscreenElement) {
				fullScreen = false;
			}
		});
	}
</script>

<div class="flex justify-center items-center h-screen w-screen">
	<div class="container relative {fullScreen ? 'w-screen' : 'w-[700px]'} flex flex-col">
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
			class="w-full a"
			id="video"
			controls={false}
		>
			<track kind="captions" />
			Sorry, your browser doesn't support embedded videos.
		</video>

		<div
			class="controls p-2 flex items-center bg-[#5d57ff5a] justify-between {fullScreen
				? 'h-[65px] fixed w-full bottom-0'
				: 'h-auto absolute w-full bottom-0'} "
			id="controls"
		>
			<div>
				<button on:click={togglePlay}>
					{#if playing}
						<svg
							xmlns="http://www.w3.org/2000/svg"
							viewBox="0 0 24 24"
							fill="currentColor"
							class="w-6 h-6 text-[#5c57ff]"
						>
							<path
								fill-rule="evenodd"
								d="M6.75 5.25a.75.75 0 01.75-.75H9a.75.75 0 01.75.75v13.5a.75.75 0 01-.75.75H7.5a.75.75 0 01-.75-.75V5.25zm7.5 0A.75.75 0 0115 4.5h1.5a.75.75 0 01.75.75v13.5a.75.75 0 01-.75.75H15a.75.75 0 01-.75-.75V5.25z"
								clip-rule="evenodd"
							/>
						</svg>
					{:else}
						<svg
							xmlns="http://www.w3.org/2000/svg"
							viewBox="0 0 24 24"
							fill="currentColor"
							class="w-6 h-6 text-[#5c57ff]"
						>
							<path
								fill-rule="evenodd"
								d="M4.5 5.653c0-1.426 1.529-2.33 2.779-1.643l11.54 6.348c1.295.712 1.295 2.573 0 3.285L7.28 19.991c-1.25.687-2.779-.217-2.779-1.643V5.653z"
								clip-rule="evenodd"
							/>
						</svg>
					{/if}
				</button>
			</div>

			<progress class="basis-10/12" min="0" max="100" id="progress" on:input={setVideoProgress} />

			<div>
				<button on:click={toggleMute}>
					{#if muted}
						<svg
							xmlns="http://www.w3.org/2000/svg"
							viewBox="0 0 24 24"
							fill="currentColor"
							class="w-6 h-6 text-[#5c57ff]"
						>
							<path
								d="M13.5 4.06c0-1.336-1.616-2.005-2.56-1.06l-4.5 4.5H4.508c-1.141 0-2.318.664-2.66 1.905A9.76 9.76 0 001.5 12c0 .898.121 1.768.35 2.595.341 1.24 1.518 1.905 2.659 1.905h1.93l4.5 4.5c.945.945 2.561.276 2.561-1.06V4.06zM17.78 9.22a.75.75 0 10-1.06 1.06L18.44 12l-1.72 1.72a.75.75 0 001.06 1.06l1.72-1.72 1.72 1.72a.75.75 0 101.06-1.06L20.56 12l1.72-1.72a.75.75 0 00-1.06-1.06l-1.72 1.72-1.72-1.72z"
							/>
						</svg>
					{:else}
						<svg
							xmlns="http://www.w3.org/2000/svg"
							viewBox="0 0 24 24"
							fill="currentColor"
							class="w-6 h-6 text-[#5c57ff]"
						>
							<path
								d="M13.5 4.06c0-1.336-1.616-2.005-2.56-1.06l-4.5 4.5H4.508c-1.141 0-2.318.664-2.66 1.905A9.76 9.76 0 001.5 12c0 .898.121 1.768.35 2.595.341 1.24 1.518 1.905 2.659 1.905h1.93l4.5 4.5c.945.945 2.561.276 2.561-1.06V4.06zM18.584 5.106a.75.75 0 011.06 0c3.808 3.807 3.808 9.98 0 13.788a.75.75 0 11-1.06-1.06 8.25 8.25 0 000-11.668.75.75 0 010-1.06z"
							/>
							<path
								d="M15.932 7.757a.75.75 0 011.061 0 6 6 0 010 8.486.75.75 0 01-1.06-1.061 4.5 4.5 0 000-6.364.75.75 0 010-1.06z"
							/>
						</svg>
					{/if}
				</button>

				<button on:click={toggleFullScreen}>
					{#if fullScreen}
						<svg
							xmlns="http://www.w3.org/2000/svg"
							viewBox="0 0 24 24"
							fill="currentColor"
							class="w-6 h-6 text-[#5c57ff]"
						>
							<path
								fill-rule="evenodd"
								d="M3.22 3.22a.75.75 0 011.06 0l3.97 3.97V4.5a.75.75 0 011.5 0V9a.75.75 0 01-.75.75H4.5a.75.75 0 010-1.5h2.69L3.22 4.28a.75.75 0 010-1.06zm17.56 0a.75.75 0 010 1.06l-3.97 3.97h2.69a.75.75 0 010 1.5H15a.75.75 0 01-.75-.75V4.5a.75.75 0 011.5 0v2.69l3.97-3.97a.75.75 0 011.06 0zM3.75 15a.75.75 0 01.75-.75H9a.75.75 0 01.75.75v4.5a.75.75 0 01-1.5 0v-2.69l-3.97 3.97a.75.75 0 01-1.06-1.06l3.97-3.97H4.5a.75.75 0 01-.75-.75zm10.5 0a.75.75 0 01.75-.75h4.5a.75.75 0 010 1.5h-2.69l3.97 3.97a.75.75 0 11-1.06 1.06l-3.97-3.97v2.69a.75.75 0 01-1.5 0V15z"
								clip-rule="evenodd"
							/>
						</svg>
					{:else}
						<svg
							xmlns="http://www.w3.org/2000/svg"
							viewBox="0 0 24 24"
							fill="currentColor"
							class="w-6 h-6 text-[#5c57ff]"
						>
							<path
								fill-rule="evenodd"
								d="M15 3.75a.75.75 0 01.75-.75h4.5a.75.75 0 01.75.75v4.5a.75.75 0 01-1.5 0V5.56l-3.97 3.97a.75.75 0 11-1.06-1.06l3.97-3.97h-2.69a.75.75 0 01-.75-.75zm-12 0A.75.75 0 013.75 3h4.5a.75.75 0 010 1.5H5.56l3.97 3.97a.75.75 0 01-1.06 1.06L4.5 5.56v2.69a.75.75 0 01-1.5 0v-4.5zm11.47 11.78a.75.75 0 111.06-1.06l3.97 3.97v-2.69a.75.75 0 011.5 0v4.5a.75.75 0 01-.75.75h-4.5a.75.75 0 010-1.5h2.69l-3.97-3.97zm-4.94-1.06a.75.75 0 010 1.06L5.56 19.5h2.69a.75.75 0 010 1.5h-4.5a.75.75 0 01-.75-.75v-4.5a.75.75 0 011.5 0v2.69l3.97-3.97a.75.75 0 011.06 0z"
								clip-rule="evenodd"
							/>
						</svg>
					{/if}
				</button>
			</div>
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
	video::-webkit-media-controls-fullscreen-button {
		display: none;
	}

	progress {
		height: 9px;
		border: 0;
	}
	progress::-webkit-progress-bar {
		background-color: #f3f3f3;
		border-radius: 10px;
		border: 0;
	}
	progress::-webkit-progress-value {
		border: 0;
		border-radius: 10px;
		background-color: #5d57ff5a;
	}
</style>
