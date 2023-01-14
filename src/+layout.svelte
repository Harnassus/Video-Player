<script>
    import '../app.css';
</script>

<!-- <svelte:head>
	<link
		rel="stylesheet"
		href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css"
	/>
</svelte:head> -->

<slot>
	<!-- {fullScreen ? 'mt-[40em]' : 'mt-[13.5em]'} -->
	<!-- .container {
		position: relative;
		width: 100%;
		height: 0;
		display: flex;
		flex-direction: column;
		 /* Aspect ratio of 16:9 */
	}
	video::-webkit-media-controls {
		display: none !important;
	}
	video::-webkit-media-controls-enclosure {
		display: none !important;
	}
	video::-webkit-media-controls-fullscreen-button {
		display: none;
	}

	.controls {
		display: flex;
		align-items: center;
		justify-content: space-between;
		position: absolute;
		width: 100%;
	}
	video {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
	}
	
	.controls input[type='range']::-webkit-slider-thumb {
		-webkit-appearance: none;
		appearance: none;
		width: 10px;
		height: 10px;
		border-radius: 50%;
		background: #fff;
		cursor: pointer;
	}
	:fullscreen .controls {
		position: fixed;
	} -->

</slot>