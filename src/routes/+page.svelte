<script>
	import { browser } from '$app/environment';

	if (browser) {
	}
</script>

<svelte:head>
	<link
		rel="stylesheet"
		href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css"
	/>
</svelte:head>

<div class="video-container">
	<video
		id="video"
		preload="metadata"
		src="https://res.cloudinary.com/dvzkop7eh/video/upload/v1673052095/ad_mq7af1.mp4"
	/>
  <div class="controls">
    <button>
      <i class="fa fa-play"></i>
    </button>
  </div>
</div>

<style>
	.video-container {
		display: flex;
		width: 500px;
    height: 500px;
    flex-direction: column;
    position: relative;
		align-items: center;
		justify-content: center;
	}
	.video-container > video {
		width: 100%;
		height: 100%;
    position: absolute;
	}
  .controls{
    z-index: 9999999;
    width: 100%;
    justify-self: flex-end;
    position: relative;
    top: 6.5em;
    height: 50px;
    background-color: rgba(0, 0, 0, 0.337);
  }
</style>
