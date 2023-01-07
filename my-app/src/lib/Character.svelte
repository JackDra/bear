<script lang="ts">
	import { onDestroy } from 'svelte'
	import { GLTF, useGltfAnimations } from '@threlte/extras'

	let currentActionKey = 'idle'

	const { gltf, actions } = useGltfAnimations(({ actions }) => {
		// Uncomment to see all the different possible action keys
		// console.log(actions);
		// set the initial animation
		actions[currentActionKey]?.play()
	})

	function transitionTo(nextActionKey: string, duration = 1) {
		const currentAction = $actions[currentActionKey]
		const nextAction = $actions[nextActionKey]
		if (!nextAction || currentAction === nextAction) return
		// Function inspired by: https://github.com/mrdoob/three.js/blob/master/examples/webgl_animation_skinning_blending.html
		nextAction.enabled = true
		if (currentAction) {
			currentAction.crossFadeTo(nextAction, duration, true)
		}
		// Not sure why I need this but the source code does not
		nextAction.play()
		currentActionKey = nextActionKey
	}

	onDestroy(() => {
		// We unsubscribe otherwise we'd have old subscriptions still active
	})
</script>

<GLTF bind:gltf={$gltf} url="bear_nofur.glb" />
<!-- <GLTF bind:gltf={$gltf} url="https://threejs.org/examples/models/gltf/Xbot.glb" /> -->