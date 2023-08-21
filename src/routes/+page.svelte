<script lang="ts">
	import {onMount} from 'svelte';
	import {Application, Texture, Sprite} from 'pixi.js';
	import {Viewport} from 'pixi-viewport';

	onMount(() => {
		const canvas = document.querySelector('#canvas') as HTMLCanvasElement;

		const app = new Application({
			view: canvas,
			resolution: 1, // window.devicePixelRatio || 1,
			// autoDensity: true,
			backgroundColor: 0x6495ed,
			resizeTo: window,
		});

		const viewport = new Viewport({
			// screenWidth: window.innerWidth,
			// screenHeight: window.innerHeight,
			worldWidth: 1000,
			worldHeight: 1000,

			events: app.renderer.events, // the interaction module is important for wheel to work properly when renderer.view is placed or scaled
		});

		// add the viewport to the stage
		app.stage.addChild(viewport);

		// activate plugins
		viewport.drag().wheel();


		// add a red box
		const sprite = viewport.addChild(new Sprite(Texture.WHITE));
		sprite.tint = 0xff0000;
		sprite.width = sprite.height = 100;
		sprite.position.set(100, 100);

	
	});
</script>

<canvas id="canvas" style="width:100%; height: 100%; display: block; position: absolute; top: 0; left: 0;" />
